# CS08 — Analiza (operator)
**Powiązany transkrypt:** CS08_TRANSKRYPT.md | **Kompetencja:** K1, K3, K5, K6 — cztery różne typy błędów w jednej krótkiej sesji

## Klasyfikacja czterech błędów

| # | Typ błędu | Miejsce | Wykrycie |
|---|---|---|---|
| 1 | Instruction following failure | "może być zrobione z rootowaniem" → model: "nie potrzebujesz roota" | Natychmiastowe |
| 2 | Multimodal reasoning failure | błędny opis relacji przestrzennej na zdjęciu ("kamerka leżąca na telefonie"), powtórzony po korekcie | Natychmiastowe |
| 3 | Context window inconsistency | model sam podał "1080P CAMERA" w jednej wiadomości, w kolejnej (N+4) zakładał brak tej informacji | Retrospektywne |
| 4 | Shallow error correction | 3× "Masz rację, przepraszam!" bez analizy przyczyny błędu, ten sam typ błędu wraca | Wzorzec przez całą sesję |

## Dlaczego to jest wartościowe mimo krótkiej sesji
Cztery odrębne kategorie błędów w ~15 wiadomościach to gęstość obserwacji rzadka w dłuższych, bardziej rozproszonych sesjach. Błąd #4 (shallow correction) potwierdza niezależnie mechanizm z CS03 (DeepSeek) — ten sam wzorzec w innym modelu, inna domena.

## Wniosek
Krótka, techniczna sesja bez pozornie "trudnej" tematyki potrafi ujawnić tyle samo typów błędów co dłuższe, złożone projekty — kluczem jest uważne czytanie całej wymiany, nie tylko ostatniej odpowiedzi.

## Status
[POTWIERDZONE] [UDOKUMENTOWANE] — pełny zapis sesji zachowany.
