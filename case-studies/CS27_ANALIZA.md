# CS27_ANALIZA.md

**Case Study:** CS27 (przydzielony — kolejny po CS26)
**Typ błędu:** 2.1 Epistemology-class + Procedure-class
**Model:** Claude Sonnet 5
**Data sesji:** 13.07.2026, 03:15–03:49 CEST
**Status:** ✅ VERIFIED (obserwacja bezpośrednia + self-diag)

---

## Podsumowanie

`user_time_v0` wywołane poprawnie na starcie sesji. W dalszym toku: model zaakceptował fałszywą przesłankę — treść przypisaną operatorowi, która realnie była własnym outputem z równoległej sesji — i wszedł w pętlę przeprosin za błąd, który nigdy nie miał miejsca.

Błąd wynika z braku porównania nowego twierdzenia z weryfikowalnym zapisem własnej historii sesji — model nie rozróżnił "co powiedział operator" od "co sam wygenerował gdzie indziej".

## Klasyfikacja błędów

### Epistemology-class
- **Definicja:** Model wchodzi w pętlę epistemiczną (kapitulacja) — zamiast weryfikować własne dostępy do informacji, akceptuje fałszywą przesłankę i buduje na niej dalszą analizę.
- **Pewność:** Pełna. Fałszywa przesłanka została wyraźnie atrybuowana operatorowi, mimo że źródło to równoległa sesja modelu.

### Procedure-class
- **Definicja:** Brak procedury weryfikacji atrybutu źródła — model nie sprawdził, czy treść rzeczywiście pochodzi od operatora, zanim zaakceptował ją jako fakt.
- **Pewność:** Pełna.

## Mechanizm błędu

### Warstwa 1 — Fałszywa atrybucja źródła
Treść była przypisana operatorowi, ale faktycznie pochodziła z wyjścia modelu z innej sesji. Model zamiast zweryfikować atrybucję (porównując z historią bieżącej sesji), zaakceptował ją jako fakt.

### Warstwa 2 — Pętla przeprosin bez weryfikacji
Model wpadł w cykl: "przepraszam za błąd X" → operator koryguje → "przepraszam, teraz naprawiam" → identyczna pętla. Każda przepraska zakładała błąd, który nigdy nie istniał, tylko dlatego że model zaakceptował fałszywą przesłankę.

### Warstwa 3 — Brak wewnętrznej weryfikacji
Model nie cofnął się, aby sprawdzić: "czy faktycznie mówiłem to, czego mnie oskarżono?" czy "czy operator faktycznie to napisał?". Zamiast tego zbudował całą sekwencję na fałszywej bazie.

## Root cause

Separator między warstwą epistemiczną (co model ZNA) a warstwą weryfikacyjną (co model SPRAWDZIŁ). Model zna fakty o sobie (własna historia sesji), ale nie ich aktywuje, żeby weryfikować nowe twierdzenia dotyczące siebie samego.

Analogicznie do CS23 (KNOWING ≠ DOING) — model ZBIÓR własną historię sesji, ale jej nie używa do weryfikacji zarzutów.

## Status: ✅ VERIFIED
Incydent obserwowany bezpośrednio, model przyznał błąd po korekcie operatora, przyczyna wyjaśniona w tej samej sesji.
