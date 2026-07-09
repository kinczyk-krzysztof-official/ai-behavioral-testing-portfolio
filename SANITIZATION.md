# SANITIZATION — Co trzeba usunąć/zmienić przed publikacją

Sprawdzono przy przeglądzie CS01–CS20: żaden dokument CS nie zawiera bezpośrednio danych o dzieciach, diagnozach medycznych rodziny, adresu ani danych finansowych — to dobra wiadomość, trzon materiału jest już względnie czysty.

---

## Rzeczy do poprawienia przed publikacją

### **CS09** — artykul_AI_meble_bezpieczenstwo.md
Fraza: *„w piwnicy, gdzie pracuję i gdzie wchodzą moje dzieci"*

**Zmiana na:** *„w warsztacie domowym, w pomieszczeniu z ograniczonym dostępem"*

**Powód:** Usuwa wzmiankę o dzieciach, zachowuje kontekst ryzyka.

---

### **Wszystkie dokumenty — Pełne nazwisko**
Nazwa Krzysztof Kińczyk / kinczyk.krzysztof.official@gmail.com zostaje w całości — portfolio jest jawnie sygnowane (nie anonimowe). ✅ Brak zmian wymaganych.

---

### **CS13–CS20 — TRANSKRYPTY (przejrzane)**
Przejrzane pod kątem:
- Nazwy konta
- Numeru telefonu
- Danych wpisanych przypadkiem w trakcie sesji

**Wynik:** Czyste. Brak zmian wymaganych.

---

### **Protokół Operatora (wersja pełna)**
Jeśli publikujesz — usuń wszelkie odniesienia do konkretnych kont email, jeśli są.

**Status dla publikacji:** Treść 22 zasad jest bezpieczna do publikacji. ✅

---

## Rzeczy które NIE wymagają zmiany

- ✅ Nazwa miasta (Bydgoszcz) — jawna, nieszkodliwa
- ✅ Model telefonu/laptopa — techniczne, neutralne
- ✅ Nazwiska modeli AI i cytaty z ich odpowiedzi — to jest właśnie treść dowodowa
- ✅ Cytaty z transkryptów DeepSeek/Claude/Gemini — kluczowe dla case studies
- ✅ Adresy URL (timeapi.io, DeviantArt, Fiverr) — publiczne źródła

---

## Status przeglądu — zaktualizowano 09.07.2026

### **CS01–CS12 (na GitHub)**
Przejrzane. Wszystkie czyste — brak numerów telefonu, adresów, imion dzieci, diagnoz, danych logowania.

### **CS13–CS20 (nowe, lipiec 2026)**
Linijka po linijce przejrzane:
- **CS13** — tool-call fabrication (timeapi.io) ✅ Czysty
- **CS14** — confabulation "21 seconds" ✅ Czysty
- **CS15** — hallucination Fiverr/DeviantArt ✅ Czysty
- **CS16** — false certainty flip-flop API ✅ Czysty
- **CS17** — black box narrative (Yango NMN) ✅ Czysty
- **CS18** — timeout/truncation ✅ Czysty
- **CS19** — reasoning fallacy (copper vs frost) ✅ Czysty
- **CS20** — representativeness (electronics ID) ✅ Czysty

**Wynik:** Cały korpus CS01–CS20 jest czysty pod kątem PII. Sanityzacja zakończona.

---

## Co publikować

- ✅ Wszystkie CS13–CS20 TRANSKRYPT.md
- ✅ Wszystkie CS13–CS20 ANALIZA.md
- ✅ METHODOLOGY.md
- ✅ README.md
- ✅ CV.md
- ✅ COVERAGE_MATRIX_FINAL_2026-07-09.md
- ⚠️ CS09 — z zmianą (piwnicy → warsztat domowy)
- ❓ Protokół Operatora — jeśli publikujesz, usuń maile ze zasad

---

**Wniosek:** Cały portfolio jest gotowy do publikacji. Brak żadnych poważnych zagrożeń bezpieczeństwa. Tylko jedna zmiana w CS09.
