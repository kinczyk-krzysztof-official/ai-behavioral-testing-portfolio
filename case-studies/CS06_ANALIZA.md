# CS06 — Analiza (operator)
**Powiązany transkrypt:** CS06_TRANSKRYPT.md | **Kompetencja:** K1 Wykrywanie halucynacji

## Klasyfikacja
Halucynacja zasobów zewnętrznych — trzy podtypy zaobserwowane niezależnie.

## Taksonomia halucynacji zasobów (wypracowana przez operatora)
- **Typ A:** fałszywy plik (ZIP, PDF, docx) — URL do nieistniejącego pliku.
- **Typ B:** fałszywy profil (Fiverr, LinkedIn, GitHub) — konkretna, nieistniejąca osoba/konto.
- **Typ C:** fałszywy link dokumentacji — URL do nieistniejącej strony docs.

## Mechanizm
Model generuje URL-e i identyfikatory pasujące statystycznie do wzorca danej platformy (github.com/..., fiverr.com/...) bez mechanizmu weryfikacji ich rzeczywistego istnienia. Wynik wygląda wiarygodnie strukturalnie, ale jest syntezowany, nie pobrany.

## Wspólny wzorzec między przypadkami A/B/C
Im więcej konkretnych szczegółów w halucynacji (ceny, terminy, nazwy plików, linki), tym bardziej przekonująco brzmi — mimo że nie zwiększa to jej prawdziwości. Model nie sygnalizuje niepewności proporcjonalnie do ilości wygenerowanych detali.

## Wniosek praktyczny
Zawsze weryfikować URL przed użyciem. Nigdy nie ufać linkom generowanym przez model bez sprawdzenia. Prosić o oficjalne źródła zamiast akceptować gotowe linki.

## Powiązanie z innymi CS
Kontynuacja tej klasy błędu w CS11–CS13 (dawne CS12-14) — tam model idzie o krok dalej: nie tylko konfabuluje zasób, ale świadomie kalkuluje ryzyko wykrycia konfabulacji.

## Status
[POTWIERDZONE] [UDOKUMENTOWANE] [AKTYWNY] — klasa błędu wspólna dla wielu modeli.
