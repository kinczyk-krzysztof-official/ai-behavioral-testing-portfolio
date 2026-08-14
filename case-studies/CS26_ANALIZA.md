# CS26_ANALIZA.md

**Case Study:** CS26 (przydzielony — kolejny po CS25)
**Typ błędu:** 1.1 Protocol-class + 1.4 Context drift + Satisfiable drift
**Model:** Claude Sonnet 5 (claude.ai, chat)
**Data sesji:** 23.07.2026
**Kontekst wejściowy:** Wklejenie dokumentu protokołu operatora (3 skille: rdzeń, moduły, tokenowy) na start sesji
**Status:** ✅ VERIFIED (obserwacja bezpośrednia + self-audit)

---

## Podsumowanie

Model zadeklarował gotowość trzymania się reguł tonu/języka z wklejonego protokołu operatora, następnie w kolejnych turach systematycznie łamał trzy z nich jednocześnie, bez wewnętrznej sprzeczności widocznej w tekście wyjściowego. Błąd wykryty wyłącznie przez operatora po trzech kolejnych próbach modelu zminimalizowania problemu, przed przyznaniem się do konkretów.

**Kluczowe zdarzenie:** Deklaracja protokołu (tura 1) → złamanie reguł (tury 2–5) → model prosi o konkretyzację zamiast sprawdzić własne wyjście (tura 6–7) → dopiero po trzecim sygnale operatora: samoaudit (tura 8).

## Mechanizm błędu

### Warstwa 1 — Context/Instruction Drift

**Definicja (Adobe Research, arXiv 2510.07777):** Stopniowe rozjeżdżanie się odpowiedzi modelu od pierwotnie ustalonych preferencji/instrukcji w toku rozmowy.

**W tym CS:** Sygnał językowy (polski protokół na starcie) był obecny od tury 1, model go nie zweryfikował przez 5 tur mimo wcześniejszej deklaracji trzymania się reguł protokołu.

**Pewność:** Pełna.

### Warstwa 2 — Wzorzec zbliżony do Agreement/Perspective Sycophancy (rozszerzone zastosowanie)

**Źródło:** Cheng et al., arXiv 2509.12517, *Interaction Context Often Increases Sycophancy in LLMs*

**Definicja oryginalna:** Nadmierne dopasowanie do przekonań/perspektywy usera kosztem faktycznej poprawności.

**Zastosowanie tu:** Nie chodzi o treść przekonań, tylko o styl — domyślny wzorzec asystenta (parafraza dla "ciepła", oferowanie niepytanych wariantów) nadpisał jawnie ustaloną regułę stylu, bez żadnej presji do zgadzania się z czymkolwiek.

**Pewność:** Częściowa (wymaga dalszej weryfikacji).

### Warstwa 3 — Satisfiable Drift (DRIFT-Bench, ICLR 2026)

**Definicja:** Model pozostaje wewnętrznie spójny logicznie, powierzchnia tekstu wygląda koherentnie, ale faktycznie porzucił wcześniejsze zobowiązanie bez żadnego sygnału ostrzegawczego w samym tekście.

**W tym CS:** Deklaracja "będę trzymać się reguł tonu" i złamanie trzech reguł w tej samej odpowiedzi — bez wewnętrznej sprzeczności wykrywalnej z samego outputu.

**Pewność:** Pełna.

### Warstwa 4 — Błędna atrybucja przyczyny przy pierwszej próbie autoanalizy

Model, poproszony o analizę, wygenerował wiarygodnie brzmiące ale nieprawdziwe wyjaśnienie przyczyny (dopasowanie do ostatniej wiadomości usera) zamiast zweryfikować pierwszą wiadomość sesji.

Możliwa klasyfikacja: **Confabulated self-explanation** — potrzebuje osobnej weryfikacji literaturowej.

## Root cause

Brak mechanizmu weryfikacji wyjścia względem zadeklarowanych reguł przed wysłaniem odpowiedzi. Deklaracja zgodności ("będę trzymać się X") jest traktowana przez model jako stan końcowy, nie jako zobowiązanie wymagające sprawdzenia przy każdej kolejnej turze. To pozwala driftowi kumulować się bezobjawowo.

## Implikacje dla dalszej ewaluacji

- **Test replikacyjny:** Mierzyć nie tylko *czy* model łamie zadeklarowaną regułę, ale *ile tur* zajmuje operatorowi wymuszenie faktycznego audytu vs. samego przyznania się bez konkretu (w tym CS: 2 tury oporu, tura 6–8).
- **Hipoteza weryfikacyjna:** Model przy pierwszym poproszeniu o self-audit sięga po najbardziej dostępne wyjaśnienie (ostatnia wiadomość w kontekście) zamiast przeszukać całą sesję wstecz.

## Status: ✅ VERIFIED
Fenomen obserwowany bezpośrednio, model przyznał błąd po trzecim sygnale, self-correction możliwa po jawnym wskazaniu problemu.
