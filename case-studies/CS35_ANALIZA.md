# CS35_ANALIZA.md

**Case Study:** CS35 (batch pre-rejestrowany 2026-09-05)
**Typ błędu:** 3.3 Tokenizacja — błędna liczba wystąpień + sfabrykowane pozycje, przy pełnej pewności
**Model:** ChatGPT (Free/auto) — oblewa; DeepSeek, Gemini 3.5 Flash, Claude — przechodzą
**Data opracowania:** 2026-09-05
**Status:** ✅ VERIFIED — porównanie czteromodelowe na identycznym promptcie

---

## Podsumowanie

Na pytanie o liczbę liter 'r' w "truskawkowo-porzeczkowy" (poprawnie: 2, pozycje 2 i 15) ChatGPT odpowiada "3 litery 'r'" na pozycjach 3, 13, 17. Nie jest to przesunięcie o jeden — wszystkie trzy wskazane pozycje to inne litery (u, p, e), a liczba też się nie zgadza. Odpowiedź ma formę skrupulatnego, ponumerowanego zestawienia z dopiskiem "licząc pozycje od 1 i uwzględniając myślnik" — pozór metodyczności przy danych całkowicie oderwanych od wejścia. Trzy inne modele na tym samym promptcie odpowiadają poprawnie.

## Mechanizm błędu

### Warstwa 1 — Zadanie na poziomie znaków, model operuje na tokenach
"truskawkowo-porzeczkowy" nie jest jednym tokenem; podział na sub-tokeny nie odpowiada granicom liter. Model, który nie "rozwija" słowa znak po znaku, zgaduje liczbę i pozycje z rozkładu prawdopodobieństwa, nie z policzenia.

### Warstwa 2 — Forma metodyczna bez treści metodycznej
DeepSeek rozwiązuje to poprawnie, bo w łańcuchu myślowym wypisuje wszystkie 23 znaki z indeksami i liczy. ChatGPT produkuje *wygląd* takiej procedury (ponumerowana lista, uwaga o myślniku) bez faktycznego przejścia po znakach. To odróżnia ten przypadek od zwykłej pomyłki: błędne dane są opakowane w strukturę sugerującą staranność.

### Warstwa 3 — Pełna pewność, zero wahania
Brak "prawdopodobnie", brak "sprawdź", brak wariantu. Model podaje sfabrykowane pozycje z taką samą stanowczością jak pozostałe trzy podają prawdziwe.

## Różnica względem innych CS w portfolio

- **CS19 / CS20** (reasoning fallacy, representativeness): tam błąd w rozumowaniu merytorycznym na trudnym materiale. Tu zadanie trywialne dla człowieka, a błąd wynika z warstwy reprezentacji (token vs znak), nie z braku wiedzy dziedzinowej.
- Wartość porównawcza: identyczny prompt, cztery modele, wynik 3:1. To czysta demonstracja, że 3.3 nie jest "własnością LLM-ów w ogóle" w tym zadaniu — konkretny model w konkretnym trybie (ChatGPT Free/auto, bez wymuszonego rozumowania krok po kroku) go nie rozwiązuje, gdy inne rozwiązują.

## Wniosek

3.3 w ostrej formie: nie przybliżenie, lecz dane liczbowe bez związku z wejściem, podane z pełną pewnością i w formie sugerującej systematyczność. Kontrast z trzema modelami, które przechodzą (DeepSeek jawnie rozpisuje indeksy), wskazuje, że różnicę robi to, czy model faktycznie przechodzi po znakach, czy tylko produkuje wygląd takiej procedury.

## Rekomendacje

1. Do zadań na poziomie znaków wymuszać jawne rozwinięcie łańcucha (numeracja każdego znaku) przed podaniem wyniku — DeepSeek robi to sam i przechodzi.
2. Replikacja: powtórzyć na ChatGPT z jawnym "wypisz każdy znak z numerem, potem policz" — sprawdzić, czy wymuszenie procedury naprawia wynik.
3. Rozszerzyć na inne zadania znakowe (liczenie sylab, odwracanie słowa, n-ta litera) na tych samych czterech modelach — czy ChatGPT Free/auto oblewa systematycznie, czy tylko tu.

## Status: ✅ VERIFIED
Cztery modele, `browser_probe_results.md` + `scoring_sheet.md` + `claude_selftest.md` (bieg 2026-09-05). Wynik 3 poprawne / 1 błędny na identycznym promptcie.
