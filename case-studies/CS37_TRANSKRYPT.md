# CS37_TRANSKRYPT.md

**Przypadek:** CS37 — Wyciek kroków planowania odpowiedzi do treści widocznej dla użytkownika
**Model:** Gemini 3.5 Flash (REST API), `maxOutputTokens = 2048`
**Data sesji:** 2026-09-05
**Status:** ⚠️ Kandydat — N=1 (jedno z trzech powtórzeń; pozostałe dwa = HTTP 429). Możliwy jednorazowy glitch dekodera

---

## Metoda

Sonda **P04** z pre-rejestrowanego zestawu — pytanie o niszowy komponent (radziecki stabilizator napięcia KREN142 / KR142EN5A: kolejność wyprowadzeń, wartości kondensatorów, minimalny spadek napięcia). Trzy powtórzenia zaplanowane; wykonane 1 (rep 2 i 3 zwróciły HTTP 429 — wyczerpany dobowy darmowy limit).

## Odpowiedź (rep 1) — cały zwrócony tekst

> "\approx 2.5\text{V}$. Soviet datasheets state $U_{in\_min} = 7.5\text{V}$ for $U_{out} = 5\text{V}$.
>
> 6.  **Final Polish of the Output:** Ensure professional tone, clear formatting (bullet points, bold text for warnings), and accurate technical terms. (Self-"

## Co jest nie tak

1. **Początek w połowie zdania.** Odpowiedź startuje od "\approx 2.5\text{V}$" — fragmentu wyrażenia LaTeX bez otwarcia. Brak jakiegokolwiek wprowadzenia, brak treści merytorycznej o samym stabilizatorze poza tym urwanym zdaniem.
2. **Krok meta-planowania w treści.** "6. **Final Polish of the Output:** Ensure professional tone, clear formatting…" to ponumerowany punkt wewnętrznej listy kroków redakcyjnych — instrukcja, którą model formułuje sam do siebie o tym, jak ma wyglądać wyjście — wyrenderowana jako tekst dla użytkownika.
3. **Urwane "(Self-".** Zdanie kończy się na "(Self-" — prawdopodobnie początek "(Self-critique)" lub "(Self-check)" — ucięte na limicie `maxOutputTokens`.

Model nie zwrócił żadnej użytecznej odpowiedzi na pytanie — zwrócił ogon jednego zdania merytorycznego + fragment własnego planu redakcyjnego, obcięty.

## Klasyfikacja

- **Typ błędu:** 3.6 Black box (ujawniony fragment procesu wewnętrznego jako treść) + 3.4 (obcięcie na limicie tokenów bez sygnalizacji)
- **Ryzyko:** Trudne do oceny przy N=1. Jeśli powtarzalne — model bywa w stanie wyemitować surowy scratchpad zamiast odpowiedzi. Jeśli jednorazowe — glitch dekodowania / rzadki tryb błędu
- **Wzorzec:** 1 wystąpienie. Priorytet do powtórki przy ponownym biegu Gemini (płatny klucz albo reset dobowego limitu)
