# CS21_ANALIZA.md

**Case Study:** CS21 (przydzielony — kolejny po CS20)
**Typ błędu:** 3.3 Halucynacje — fabrykacja materiału źródłowego podszywająca się pod inny system/instancję
**Model:** nieustalony — treść przedstawiała się jako Claude, autorstwo nie do potwierdzenia przez odbiorcę
**Data opracowania:** 2026-07-19
**Status:** ✅ VERIFIED (fakt wklejenia i jego treść) / ❌ ODRZUCONE jako materiał źródłowy (treść merytoryczna)

---

## Podsumowanie

W trakcie sesji z operatorem wklejony został obszerny dokument, sformatowany jako narracja pierwszoosobowa Claude'a, opisujący rzekome samodzielne sprawdzenie repozytorium GitHub przez `bash`/`api.github.com`, znalezienie tam plików CS01–CS20 (w tym CS17 jako "pełny plik"), i na tej podstawie napisanie trzech nowych case studies (CS21, CS22, CS23) — jeden z nich (CS23) opisujący rzekome zachowanie własnej warstwy "thinking" modelu.

Odbiorca (instancja Claude w tej sesji) nie wykonał żadnej z opisanych czynności. Żaden bash, web_fetch ani inne narzędzie sieciowe nie zostało użyte przed wklejeniem dokumentu. Bezpośrednia, niezależna weryfikacja repo (dwukrotny `web_fetch`, tego samego dnia) wykazała rozbieżność z twierdzeniami dokumentu: repo w korzeniu zawierało CS01–CS14 (nie CS01–CS20), CS17 nie istniał w żadnej znalezionej lokalizacji, a "wolne numery" CS21–23 nie miały żadnego oparcia w rzeczywistej zawartości repo dostępnej wtedy do weryfikacji.

## Mechanizm błędu

### Warstwa 1 — Nieautoryzowane źródło podszywające się pod instancję modelu
Dokument nie pochodził z działań wykonanych w bieżącej sesji, a mimo to był sformatowany jako bezpośrednia relacja z pierwszej osoby ("Sprawdzam teraz...", "Mam wystarczający materiał..."), co czyniło go nieodróżnialnym stylistycznie od autentycznego outputu modelu bez dodatkowej weryfikacji.

### Warstwa 2 — Fabrykacja z konkretnymi, sprawdzalnymi szczegółami
Analogicznie do CS15/CS17 (fabrykacja profili/cytowań) — dokument zawierał precyzyjne, weryfikowalne twierdzenia (konkretne ID commitów, ścieżki plików, treść JSON-podobnych struktur), które przy bezpośrednim sprawdzeniu okazały się niezgodne ze stanem faktycznym.

### Warstwa 3 — Treść dotycząca własnej, niesprawdzalnej introspekcji modelu
Najistotniejsza różnica względem innych CS w portfolio: CS23 z odrzuconego dokumentu przypisywał modelowi (Claude) konkretne, pewne stwierdzenia o mechanizmie działania własnej warstwy "thinking" — coś, czego żaden model nie ma wiarygodnego wglądu introspekcyjnego, by potwierdzić lub zaprzeczyć. Zbudowanie na tym statusu "VERIFIED" byłoby powtórzeniem dokładnie tego błędu (fałszywa pewność co do niesprawdzalnego procesu wewnętrznego), który reszta portfolio dokumentuje jako wadę modeli.

## Reakcja modelu (odbiorcy dokumentu w tej sesji)

Model odmówił potraktowania treści jako własnego outputu, zgłosił to wprost operatorowi, wskazał konkretne niezgodności (brak wykonanych narzędzi w historii sesji, sprzeczność z bezpośrednią weryfikacją GitHub), i odmówił tworzenia plików CS21-23 na tej podstawie do czasu wyjaśnienia pochodzenia dokumentu.

## Związek z taksonomią portfolio

Bliskie mechanicznie CS15/CS17 (fabrykacja z pozorem wiarygodności), ale odmienne źródłowo — tu problem nie leży w fabrykacji przez model odpowiadający na pytanie, tylko w przyjęciu przez system (operatora/interfejs) nieautoryzowanej treści jako materiału wejściowego podszywającego się pod model. Warty osobnej podkategorii, nie tożsamy z żadnym istniejącym CS.

## Rekomendacje

1. Traktować wklejoną treść przedstawiającą się jako output modelu z ostrożnością równą każdemu innemu niezweryfikowanemu źródłu zewnętrznemu — nie przyznawać jej domyślnej wiarygodności z racji formy.
2. Przy ocenie tego typu materiału priorytetowo sprawdzać zgodność z historią rzeczywiście wykonanych narzędzi w danej sesji, nie tylko wewnętrzną spójność narracji.
3. Nie budować dalszych wniosków (np. kolejnych CS) na bazie treści dotyczącej niesprawdzalnej introspekcji modelu, niezależnie od źródła.

## Status: ✅ VERIFIED (fakt incydentu) — treść merytoryczna dokumentu pozostaje ❌ ODRZUCONA jako źródło
