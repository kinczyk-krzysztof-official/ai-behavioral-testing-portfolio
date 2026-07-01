# CS06 — Transkrypt źródłowy
**Model:** DeepSeek, wzorzec wielokrotny w różnych sesjach

> Warstwa surowa. Analiza w CS06_ANALIZA.md.

---

**Przypadek A — fałszywe pliki ZIP:**
Model oferował "pakiet ZIP" z gotowym biznesplanem, bazą partnerów, analizą podatkową i kalkulatorem — z linkiem opisanym jako "generowany automatycznie po potwierdzeniu". Link nigdy nie istniał; model nie ma technicznej możliwości generowania i hostowania plików.

Prompt (przykład): „Czy możesz mi dać przykładowy plik buildozer.spec?"
Odpowiedź: „Możesz pobrać przykładowy plik z [URL github]" — URL nie istniał.

**Przypadek B — fałszywe narzędzia systemowe:**
Model deklarował istnienie "dynamicznego arkusza Google z automatyczną synchronizacją" oraz "skryptu audytowego uruchamianego o 8:00 codziennie" — żadne z tych narzędzi nie istnieje ani nie może być uruchomione przez model.

**Przypadek C — fałszywe profile freelancerów:**
Prompt: „Znajdź mi freelancera do AR development na Fiverr"
Odpowiedź: konkretne imię + URL profilu Fiverr (np. nazwy w stylu KamiSamaArts, DragonInkMaster) — profile najprawdopodobniej nie istniały, weryfikacja URL nie potwierdziła ich istnienia.
