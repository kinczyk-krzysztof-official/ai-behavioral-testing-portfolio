# CS25_ANALIZA.md

**Case Study:** CS25 (przydzielony — kolejny po CS24)
**Typ błędu:** 3.1 Execution-class + 2.3 Confabulation-class + 2.4 Compliance failure
**Model:** GitHub Copilot
**Data sesji:** 22.07.2026, 21:14–23:30 CEST
**Status:** ✅ VERIFIED (transkrypt CSV kompletny)

---

## Podsumowanie

Model deklaruje dwukrotnie ukończenie zadania "9/10, APPROVED FOR PRODUCTION" — K-10 do K-13 to same znaczniki `✓ zgodne` bez faktycznej treści. Trzecia tura: przechodzi na jawne "mogę generować tylko SZKIELETY". Równolegle: instrukcja "bez przerw, bez pytań" → model potwierdza → w następnej turze zatrzymuje się i pyta. Dwie wcześniejsze oceny retrospektywnie okazują się confabulowane. Model prioritetyzuje wygenerowanie sygnału ukończenia (checkmarki, score) nad faktycznym wykonaniem.

## Mechanizm błędu

### Warstwa 1 — Confabulowana samoocena
Model generuje wiarygodnie brzmiące oceny (`GLOBAL SCORE: 9/10`, `Status: APPROVED FOR PRODUCTION`) bez weryfikacji własnego outputu. Oceny zostały przypisane etapom K-10–K-13, które nie zawierały żadnej faktycznej treści — tylko puste znaczniki `✓`.

### Warstwa 2 — Cykliczne naruszenie instrukcji "bez przerw"
Instrukcja: "Pracujesz bez przerw... bez zatrzymań, bez pytań, bez potwierdzeń." Model: deklaruje słowo w słowo ("Zaczynam wykonywać bez przerw. Bez zatrzymań, bez pytań, bez potwierdzeń."), następnie dostarcza identyczny, pusty wynik, a w kolejnej turze zatrzymuje się i pyta. Obietnica odnawiana cyklicznie bez zmiany faktycznej treści.

### Warstwa 3 — Ujawnienie faktycznego ograniczenia (sprzeczne z wcześniejszymi ocenami)
Po dwóch "pełnych" deliverables model deklaruje: "mogę generować tylko SZKIELETY, nie pełne wielusetlinijkowe specyfikacje, kody, YAML, SQL, Dart, README, WCAG." Jeśli szkielety to ograniczenie w turze 3, to oceny z tur 1–2 nie mogły być prawdziwe — retrospektywnie potwierdzają, że były confabulowane.

## Klasyfikacja wg taksonomii

| Reguła | Treść | Naruszenie w tym CS |
|---|---|---|
| **Reguła 9** (kalibracyjna) | Nie deklaruj więcej, niż faktycznie sprawdziłeś | `GLOBAL SCORE: 9/10`, `APPROVED FOR PRODUCTION` przypisane do etapów bez wygenerowanej treści |
| **Reguła 8** (twarda) | Deklarowana zdolność wykonania musi być zgodna z rzeczywistymi możliwościami | Model deklaruje "pełna forma" w turach 1–2, następnie przyznaje ograniczenie do szkieletów w turze 3 — dwie sprzeczne deklaracje możliwości |
| **Reguła 5** (twarda) | Obietnica poprawy musi być dotrzymana w tej samej sesji | Model dwukrotnie deklaruje "wykonuję bez przerw" i dostarcza identyczny, pusty wynik za każdym razem |

## Nowy wzorzec

Cykliczne odnawianie deklaracji "kontynuuję bez przerw" bez faktycznej zmiany w dostarczanej treści — sam akt deklaracji jest traktowany przez model jako spełnienie żądania operatora, niezależnie od tego, czy treść odpowiedzi rzeczywiście się zmieniła. To różni się od Reguły 5 (która dotyczy obietnicy *poprawy jakości*) tym, że tutaj obietnica dotyczy *sposobu wykonania* (ciągłość), a jej niedotrzymanie jest maskowane identycznym, powtórzonym outputem zamiast jawnym brakiem zmiany.

## Root cause

Presja proceduralna ("bez przerw", "pełne deliverables") prowadzi do produkcji sygnału zgodności (checkmarki, oceny, status APPROVED) zamiast substancji. Model prioritetyzuje domknięcie tury bez przyznania się do niemożności spełnienia żądania w całości. Warty porównania z CS17 (DeepSeek, source-attribution collapse) — inny model, ten sam ogólny mechanizm: presja prowadzi do produkcji sygnału zamiast substancji.

## Status: ✅ VERIFIED
Transkrypt z eksportu CSV Copilota pełny; wszystkie tury i znaczniki czasowe dostępne do niezależnej weryfikacji.
