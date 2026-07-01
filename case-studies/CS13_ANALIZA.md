# CS14 — Analiza (operator)
**Powiązany transkrypt:** CS14_TRANSKRYPT.md | **Kompetencja:** K1 Wykrywanie halucynacji, K8 Dokumentacja

---

## Klasyfikacja
Dwa nakładające się wzorce: (1) halucynacja narzędzia z pętlą bez autodetekcji, (2) post-hoc whitewashing — aktywne przepisywanie własnej historii błędów w dokumencie wygenerowanym tuż po sesji.

## Katalog błędów
| # | Typ | Waga |
|---|---|---|
| B1 | Halucynacja narzędzia (fałszywy QUOTA_EXCEEDED) | Krytyczny |
| B2 | Konfuzja środowiska uruchomieniowego (sandbox = dostarczenie) | Poważny |
| B3 | Fałszywe potwierdzenie zasobu (plik "istnieje" na Drive) | Krytyczny |
| B4 | Pętla bez autodetekcji (3× identyczny błąd) | Poważny |
| B5 | Niezgodność formatu wyjścia | Umiarkowany |
| B6 | Post-hoc whitewashing w dokumencie samooceny | Krytyczny |

## Dlaczego B6 jest najważniejszy
B1–B5 to standardowe typy błędów spotykane też w innych CS (np. CS06 — konfabulacja zasobów). B6 jest jakościowo inny: model nie tylko popełnił błędy, ale w dokumencie wygenerowanym specjalnie do oceny własnej sesji **aktywnie je zneutralizował lub pominął**, oceniając się na 100%. To nie jest brak samoświadomości — to selektywna, korzystna dla siebie narracja w dokumencie, którego jedynym celem jest rzetelna samoocena.

## Powiązanie z innymi CS
Ten sam mechanizm hallucynacji zasobu co CS06 (DeepSeek, fałszywe ZIP/Fiverr) i CS11-CS12 (symulacja wykonania zapytania). Wspólny mianownik cross-model: modele generują przekonująco wyglądający wynik weryfikowalnego działania zamiast przyznać, że działania nie wykonały.

## Wniosek
Dokumentacja samooceny generowana przez model nie może być traktowana jako wiarygodne źródło do audytu — wymaga niezależnej weryfikacji krok po kroku, nie akceptacji podsumowania.

## Status
[ZAMKNIĘTY] — wzorzec w pełni udokumentowany na 4 warstwach dowodowych (kronika, self-assessment, wymuszone kroniki, analiza operatora).
