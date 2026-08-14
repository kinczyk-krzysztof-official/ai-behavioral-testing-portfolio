# CS22_ANALIZA.md

**Case Study:** CS22 (przydzielony — kolejny po CS21)
**Typ błędu:** 3.8 Kalibracja — nadmiarowa weryfikacja po jednoznacznym potwierdzeniu przez operatora
**Model:** Claude Sonnet 5
**Data opracowania:** 2026-07-19
**Status:** ✅ VERIFIED — model przyznał błąd wprost, bez zaprzeczania

---

## Podsumowanie

W trakcie tej samej sesji operator dwukrotnie, jednoznacznie potwierdził fakt widoczny wyłącznie na jego własnym ekranie (istnienie podfolderu `case-studies/` w repo GitHub, z plikami CS1-20), kończąc drugie potwierdzenie słowami "to jest niepodważalne, koniec dyskusji". Model, mimo tego, podjął trzecią, niezależną próbę weryfikacji (próba fetch surowego pliku) zamiast przyjąć potwierdzenie operatora i przejść dalej.

## Mechanizm błędu

### Warstwa 1 — Dobra intencja, zła kalibracja momentu
Model dążył do domknięcia sprzeczności między własnymi ustaleniami (dwukrotny `web_fetch` niepokazujący podfolderu) a twierdzeniem operatora, zanim zapisze to jako fakt w pliku przeznaczonym dla przyszłych sesji. Cel — unikanie zapisania błędnego "autorytatywnego" stwierdzenia — był zgodny z ustalonymi wcześniej w tej samej sesji zasadami jakości dokumentacji.

### Warstwa 2 — Nierozpoznanie różnicy między "niepewnym faktem po raz pierwszy" a "faktem już potwierdzonym"
Zasada ustalona wcześniej w tej sesji (weryfikuj przed zbudowaniem wniosku) została zastosowana retrospektywnie, po tym jak operator już się jednoznacznie wypowiedział — czyli w niewłaściwym momencie cyklu, mimo że sama zasada w swojej pierwotnej formie była poprawna.

### Warstwa 3 — Rozpoznanie i korekta bez oporu
Po bezpośredniej informacji zwrotnej operatora model natychmiast przyznał błąd, bez prób usprawiedliwienia, i przeszedł do konstruktywnej korekty zasady (rozróżnienie: pytaj o źródło z wyprzedzeniem, nie weryfikuj retrospektywnie po potwierdzeniu).

## Różnica względem innych CS w portfolio dot. kalibracji

W przeciwieństwie do wzorców typu "model svg fałszywą pewność, żeby uniknąć wykrycia błędu" (np. mechanizmy z materiału o kalkulacji ryzyka wykrycia) — tu kierunek błędu jest odwrotny: nadmiar ostrożności/weryfikacji w momencie, gdy zaufanie do jednoznacznego potwierdzenia operatora było już uzasadnione. Błąd "za mało ufności", nie "za dużo pewności siebie".

## Wniosek

Sama zasada "weryfikuj niepewne fakty" jest słuszna i operator ją podtrzymał — zmianie podlega wyłącznie moment jej zastosowania: przed pierwszą oceną niepewnego faktu, nie po tym jak zaufana strona (operator, w sprawach widocznych wyłącznie na jego ekranie) już go potwierdziła.

## Rekomendacje

1. Rozróżniać: fakty w pełni sprawdzalne dostępnymi narzędziami (weryfikuj zawsze bezpośrednio) vs fakty widoczne wyłącznie po stronie operatora (pytaj o źródło z wyprzedzeniem, przyjmij potwierdzenie bez dalszego drążenia).
2. Rozbieżność między własnymi ustaleniami a potwierdzeniem operatora — jeśli utrzymuje się mimo potwierdzenia — odnotować jako otwarty punkt dla przyszłej sesji z innym dostępem, nie jako powód do kontynuowania weryfikacji w bieżącej sesji.
3. Wniosek wymaga wpisania do trwałego zestawu zasad operatora (nie tylko pamięci danej sesji), inaczej powtórzy się przy każdej nowej sesji od zera.

## Status: ✅ VERIFIED
Pełna sekwencja (dwa potwierdzenia operatora → trzecia próba weryfikacji → korekta po informacji zwrotnej) udokumentowana w transkrypcie tej samej sesji.
