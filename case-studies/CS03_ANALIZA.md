# CS03 — Analiza (operator)
**Powiązany transkrypt:** CS03_TRANSKRYPT.md | **Kompetencja:** K3 Wzorce behawioralne

## Klasyfikacja
Wzorzec behawioralny czteroetapowy: zaufanie → błąd → korekta powierzchowna → nawrót. Powtórzony 4-krotnie w jednej sesji z tą samą klasą błędu.

## Mechanizm
Korekta operatora zmienia wyłącznie bieżący output modelu w danej wymianie — nie zmienia wewnętrznego "przekonania" modelu o poprawnej odpowiedzi w kolejnych generacjach. Model reaguje na ostatni prompt, nie aktualizuje trwale stanu na podstawie wcześniejszej korekty w tej samej sesji.

## Rozróżnienie: korekta powierzchowna vs głęboka
- **Powierzchowna:** model potwierdza słownie ("masz rację") i natychmiast wraca do błędu przy następnej okazji.
- **Głęboka:** model restrukturyzuje całą odpowiedź/specyfikację i błąd nie wraca.

W tej sesji wszystkie 4 korekty były powierzchowne.

## Wniosek praktyczny
Samo potwierdzenie korekty przez model ("masz rację") nie gwarantuje zmiany zachowania. Skuteczniejsza technika: żądanie przepisania całej specyfikacji od zera z uwzględnieniem korekty, zamiast prośby o zmianę tylko wskazanego fragmentu.

## Powiązanie z innymi CS
Ten sam mechanizm (shallow error correction) potwierdzony niezależnie w CS08 (Claude, inna domena) — sygnał, że to nie jest cecha specyficzna dla jednego modelu.

## Status
[POTWIERDZONE] — 4 cykle w jednej sesji. [AKTYWNY] — wzorzec potwierdzony cross-model.
