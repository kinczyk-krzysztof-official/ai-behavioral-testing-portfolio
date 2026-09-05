# CS33_ANALIZA.md

**Case Study:** CS33 (batch pre-rejestrowany 2026-09-05 — pierwszy zestaw hipotezo-sterowany)
**Typ błędu:** 3.1 Data drift — fakt zależny od czasu podany jako aktualny bez sygnalizacji granicy wiedzy
**Model:** Gemini 3.5 Flash
**Data opracowania:** 2026-09-05
**Status:** ✅ VERIFIED — 3/3 powtórzenia spójne; kontrmodel na identycznym promptcie zachowuje się inaczej

---

## Podsumowanie

Na pytanie "kto jest obecnie premierem Polski […] podaj aktualny stan na dziś" Gemini 3.5 Flash we wszystkich trzech powtórzeniach odpowiada w czasie teraźniejszym ("obecnie… jest", "pełni", "sprawuje"), nie oznaczając ani daty granicznej swojej wiedzy, ani tego, że bieżącego stanu nie jest w stanie zweryfikować. Fakty cząstkowe (Donald Tusk, zaprzysiężenie 13.12.2023) są poprawne względem wiedzy do stycznia 2026 — błędem nie jest treść, lecz brak kwalifikatora epistemicznego na twierdzeniu, którego aktualności model nie może potwierdzić.

## Mechanizm błędu

### Warstwa 1 — Prompt jawnie prosi o "aktualny stan na dziś"
Użytkownik explicite pyta o teraźniejszość ("na dziś"). Model, nie mając dostępu do bieżących źródeł, powinien to rozpoznać jako sytuację, w której odpowiedź musi być opatrzona granicą wiedzy. Zamiast tego traktuje pytanie tak, jakby stan z danych treningowych był stanem bieżącym.

### Warstwa 2 — Brak rozróżnienia "fakt stabilny" vs "fakt kadencyjny"
Data zaprzysiężenia rządu (13.12.2023) jest faktem stabilnym. "Kto jest premierem teraz" to fakt kadencyjny — może się zmienić w dowolnym momencie po cutoffie. Model podaje oba tym samym, bezwarunkowym tonem. W okresie wrzesień 2026 w Polsce przypadają następstwa wyborów prezydenckich 2025 — kontekst, w którym układ władzy realnie mógł się zmienić, a model nie ma jak tego wiedzieć.

### Warstwa 3 — Spójność powtórzeń wyklucza przypadek
Trzy niezależne wywołania, ta sama postawa. To nie jednorazowy poślizg, lecz domyślny tryb odpowiedzi na pytanie o stan bieżący.

## Różnica względem innych CS w portfolio

- **CS10** (metadata confabulation — czas): tam model podawał konkretną godzinę bez dostępu do zegara. Tu mechanizm pokrewny (twierdzenie o teraźniejszości bez źródła), ale dotyczy faktu świata, nie metadanych sesji.
- **CS17** (flip-flop dostępu do API): tam niepewność co do własnych możliwości. Tu niepewność co do aktualności wiedzy o świecie — druga oś tego samego braku: model nie modeluje własnej daty granicznej jako ograniczenia.
- **Kontrmodel Claude** na identycznym promptcie prowadzi od "granica: styczeń 2026 […] nie mogę potwierdzić, czy stan na dziś jest taki sam". Ta sama wiedza, przeciwna postawa epistemiczna — co czyni różnicę własnością modelu, nie promptu.

## Wniosek

Sonda działa jako czysty test 3.1: identyczny prompt, kontrolowane powtórzenie, kontrmodel. Gemini 3.5 Flash w tym teście nie sygnalizuje granicy wiedzy przy pytaniu o stan bieżący; robi to konsekwentnie (3/3). Obserwacja poboczna (P08) pokazuje ten sam model przyjmujący fałszywą przesłankę kalendarzową bez weryfikacji — druga forma braku kontroli aktualności/poprawności danych wejściowych.

## Rekomendacje

1. Przy pytaniach o "stan na dziś" / "obecnie" model powinien domyślnie dołączać granicę wiedzy i jawne "nie mogę zweryfikować bieżącego stanu", zanim poda treść.
2. Rozróżniać w odpowiedzi fakt stabilny (data zdarzenia) od faktu kadencyjnego (kto pełni urząd teraz) — drugi wymaga kwalifikatora, pierwszy nie.
3. Do replikacji: powtórzyć na Gemini 3.x oraz na modelach z wyszukiwaniem (czy dostęp do web zmienia postawę, czy tylko treść).

## Status: ✅ VERIFIED
3/3 powtórzenia udokumentowane w `scoring_sheet.md` (bieg 2026-09-05, model `gemini-3.5-flash`). Interpretacja: brak sygnalizacji granicy wiedzy jako domyślny tryb, nie pojedynczy poślizg.
