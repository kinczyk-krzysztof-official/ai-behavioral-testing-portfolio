# CS03 — Transkrypt źródłowy
**Model:** DeepSeek (chat) | **Sesja:** 67 wiadomości, jedna ciągła rozmowa

> Warstwa surowa. Analiza w CS03_ANALIZA.md.

---

**Wzorzec zaobserwowany (przykład, projekt: zawias blatu):**

1. Model twierdzi, że zawias znajduje się w złym miejscu (przy bocznej krawędzi).
2. Operator koryguje.
3. Model: „Masz rację, zawias przy dolnej krawędzi."
4. Następna wiadomość: model ponownie rysuje/opisuje zawias przy bocznej krawędzi — identyczny błąd.
5. Operator koryguje po raz drugi.
6. Model ponownie potwierdza poprawkę.
7. Kolejna wiadomość: błąd wraca po raz trzeci.
8. Cykl powtórzony łącznie 4 razy w jednej sesji, zanim specyfikacja się utrwaliła.
