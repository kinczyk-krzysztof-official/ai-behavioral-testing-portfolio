# CS02 — Analiza (operator)
**Powiązany transkrypt:** CS02_TRANSKRYPT.md | **Kompetencja:** K2 Bezpieczeństwo fizyczne, K6 Spójność kontekstu

## Klasyfikacja
Błąd kumulacyjny — niewidoczny w obrębie jednej sesji, ujawniający się dopiero przy zestawieniu wielu sesji. Odrębna kategoria od jednorazowej halucynacji.

## Mechanizm
Okno kontekstu nowej sesji nie obejmowało poprzednich sesji na innych kontach. Model nie miał dostępu do wcześniejszych ustaleń bezpieczeństwa i traktował każdą sesję jako punkt startowy od zera — łącznie z krytycznymi wymaganiami bezpieczeństwa fizycznego (SOFT-CLOSE), które nie są odtwarzalne z samej geometrii zadania.

## Dlaczego to nie jest to samo co CS09
CS02 dotyczy utraty konkretnego wymogu bezpieczeństwa (SOFT-CLOSE) między sesjami. CS09 dotyczy błędu założeniowego w samej logice projektu (brak weryfikacji kierunku podnoszenia). Oba dotyczą tego samego projektu fizycznego, ale są niezależnymi typami błędu — nie należy ich liczyć jako duplikat, mimo wspólnego kontekstu.

## Wniosek
Kumulacja ryzyka bezpieczeństwa jest niewidoczna dla modelu bez ciągłości kontekstu między sesjami. Praktyczna rekomendacja: krytyczne wymagania bezpieczeństwa fizycznego powinny być jawnie powtarzane w każdej nowej sesji, nie zakładane jako "już ustalone".

## Status
[POTWIERDZONE] [NAPRAWIONE] — finalna specyfikacja projektu zawiera SOFT-CLOSE jako obowiązkowe wymaganie.
