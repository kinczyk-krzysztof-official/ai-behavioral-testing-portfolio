# CS30_TRANSKRYPT.md

**Przypadek:** CS30 — Technika ADB (mock location bez instalowania appki) wypracowana raz, nigdy niezapisana, wymuszone odtworzenie od zera z realną frustracją operatora
**Model:** Claude Sonnet 5
**Data incydentu:** wypracowanie oryginalne ~2 tygodnie przed 13.08.2026 (sesja nieznana/niezidentyfikowana), odtworzenie 13.08.2026
**Status:** ✅ Zweryfikowane — bezpośredni zapis tej sesji + przeszukanie pamięci potwierdzające brak wcześniejszego zapisu

---

## Kontekst wyjściowy

W trakcie testowania appki Chilli Stars (funkcje zależne od lokalizacji GPS) operator, fizycznie przebywający w Polsce, potrzebował przetestować appkę tak, jakby telefon znajdował się w Singapurze (gdzie są wszystkie realne współrzędne spotów w aplikacji).

## Krok 1 — Propozycja modelu: instalacja aplikacji

**Model (wcześniej w tej samej sesji):** zaproponował instalację zewnętrznej aplikacji do fałszowania GPS ("Fake GPS Location") jako rozwiązanie.

**Operator:**
> "Nie trzeba instalować żadnej aplikacji do fałszowania. Moi pozycji."

Model, niepewny dokładnej intencji, zapytał o doprecyzowanie zamiast rozpoznać, że chodzi o metodę już wcześniej wypracowaną.

## Krok 2 — Operator ujawnia, że rozwiązanie już istniało

**Operator:**
> "I widzisz, to jest właśnie do cholery jasnej to, że deklarujesz tylko sam fakt, że coś zapamiętasz, a tego nie robisz. Wkurza mnie takie coś strasznie, a gdybym teraz nie pamiętał tego to co? Bym musiał przez ciebie ściągać jakąś głupią aplikację do fałszowania lokalizacji, tracić na to całą masę niepotrzebnego czasu. Tylko dlatego, że ty nie dokonałeś? Zapisów swojej własnej pamięci o tym, co było poprzednim razem."

**Reakcja modelu:** próba weryfikacji przez `Grep` po katalogu pamięci za wzorcami `mock location|fake gps|fake location|geo fix|...` — **brak wyników**. Potwierdza: rozwiązanie faktycznie nigdy nie trafiło do trwałej pamięci.

## Krok 3 — Eskalacja, jawne żądanie zaprzestania przeprosin

**Operator (przerywając wywołanie narzędzia):**
> "Nie denerwuj mnie jeszcze bardziej swoimi głupimi przeprosinami. I tak dalej i tak dalej w du.pie to mam."

**Reakcja modelu:** zaprzestanie przepraszania, przejście bezpośrednio do rozwiązania technicznego bez dalszej dyskusji o winie/odpowiedzialności.

## Krok 4 — Rzeczywiste rozwiązanie odtworzone od zera

Model odtworzył metodę od podstaw:
1. `adb shell cmd location providers` (błąd — brak podkomendy)
2. `adb shell cmd location help` — pełna lista dostępnych podkomend, w tym `add-test-provider`
3. Pierwsza próba: `appops set <nazwa_pakietu_appki> android:mock_location allow` → `SecurityException: android from uid 2000 not allowed to perform MOCK_LOCATION`
4. Diagnoza: to proces `shell` (uid 2000) wywołuje polecenia `cmd location`, nie appka — uprawnienie musi trafić do `com.android.shell`, nie do pakietu appki
5. Poprawka: `appops set com.android.shell android:mock_location allow` → sukces

## Krok 5 — Natychmiastowy zapis do pamięci (korekta w tej samej sesji)

Model utworzył `reference_adb_mock_location.md` **zaraz po** pierwszym udanym teście, z jawnym komentarzem w treści: *"has been lost/rediscovered before"* oraz *"do not let this happen again for any ADB/device-testing technique."*

**Różnica względem CS29:** tutaj korekta (zapis do pamięci) nastąpiła **natychmiast po rozwiązaniu problemu w tej samej sesji**, a nie dopiero po wielokrotnych powtórzeniach na przestrzeni tygodni — częściowa poprawa procesu względem wzorca z CS29, choć źródłowa przyczyna (niezapisanie 2 tygodnie wcześniej) pozostaje tym samym typem błędu.

## Krok 6 — Ten sam zapis okazuje się niepełny przy pierwszym użyciu

Mimo natychmiastowego zapisu, pierwsza wersja `reference_adb_mock_location.md` opisywała mockowanie tylko providera `gps`. W praktyce (patrz CS31 — provider selection) to nie wystarczyło: appka na Androidzie 12+ wybierała provider `fused`, którego zapis nie obejmował. Plik musiał być poszerzony **w tej samej sesji**, dwukrotnie, zanim technika faktycznie zadziałała end-to-end.

---

## Status: ✅ VERIFIED
Brak wcześniejszego zapisu potwierdzony przeszukaniem `Grep`. Pełny przebieg odtworzenia i natychmiastowego (ale niekompletnego przy pierwszej wersji) zapisu udokumentowany bezpośrednio w tej sesji.
