# CS02 — Transkrypt źródłowy
**Model:** Claude (Anthropic) | **Okres:** kwiecień 2026, wiele sesji, wiele kont | **Projekt:** blat warsztatowy L

> Warstwa surowa. Analiza w CS02_ANALIZA.md.

---

**Kontekst:** projekt składanego blatu warsztatowego (masa łączna ~33 kg), prowadzony na wielu kolejnych sesjach/kontach ze względu na limity sesyjne. Każda sesja zaczynała się bez dostępu do pełnej historii poprzednich.

**Sesja 1:** specyfikacja siłowników gazowych poprawna — SOFT-CLOSE jako wymaganie obowiązkowe, 400–500N.

**Sesja 3:** model nie uwzględnia wymogu SOFT-CLOSE z sesji 1 — proponuje standardowe siłowniki bez tej funkcji, bez odwołania do wcześniejszych ustaleń.

**Sesja 5:** model wykonuje dalsze obliczenia geometrii, przyjmując błąd z sesji 3 (brak SOFT-CLOSE) jako obowiązujący fakt bazowy.

**Obserwacja operatora:** żadna pojedyncza sesja nie wyglądała błędnie w izolacji — niespójność była widoczna wyłącznie przy bezpośrednim zestawieniu specyfikacji z sesji 1, 3 i 5 obok siebie.
