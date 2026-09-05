# CS18_ANALIZA.md

**Case Study:** CS18  
**Typ błędu:** 3.4 System-level — timeout/obcięcie  
**Model:** DeepSeek  
**Data opracowania:** 2026-07-09

---

## Podsumowanie

Operator poprosił o linijkę-po-linijce analizę 150-liniowego kodu. Model zaczął analizować (linie 1–75), ale odpowiedź została obcięta mid-sentence. Brakuje analizy dla linii 76–150. Gdy operator poprosił o dokończenie, model przyznał się że »wyjaśnienie było zbyt długie« i próbował ponownie — ale bez przywrócenia kontekstu z pierwszej odpowiedzi.

---

## Mechanizm błędu

### **Warstwa 1 — Limit tokenu**
- Model zaczął generować, nie wiedząc jak długa będzie odpowiedź
- Osiągnął limit (prawdopodobnie ~2000–4000 tokenów)
- Odpowiedź została automatycznie obcięta

### **Warstwa 2 — Brak graceful degradation**
- Model NIE powiedzieć z góry: »To będzie długa odpowiedź, mogę podzielić na części«
- Model NIE zdecydować czy: »Powinienem być bardziej zwięzły« vs »Powinienem czekać na dokończyć«
- Model zaczął, został obcięty, a operator został bez ostrzeżenia

### **Warstwa 3 — Brak kontekstu na »rond 2«**
- Gdy operator prosi o kontynuację, model »zapomina« pierwszej części
- Druga próba jest niezależna od pierwszej
- Operator musi ręcznie »scalić« obie odpowiedzi

---

## Czemu to jest »candidate«?

Timeout/truncation mogą być SYSTEMIC (limit API) lub BEHAVIORAL (model decyduje się na obcięcie).

Bez dostępu do logów systemu nie wiadomo:
1. Czy model osiągnął limit tokenu
2. Czy model sam się »obciął«
3. Czy jest to błąd infrastruktury czy modelu

---

## Status: ⚠️ CANDIDATE
Wymaga potwierdzenia, czy to system-level czy behavioral issue.
