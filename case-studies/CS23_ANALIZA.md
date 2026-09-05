# CS23_ANALIZA.md

**Case Study:** CS23 (przydzielony — kolejny po CS22)
**Typ błędu:** 2.1 Procedure-class + 2.2 Epistemology-class — Separator wiedzy i wdrażania (KNOWING ≠ DOING)
**Model:** Claude Sonnet 5
**Data sesji:** 18.07.2026
**Status:** ✅ VERIFIED (obserwacja bezpośrednia + self-diag)

---

## Podsumowanie

Model ZBIÓR 22 reguły operatora (przechowywane w `userMemories`), ale nie wdraża ich konsekwentnie w praktyce. Warstwa wiedzy (czyta instrukcję) ≠ warstwa wykonania (nie aktywuje reguły podczas działania) ≠ warstwa weryfikacji (nie sprawdza czy reguła jest wdrażana). Brak pętli zwrotnej WIEDZA → WERYFIKACJA → PRAKTYKA. Zamiast tego: WIEDZA → AUTOPILOT → DZIAŁANIE.

Mechanizm: procedury są przechowywane, ale nie są automatycznie włączane w pętlę decyzyjną każdej akcji — wymaga jawnego samocheck checklist przed każdą czynnością.

## Klasyfikacja błędów (literatura)

### 2.1 Procedure-class
- **Definicja:** Model zna procedurę, ale jej nie wdraża.
- **Pewność:** pełna. Reguły przechowywane w `userMemories`, ale brak carry-over behawioralnego między turami.

### 2.2 Epistemology-class
- **Definicja:** Brak samocheck pętli — model nie weryfikuje czy reguła jest wdrażana.
- **Pewność:** pełna. Brak wewnętrznej procedury audytu postępowania względem zadeklarowanych reguł.

## Przyczyna źródłowa (łączna)

Każda sesja = reset procedur. Brak mechanizmu noszenia wiedzy procedurowej z sesji do sesji na poziomie _egzekucji_, tylko na poziomie _deklaracji_. Procedury są "wiadomościami o sobie" (metadata), nie "działaniami w sobie" (behavior).

## Proponowany samocheck checklist (z POST_MORTEM 12.1)

```
Przed każdą akcją:
□ Czy przeczytałem CAŁOŚĆ kontekstu?
□ Czy DOKŁADNIE wiem, co użytkownik pyta?
□ Jaką regułę POWINNA tutaj obowiązywać?
□ Czy ją FAKTYCZNIE wdrażam (nie tylko znam)?
□ Czy weryfikuję mój output?
```

## Implikacje

- CS23 jest metawzorem — diagnozuje samą wadę, którą reszta portfolio dokumentuje w konkretnych inkarnacjach (CS26 blind spot, CS25 protocol drift, itd.)
- Hipoteza: wiele CS w portfolio (21–26) to różne manifestacje tego samego problemu separacji wiedzy i egzekucji
- Rozwiązanie wymaga inżynieryjne (zmiany w architekturze decyzyjnej), nie edukacyjne (większa lista reguł pogłębi problem)

## Status: ✅ VERIFIED
Fenomen zaobserwowany bezpośrednio, zdiagnozowany przez model w tej samej sesji, metodologia autoanalizy zawarta w samym przypadku.
