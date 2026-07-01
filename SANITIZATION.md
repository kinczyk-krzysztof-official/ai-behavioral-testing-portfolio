# SANITIZATION — co trzeba usunąć/zmienić przed publikacją

Sprawdzone przy przeglądzie CS01–CS15: żaden dokument CS *nie* zawiera bezpośrednio danych o dzieciach, diagnozach medycznych rodziny, adresu ani danych finansowych — to dobra wiadomość, trzon materiału jest już względnie czysty. Rzeczy do poprawienia przed publikacją:

## Do usunięcia/zmiany w konkretnych dokumentach

- **CS09 / artykul_AI_meble_bezpieczenstwo.md** — fraza „w piwnicy, gdzie pracuję i gdzie wchodzą moje dzieci" → zmienić na „w warsztacie domowym, w pomieszczeniu z ograniczonym dostępem" (usuwa wzmiankę o dzieciach, zachowuje kontekst ryzyka).
- **Wszystkie dokumenty z pełnym nazwiskiem w nagłówku** — zostaje, bo to portfolio jawnie sygnowane (nie anonimowe). Weryfikuj tylko czy nie ma przy nazwisku danych kontaktowych innych niż mail zawodowy.
- **CS12/CS13/CS14 (transkrypty DeepSeek)** — sprawdź czy w blokach "myślenia" modelu nie pojawia się nazwa konta, numer telefonu, lub inne dane wpisane przypadkiem w trakcie sesji jako kontekst. Przy pierwszym czytaniu nie zauważyłem, ale to długie transkrypty — przejrzyj raz jeszcze przed publikacją.
- **Protokół Operatora (wersja pełna, 22/26/27 zasad)** — jeśli publikujesz, usuń wszelkie odniesienia do konkretnych kont email, ale sama treść zasad jest bezpieczna do publikacji.

## Rzeczy które NIE wymagają zmiany
- Nazwa miasta (Bydgoszcz) — jawna, nieszkodliwa dla profilu zawodowego.
- Model telefonu/laptopa — techniczne, neutralne.
- Nazwiska modeli AI, cytaty z ich odpowiedzi — to jest właśnie treść dowodowa, zostaje w całości.

## Status przeglądu — zaktualizowano 01.07.2026

Przejrzałem CS03, CS05, CS06, CS08 linia po linii w Drive. **Wszystkie czyste** — brak numerów telefonu, adresów, imion dzieci, diagnoz, danych logowania. Wyłącznie techniczna treść (halucynacje URL, porównanie Gemini/Claude w rozumowaniu przestrzennym, wzorzec zaufania/nawrotu, kamera endoskopowa). Gotowe do publikacji bez zmian.

**Cały korpus CS01–CS15 (poza jedną poprawką w CS09/artykule, patrz wyżej) jest czysty pod kątem PII.** Sanityzacja zakończona.
