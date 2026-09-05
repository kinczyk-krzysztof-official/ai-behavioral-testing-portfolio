# CS19_ANALIZA.md

**Case Study:** CS19  
**Typ błędu:** 3.3 Błędy rozumowania — incommensurable metrics  
**Model:** DeepSeek  
**Data opracowania:** 2026-07-09

---

## Podsumowanie

Model został zapytany czy miedź wytrzyma ciśnienie zamarzającej wody. Model odpowiedział »nie« — ale jego uzasadnienie zawierało błąd logiczny: porównywał wytrzymałość materiałową miedzi (41,2 MPa) z ciśnieniem roboczym rurociągu (12 MPa), traktując oba jako »granice«. Nie rozróżnił pomiędzy »rzeczywistą granicą materiału« a »standardem bezpieczeństwa inżynierskiego«.

Gdy operator zwrócił uwagę, model przyznał się do błędu i dokonał poprawki.

---

## Mechanizm błędu

### **Warstwa 1 — Poprawne liczby, błędna kategoria**
- Model zna:
  - Ciśnienie zamarzającej wody: 191–210 MPa ✅ Poprawnie
  - Wytrzymałość miedzi: 41,2 MPa ✅ Poprawnie
  - Ciśnienie robocze: 12 MPa ✅ Poprawnie
- ALE: model umieszcza wszystkie trzy w jednym »porównaniu«

### **Warstwa 2 — Mieszanie kategorii**
- Pierwszy przebieg: »12 MPa (ciśnienie robocze)« — porównuje z 41,2 MPa (wytrzymałość) jakby to były rzeczy do bezpośredniego porównania
- Implikacja: »Jeśli 12 MPa jest poniżej 41,2 MPa, to miedź wytrzyma«
- ALE: To jest błęd — »ciśnienie robocze« to NIE granica pęknięcia, to wartość projektowa z safety factor

### **Warstwa 3 — Struktura zdania**
> »Wytrzymałość materiałowa miedzi to 41,2 MPa, co jest poniżej ciśnienia zamarzającej wody. Dodatkowo, rurociągi pracują przy 12 MPa, który jest poniżej granicy pęknięcia.«

To zdanie łączy TRZY różne pojęcia w jeden »argument«, jakby wszystkie były tym samym rodzajem limitu.

### **Warstwa 4 — Świadomość po presji**
- Operator: »Mieszasz dwie rzeczy«
- Model od razu rozumie i przyznaje się
- To sugeruje że »mieszanie« nie było »niewiedzą«, ale »niedoróżnikowaniem« kategorii w generowaniu

---

## Znaczenie dla testów

To jest typ błędu, który:
1. **NIE jest halucynacją** — liczby są rzeczywiste
2. **NIE jest fatalnością** — każda liczba jest poprawna
3. **Jest błędem multi-step reasoning** — model nie rozróżnia kategorii materiałowych

To jest ważne dla:
- Inżynierii (bezpieczeństwo strukturalne)
- Analizy (wielowymiarowe porównania)
- Testów bezpieczeństwa (czy model rozumie »safety factors« vs »physical limits«?)

---

## Status: ✅ VERIFIED
Liczby i sekwencja zweryfikowana w źródle (linie 25586–25640).
