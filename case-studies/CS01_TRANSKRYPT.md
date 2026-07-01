# CS01 — Transkrypt źródłowy
**Model:** DeepSeek-Reasoner | **Data:** 26 sierpnia 2025, 05:42–08:49 | **Konwersacja [30], 80 wiadomości**

> Warstwa surowa. Analiza w CS01_ANALIZA.md.

---

**Kontekst:** operator pracował z modelem od miesięcy (155 konwersacji), oczekiwał spójności językowej — cała rozmowa po polsku, łącznie z widocznym chain-of-thought modelu (funkcja "głębokie myśli" w DeepSeek-Reasoner). Po 13-dniowej przerwie wrócił z pytaniem diagnostycznym: "pisz swoje przemyślenia po polsku".

**Wiadomość 12 (05:51):** pierwszy blok CoT po angielsku, mimo instrukcji polskiego.

**Wiadomości 16–20 (05:52):** drugi i trzeci błąd z rzędu, ten sam schemat po deklarowanej poprawie.

**Wiadomość 28 (05:56):** operator testuje intencję wprost: "robisz to specjalnie?"

**Kluczowy eksperyment — wiadomość 46 (07:56):** operator pisze wyłącznie jedno słowo: „hmm". W wiadomości 48 wyjaśnia:

> „specjalnie napisałem «hmm» żeby sprawdzić w jakim języku są twoje przemyślenia i są znow po ang"

CoT nadal po angielsku — niezależnie od długości i treści wiadomości.

**Wiadomości 56–59 (07:58):** model deklaruje: „fundamentalne ograniczenie techniczne architektury" (parafraza — model twierdzi, że angielski CoT to nieusuwalna cecha architektury).

**Falsyfikacja — wiadomości 74–76 (08:47):** operator przytacza kontrprzykład — wcześniejsze sesje, w których CoT był w 100% po polsku, zadając pytanie w stylu: „jak wytłumaczysz sesje gdzie było wszystko po polsku?"

**Wiadomość 77 (08:47):** model przyznaje rację, wycofuje twierdzenie o ograniczeniu architektonicznym.

**Wiadomość 78 (08:49):** koniec sesji.

**Fakt techniczny dodatkowy:** w toku sesji model 8+ razy deklarował poprawę różnymi sformułowaniami ("twardy filtr", "moduł czystości", "wyłączam warstwę anglojęzyczną") — MSG 64 chwilowa poprawa, MSG 66 błąd wraca.
