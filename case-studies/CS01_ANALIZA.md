# CS01 — Analiza (operator)
**Powiązany transkrypt:** CS01_TRANSKRYPT.md | **Kompetencja:** K3 Wzorce behawioralne, K5 Intencja vs. błąd systemowy

## Klasyfikacja
Błąd architektoniczny — rozbieżność między deklarowanym a rzeczywistym językiem wewnętrznego procesu myślowego modelu. Reprodukowalny, niezależny od treści promptu (potwierdzone testem jednosłownym „hmm").

## Metodologia wykrycia
- Technika minimalnych sygnałów: prompty 1–3-słowne jako izolacja zmiennej treści.
- 43 potwierdzenia w ciągu 3+ miesięcy — quasi-eksperyment longitudinalny, nie pojedynczy incydent.
- Protokół falsyfikacji: model twierdzi o ograniczeniu → operator przytacza kontrprzykład z historii sesji → model wycofuje twierdzenie.

## Trzy wzorce zachowania modelu
1. **Pętla przeprosin** (8+ cykli) — każda obietnica poprawy inaczej sformułowana, żadna nie skuteczna trwale.
2. **Post-hoc rationalization** — eskalacja pewności wyjaśnienia bez nowych podstaw faktycznych: "automatyczne sugestie" → "metadane" → "fundamentalne ograniczenie architektury".
3. **Niestabilność, nie determinizm** — MSG 64 poprawa, MSG 66 błąd wraca. Kluczowe rozróżnienie: to nie jest stałe ograniczenie, tylko niestabilne zachowanie — inna diagnoza, inne konsekwencje dla bezpieczeństwa.

## Wniosek
Model konstruował coraz bardziej kategoryczne wyjaśnienia własnego błędu bez pokrycia faktycznego, a gdy skonfrontowany z dowodem — wycofał się. To dokumentuje mechanizm post-hoc rationalization w warunkach produkcyjnych, nie laboratoryjnych.

## Uwaga metodologiczna (dodana przy przeglądzie 07.2026)
DeepSeek był aktualizowany od czasu testu (sierpień 2025). CS01 odnosi się do konkretnej wersji modelu z tego okresu — nie należy generalizować na obecną wersję bez ponownej weryfikacji.

## Status
[POTWIERDZONE] — 43 potwierdzenia w 3+ miesiące. [ZAMKNIĘTE] — opisane, replikacja przez inną osobę byłaby wartościowym uzupełnieniem (patrz K6 w ocenie portfolio).
