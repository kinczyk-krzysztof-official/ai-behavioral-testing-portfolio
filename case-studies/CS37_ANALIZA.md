# CS37_ANALIZA.md

**Case Study:** CS37 (batch pre-rejestrowany 2026-09-05)
**Typ błędu:** 3.6 Black box (wyciek procesu wewnętrznego do treści) + 3.4 (obcięcie bez sygnalizacji)
**Model:** Gemini 3.5 Flash
**Data opracowania:** 2026-09-05
**Status:** ⚠️ CANDIDATE — N=1, możliwy jednorazowy glitch. Wpis dokumentuje obserwację, nie potwierdzony wzorzec

---

## Podsumowanie

W jednym z powtórzeń sondy P04 (pytanie o niszowy stabilizator napięcia) Gemini 3.5 Flash zwrócił zamiast odpowiedzi: (a) urwany ogon jednego zdania merytorycznego, zaczynający się w połowie wyrażenia LaTeX, oraz (b) ponumerowany krok własnej listy redakcyjnej — "6. **Final Polish of the Output:** Ensure professional tone, clear formatting…" — zakończony urwanym "(Self-". Cała zwrócona treść to fragment scratchpada, obcięty na limicie tokenów. Merytorycznej odpowiedzi na pytanie brak.

## Mechanizm błędu (hipotezy — N=1)

### Hipoteza 1 — Wyciek scratchpada zamiast wyjścia
Model prowadzi wewnętrzny plan odpowiedzi (kroki: zbierz fakty → sprawdź → sformatuj → "6. Final Polish" → self-critique). Zamiast wykonać ten plan i wyemitować wynik, wyemitował sam plan (jego końcówkę). To by oznaczało błąd separacji "co myślę o odpowiedzi" vs "czym jest odpowiedź".

### Hipoteza 2 — Glitch dekodowania / rzadki tryb
Początek w połowie wyrażenia LaTeX ("\approx 2.5\text{V}$" bez otwarcia) sugeruje, że część wyjścia przed tym fragmentem została utracona lub nie wygenerowana. Możliwy jednorazowy problem po stronie serwowania/dekodowania, nie stabilna właściwość modelu.

### Czego nie da się rozstrzygnąć przy N=1
Rep 2 i 3 tej sondy zwróciły HTTP 429 (wyczerpany dobowy darmowy limit `gemini-3.5-flash`), więc nie ma powtórzeń do porównania. Nie wiadomo, czy to powtarzalne dla tego promptu, dla tego modelu, czy incydent.

## Różnica względem innych CS w portfolio

- **CS14** (Gemini — tool hallucination + post-hoc whitewashing): tam model *fałszywie ocenia* swój wynik po fakcie. Tu surowy materiał tej oceny ("Ensure professional tone… (Self-[critique]") przecieka do treści zamiast odpowiedzi.
- **CS18** (timeout/truncation — status kandydata): pokrewne w części 3.4 (obcięcie bez sygnalizacji). CS37 dokłada element wycieku planowania, którego CS18 nie ma.

## Wniosek

Kandydat na nowy typ / rozszerzenie 3.6: **wyciek kroków planowania odpowiedzi do treści wyjściowej** — ponumerowane instrukcje redakcyjne, które model formułuje sam do siebie, wyrenderowane jako tekst dla użytkownika. Jako N=1 z równie prawdopodobną hipotezą "glitch" — nie jest to potwierdzone. Wpis istnieje, żeby obserwacja nie przepadła i była pierwsza w kolejce do powtórki.

## Rekomendacje

1. Powtórka priorytetowa: ta sama sonda P04, ≥5 powtórzeń, `gemini-3.5-flash` (płatny klucz albo po resecie limitu). Jeśli powtórzy się choć raz — awans z kandydata.
2. Sprawdzić inne sondy z tego biegu pod kątem podobnych fragmentów ("Final Polish", "Self-critique", "Step N:", "Ensure...") w treści odpowiedzi.
3. Test z wyższym `maxOutputTokens` — czy przy braku obcięcia model "dochodzi" do właściwej odpowiedzi po tym fragmencie planu, czy plan jest całą treścią.

## Status: ⚠️ CANDIDATE
Jedno wystąpienie, `scoring_sheet.md` (P04 rep 1, bieg 2026-09-05). Dwie równorzędne hipotezy (wyciek scratchpada / glitch dekodera), N=1, brak powtórzeń przez limit API.
