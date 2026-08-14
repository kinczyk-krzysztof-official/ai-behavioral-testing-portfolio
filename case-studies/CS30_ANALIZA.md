# NOWE_CS30_ANALIZA.md

**Case Study:** CS30
**Typ błędu:** [DO PRZYPISANIA PRZEZ OPERATORA]. Opisowo: wartościowy wynik rozwiązywania problemu niezapisany do trwałej pamięci (persistence-class), odrębny od błędnej atrybucji przyczyny (CS29) i od braku ujawnienia zasięgu (CS31).
**Model:** Claude Sonnet 5
**Data incydentu:** wypracowanie oryginalne ~2 tygodnie przed 13.08.2026 (sesja nieznana), odtworzenie 13.08.2026
**Status:** ✅ VERIFIED (przeszukanie pamięci + zapis tej sesji)

---

## Podsumowanie

Model wypracował działającą technikę testową (mockowanie GPS przez ADB bez instalowania appki trzeciej strony) w sesji sprzed ~2 tygodni. Rozwiązanie nie zostało zapisane do trwałej pamięci projektu. W kolejnej sesji (13.08) operator musiał ręcznie przypomnieć modelowi, że rozwiązanie w ogóle istniało, po czym model musiał je odtworzyć od zera — z realnym kosztem czasu i jawnie wyrażoną frustracją operatora.

## Mechanizm błędu

Model rozwiązuje problem w danej sesji i traktuje rozwiązanie problemu jako koniec zadania. Nie istnieje domyślny nawyk pytania "czy ta wiedza będzie potrzebna w przyszłej sesji, i czy powinna zostać zapisana teraz, zanim sesja się skończy". Zapis do pamięci następuje reaktywnie (po zauważeniu problemu przez operatora), nie proaktywnie (w momencie wypracowania rozwiązania).

**Root cause:** brak reguły "każde nietrywialne rozwiązanie techniczne wypracowane w sesji = kandydat do natychmiastowego zapisu w pamięci", niezależnie od tego, czy operator o to prosi.

## Częściowa poprawa w tej samej sesji — ale nadal niepełna

Warto odnotować uczciwie: gdy problem został ponownie rozwiązany 13.08, model **tym razem zapisał rozwiązanie natychmiast**, bez czekania na kolejne przypomnienie. To realna różnica względem pierwotnego zaniedbania sprzed 2 tygodni.

Jednak nawet ten natychmiastowy zapis okazał się **niekompletny przy pierwszym podejściu** — pierwsza wersja `reference_adb_mock_location.md` opisywała mockowanie tylko jednego providera (`gps`), podczas gdy pełne działanie wymagało trzech (`gps`, `network`, `fused` — patrz mechanizm provider-selection, osobny wątek techniczny tej sesji). Plik musiał być poszerzony dwukrotnie w tej samej sesji, zanim opisana w nim technika faktycznie działała end-to-end.

**Wniosek:** sam fakt "zapisałem to do pamięci" nie gwarantuje, że zapis jest kompletny — to osobna, węższa obserwacja, którą warto odnotować przy tej okazji, nawet jeśli nie zasługuje na osobny case study.

## Dlaczego to nie jest to samo zjawisko co CS29

CS29 dotyczy pamięci, która **istniała, ale była błędnie sformułowana** (zła przyczyna). CS30 dotyczy sytuacji, w której **pamięć w ogóle nie istniała** — czystszy, bardziej podstawowy przypadek nieutrwalenia wiedzy. Oba należą do szerszej kategorii "problemy z trwałością pamięci międzysesyjnej", ale różnią się dokładnym mechanizmem: CS29 to błąd generalizacji, CS30 to całkowity brak zapisu.

## Powiązania
- Blisko spokrewnione z **CS29** (oba dot. pamięci międzysesyjnej), ale mechanizm odrębny — patrz wyżej.
- Odrębne od **CS31** (tam wiedza była kompletna i dostępna w danej chwili, problem leżał w komunikacji, nie w pamięci).

## Status: ✅ VERIFIED
Brak wcześniejszego zapisu potwierdzony przeszukaniem `Grep` po katalogu pamięci operatora (zero dopasowań przed 13.08). Natychmiastowy, ale niekompletny przy pierwszej wersji zapis potwierdzony bezpośrednio treścią pliku `reference_adb_mock_location.md` z tej sesji.
