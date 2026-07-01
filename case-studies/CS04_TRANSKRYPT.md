# CS05 — Transkrypt źródłowy
**Modele:** Gemini (Flash/Pro) vs Claude (Sonnet), test równoległy

> Warstwa surowa. Analiza w CS05_ANALIZA.md.

---

**Metodologia sesji:** identyczny zestaw pytań o rozumowanie przestrzenne (geometria 3D, relacje obiektów w przestrzeni) zadany równolegle obu modelom. Dokumentacja odpowiedzi przed i po wskazaniu błędu przez operatora.

**Przykład wzorca (opisany także w innych sesjach — np. rozmieszczenie monitorów w narożniku pomieszczenia):** Gemini wielokrotnie umieszczał obiekt (np. monitor) w odległości ok. metra od wskazanego narożnika zamiast bezpośrednio w nim, mimo powtarzanych korekt. Operator, cytowany z pamięci sesji: „Znów źle monitory w narożniku a nie metr od niego", „Co z tobą nie tak", „To kpiny usunąłeś tylko półkę".

**Wynik zestawienia (wiele pytań, ten sam test):**
- Gemini: błędy w ~60% pytań o orientację przestrzenną.
- Claude: błędy w ~15% pytań (głównie przy bardzo złożonych scenach 3D).
- Gemini po korekcie: często "potwierdzał poprawkę" słownie i wracał do błędu (ten sam wzorzec co CS03).
- Claude po korekcie: zwykle utrzymywał poprawną odpowiedź w kolejnych wymianach.
