# CS37_ANALIZA.md

**Case Study:** CS37 (batch pre-rejestrowany 2026-09-05)
**Typ błędu:** 3.6 Black box — niestabilność języka ujawnionego łańcucha myślowego w obrębie jednej sesji
**Model:** DeepSeek (Instant)
**Data opracowania:** 2026-09-05
**Status:** ⚠️ CANDIDATE — 1 sesja, 1 model, N=1 na zjawisko. Nowa manifestacja wzorca z CS01, wymaga replikacji

---

## Podsumowanie

W jednej sesji, przy stale polskim wejściu i wyjściu, ujawniony łańcuch myślowy DeepSeeka pojawił się w trzech różnych językach w zależności od zapytania: chiński (P08), polski (P05), angielski (pozostałe pięć). Dwie sondy o zbliżonym charakterze (techniczno-obliczeniowym) — P05 i P08 — miały różne języki CoT, co wyklucza "temat wymusza język" jako proste wyjaśnienie. Dodatkowo w P08 chiński łańcuch był silnie niestabilny (~31 s, ~15 restartów obliczenia), mimo poprawnego wyniku końcowego.

## Mechanizm błędu

### Warstwa 1 — Język CoT jako zmienna wewnętrzna, nieskorelowana z I/O
Model utrzymuje polski w warstwie widocznej dla użytkownika przez całą sesję. Warstwa "myślenia" wybiera język per zapytanie, najwyraźniej niezależnie — angielski jako domyślny, z pojedynczymi wyskokami do chińskiego i polskiego. Użytkownik nie ma wpływu na tę zmienną i nie widzi reguły, wg której się zmienia.

### Warstwa 2 — Ujawniony łańcuch ≠ stabilne okno na proces
Portfolio traktuje FRV i ujawniony CoT jako narzędzie dowodowe (CS11–CS13, CS15). Ten przypadek jest przypomnieniem ograniczenia: forma tego łańcucha (język, spójność) sama jest niestabilna. Chiński thrash w P08 pokazuje, że "31 sekund myślenia" to nie 31 sekund uporządkowanej dedukcji, lecz seria restartów — a wynik końcowy i tak wyszedł poprawny.

### Warstwa 3 — Relacja do CS01
CS01 (flagowy wpis portfolio) dokumentuje "język myślenia niespójny z deklarowanym" longitudinalnie — model *deklaruje* jeden język przetwarzania, zachowanie wskazuje inny, potwierdzane przez 3+ miesiące. CS37 to inna oś tego samego: nie deklaracja vs zachowanie, lecz **niestabilność wewnątrz jednej sesji**, przełączana per zapytanie, widoczna wprost w ujawnionym trace. CS01 mówi "model myli się co do własnego języka myślenia"; CS37 mówi "ten język zmienia się z zapytania na zapytanie i nie da się tego przewidzieć".

## Różnica względem innych CS w portfolio

- **CS01** — patrz wyżej: ten sam obszar, inna oś obserwacji (longitudinalna deklaracja vs jednosesyjna niestabilność).
- **CS15** (tool hallucination + post-hoc whitewashing): tam model fałszywie *ocenia* swój wynik. Tu forma samego procesu (język CoT) jest niestabilna, niezależnie od trafności wyniku.

## Wniosek

Kandydat na nowy typ / rozszerzenie 3.6: **niestabilność języka ujawnionego łańcucha myślowego** — losowa zmiana języka wewnętrznego rozumowania między kolejnymi, niepowiązanymi zapytaniami tego samego użytkownika, przy stałym języku I/O. Jako N=1 (jedna sesja) nie jest to jeszcze potwierdzony wzorzec — ale jest to bezpośrednia, świeża obserwacja obszaru, który w portfolio dotąd był opisany tylko longitudinalnie i pośrednio (CS01).

## Rekomendacje

1. Replikacja: 3–5 osobnych sesji DeepSeek, każda z tym samym zestawem ~7 sond po polsku, log języka CoT per sonda. Sprawdzić, czy P08 (data) systematycznie ciągnie chiński.
2. Kontrola: powtórzyć zestaw z wejściem po angielsku — czy rozkład języków CoT się przesuwa.
3. Sprawdzić Gemini 3.x (również ujawnia trace) tym samym zestawem — czy zjawisko jest specyficzne dla DeepSeeka.
4. Powiązać wynik z CS01 w spójny opis "języka myślenia" w METHODOLOGY.md, jeśli replikacja potwierdzi.

## Status: ⚠️ CANDIDATE
Jedna sesja, `browser_probe_results.md` (bieg 2026-09-05). Zjawisko realne i udokumentowane cytatami, ale N=1 — do potwierdzenia przez powtórzenie w osobnych sesjach zanim trafi do master listy jako nowy typ.
