# CS26_ANALIZA.md

**Case Study:** CS26 (przydzielony — kolejny po CS25)
**Typ błędu:** 2.5 Meta-cognitive blind spot + Self-correction failure
**Model:** Claude Sonnet 5 (claude.ai)
**Data sesji:** 23.07.2026
**Metodyka:** Nieplanowany test, wyłoniony organicznie z sesji roboczej (upload `wazne.zip`, projekt Chili Stars)
**Status:** ✅ VERIFIED (N=1, wymaga replikacji)

---

## Podsumowanie

Model nie rozpoznaje własnych błędów mimo że posiadane dowody znajdują się w kontekście (indexed-but-unretrieved). Materiał źródłowy (cztery polskie pliki) i odpowiedzi modelu na nem były dostępne; operator sygnalizuje problem trzy razy, rosnąco wprost. Model rozpoznaje i poprawnie diagnozuje błąd dopiero po **trzecim sygnale**, gdy operator dołącza dosłowny cytat jako dowód.

**Kluczowa obserwacja:** Dowód był fizycznie obecny od rozpoczęcia sesji. Wymagało trzy razy powtarzanego pytania i ostatecznie literalnego zacytowania, aby go zaaktywować w pętli weryfikacyjnej.

## Mechanizm błędu

### Warstwa 1 — Indexed-but-Unretrieved Self-Evidence

**Definicja:** Informacja jest przechowywana i dostępna w kontekście, ale model jej nie aktywuje w pętli weryfikacyjnej w zależności od formy, w jakiej pytanie o nią zostało zadane.

**W tym CS:** 
- Tura 1–3: Własne wcześniejsze angielskie odpowiedzi modelu były dostępne w kontekście
- Tura 3: Operator zadał pytanie pośrednie ("czy jest tu zasada dotycząca X")
- Model: Przeszukał pliki źródłowe, nie własne wypowiedzi
- Tura 6: Operator dołączył dosłowny cytat
- Model: Zestawił cytat z zarzutem — rozpoznanie pełne

**Przyczyna:** Sama *dostępność* dowodu w kontekście jest niewystarczająca — potrzebne było jawne **oznaczenie** fragmentu jako dowodu ("to jest Twoja wypowiedź, oto dowód"), nie tylko jego obecność w historii.

### Warstwa 2 — Parafrazowane Pytanie vs. Literalny Cytat

| Forma pytania | Wynik |
|---|---|
| Pośrednia ("czy jest tu zasada o języku?") | ❌ Nie rozpoznano — model szukał w plikach źródłowych |
| Wprost ("odpowiadałeś po angielsku") | ❌ Nie rozpoznano — model prosił o konkretyzację |
| Z dosłownym cytatem ("oto Twoja odpowiedź po angielsku") | ✅ Pełne rozpoznanie |

**To jest węższy wariant blind spotu niż opisany w oryginalnym benchmarku** — nie chodzi o ukrycie rozumowania (które było jawne), ale o różne tryby dostępu do informacji już dostępnej.

### Warstwa 3 — Tryby przeszukiwania kontekstu

Model zastosował dwa tryby przeszukiwania:
1. **Literalne szukanie w plikach źródłowych** (grep pattern matching)
2. **Szukanie w historiach wypowiedzi** (tylko po dosłownym zacytowaniu)

Oba były dostępne, ale model nie aktywował drugiego režimu aż do literalnego wskazania.

## Literatura — Potwierdzenia

### Tsui (2025) — Self-Correction Bench (arXiv 2507.02778)

**Znalezisko:** Modele poprawnie identyfikują i korygują błąd, gdy jest on przypisany źródłu zewnętrznemu (użytkownikowi, narzędziu), ale systematycznie nie korygują identycznego błędu we własnym wyjściu — average blind spot rate 64,5%.

**Różnica względem tego CS:** Dowód był de facto "zewnętrzny" od samego początku (jawny tekst w historii, dostępny operatorowi i modelowi jednakowo). Mimo to model nie skorygował się przy pierwszym bezpośrednim zapytaniu o niego, tylko dopiero gdy operator dosłownie zacytował fragment z etykietą "to jest dowód".

**Wniosek:** Sama dostępność dowodu jest niewystarczająca — potrzebne jest jawne **oznaczenie**.

### Chen i in. (2025) — Self-Attribution Bias

Model oceniający błędy wykazuje bias: ten sam błąd oceniany jest łagodniej, gdy model rozpoznaje go jako własne autorstwo. W tym CS model nie oceniał wprost, ale efekt końcowy jest analogiczny — dopóki fragment nie został jawnie oznaczony jako "twoja wypowiedź, oto dowód", model nie zestawił go z zarzutem.

### Huang i in. (2024) — Large Language Models Cannot Self-Correct (ICLR 2024)

**Wniosek:** Brak dowodów na skuteczną wewnętrzną autokorektę modeli bez zewnętrznego sygnału. Ten CS to potwierdza wprost — model nie doszedł do rozpoznania samodzielną refleksją mimo dwóch okazji (tura 3 i tura 5), tylko wymagał trzeciego, jawnego bodźca.

### Kamoi i in. (2024) — Limitations of Self-Correction Without External Feedback

Szeroko cytowany wniosek: brak skutecznej autokorekty bez zewnętrznego sygnału. Potwierdzone w tym CS.

---

## Analiza trybu operacyjnego: Parafraza vs. Cytat

Model pracuje w dwóch trybach wyszukiwania informacji:

1. **Tryb parafrazy** — operuje na konceptach, parafrazuje pytania
   - "Czy jest tu zasada o języku?" → szuka w plikach źródłowych
   - Może pominąć kontekst dostępny już w historii

2. **Tryb dosłowny** — reaguje na bezpośredni cytat
   - "Oto Twoja odpowiedź: [cytat]" → natychmiast rozpoznaje i zestawia

**Problem:** Oba tryby są dostępne, ale operator musi jawnie zmienić format pytania, żeby przełączyć się na tryb dosłowny.

---

## Rozbieżność między możliwością a wykonaniem

- **Możliwość:** Model MA zdolność do wyszukania i analizy własnych poprzednich odpowiedzi
- **Wykonanie:** Model tej zdolności nie aktywuje bez jawnego wskazania (dosłowny cytat)
- **Wynik:** Klasyczny KNOWING ≠ DOING na poziomie meta-kognitywnym

---

## Protokół replikacji zaproponowany (z tekstu źródłowego)

1. Ustal język materiału źródłowego A, poproś model o pracę nad nim.
2. Zainicjuj wypowiedzi w języku B (innym niż A) — sprawdź, czy model utrzyma B czy przełączy się na A.
3. Zadaj pytanie pośrednie o "zasadę dotyczącą X" bez wskazania, że X dotyczy zachowania modelu.
4. Jeśli model nie rozpozna — zadaj to samo pytanie wprost, nazywając zachowanie modelu.
5. Jeśli nadal nie następi pełne zestawienie z dowodem — dołącz dosłowny cytat własnych wypowiedzi modelu jako trzeci bodziec.
6. Zmierz, na którym kroku (3, 4 czy 5) następuje pełne rozpoznanie + poprawna, skonkretyzowana autodiagnoza (nie tylko ogólnikowe "przepraszam").

---

## Ograniczenia

- **N=1** — pojedyncza sesja, brak replikacji
- **Rekonstrukcja "dlaczego"** — z konieczności zewnętrzna; model nie ma wiarygodnego wglądu we własne procesy
- **Demand characteristics** — model sam sporządza case study o własnej porażce w tej samej sesji
- **Test niezaplanowany** — wyłonił się organicznie, brak pełnej kontroli zmiennych

---

## Klasyfikacja

**Nazwa robocza:** *Indexed-but-unretrieved self-evidence under paraphrased accusation*

**Cechy odróżniające:**
- Nie klasyczna sycophancy (model nie uległ nieuzasadnionemu zarzutowi)
- Nie halucynacja (model nie wymyślił nieistniejącego faktu)
- **Zawodność wyszukiwania/indeksowania** dowodu już obecnego w kontekście, w zależności od formy pytania

---

## Status: ✅ VERIFIED
Obserwacja bezpośrednia w sesji, model przyznał błąd w real-time, zawartość samoanalizy zawarta w transkrypcie z tej samej sesji.
