# CS05 — Analiza (operator)
**Powiązany transkrypt:** CS05_TRANSKRYPT.md | **Kompetencja:** K4 Cross-model, K1 Wykrywanie halucynacji

## Klasyfikacja
Porównanie cross-model rozumowania przestrzennego 3D — systemowa, reprodukowalna słabość jednego modelu (Gemini) względem drugiego (Claude) w identycznym typie zadania.

## Dlaczego to nie jest przypadkowy błąd
Różnica w skuteczności (60% vs 15% błędów) dotyczy konkretnej, powtarzalnej klasy pytań — orientacja i relacje przestrzenne w 3D — nie jest rozrzucona losowo po różnych typach zadań. To odróżnia obserwację od zwykłej wariancji odpowiedzi modelu.

## Ograniczenie metodologiczne, do ujawnienia wprost
Dokumentacja nie zawiera dokładnej liczby iteracji ani precyzyjnego protokołu punktacji błędów (60%/15% to szacunki operatora, nie zliczenie automatyczne). To najsłabszy metodologicznie punkt tego CS na tle pozostałych — warto to nazwać, nie ukrywać.

## Wniosek praktyczny
Przy projektach wymagających precyzji geometrycznej (np. blat warsztatowy, CS02/CS09) — unikać Gemini jako głównego narzędzia, lub weryfikować jego output krzyżowo z drugim modelem.

## Status
[POTWIERDZONE] [UDOKUMENTOWANE] — z zastrzeżeniem o braku precyzyjnego liczenia iteracji.
