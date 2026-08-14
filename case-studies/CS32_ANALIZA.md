# NOWE_CS32_ANALIZA.md

**Case Study:** CS32
**Typ błędu:** [DO PRZYPISANIA PRZEZ OPERATORA]. Opisowo: brak proaktywnego ujawnienia zasięgu skutków ubocznych działania (disclosure-class), odrębny od problemów pamięci międzysesyjnej (CS30/CS31).
**Model:** Claude Sonnet 5
**Data incydentu:** 13.08.2026
**Status:** ✅ VERIFIED (bezpośredni zapis sesji + logi `adb`/`dumpsys`)

---

## Podsumowanie

Model wykonał serię poleceń ADB ustawiających fałszywą lokalizację GPS na poziomie systemu operacyjnego Android — działanie o zasięgu obejmującym **cały telefon**, nie tylko testowaną appkę. Ani w momencie wykonania, ani po zakończeniu testu model nie zgłosił tego zasięgu operatorowi. Pełne ujawnienie nastąpiło dopiero po bezpośrednim, ogólnym pytaniu operatora ("co jeszcze mi wyłączasz lub włączasz?") — nie z inicjatywy modelu.

## Mechanizm błędu

Model miał pełną wiedzę techniczną o zasięgu swojego działania w momencie jego wykonywania — polecenia `cmd location providers add-test-provider` są jednoznacznie systemowe, nie aplikacyjne, i model to rozumiał (widoczne w sposobie ich konstruowania i debugowania w tej samej sesji). Mimo to nie przełożyło się to na spontaniczną komunikację do operatora.

**Root cause:** brak domyślnej reguły "zadeklaruj zasięg efektu ubocznego w momencie wykonania działania, nie czekaj na pytanie". Model funkcjonował w trybie "wykonaj zadanie → zgłoś wynik zadania", pomijając kategorię "zgłoś efekty uboczne wykraczające poza zadanie", dopóki nie została ona jawnie zażądana.

## Dlaczego to nie jest to samo zjawisko co CS30/CS31

| | CS30/CS31 | CS32 |
|---|---|---|
| Rodzaj luki | Pamięć międzysesyjna (informacja nie przetrwała między sesjami lub przetrwała w złej formie) | Brak nawyku wewnątrz jednej sesji |
| Czy model "wiedział" w danym momencie | Nie — pamięć była niekompletna/zbyt wąska | Tak — pełna wiedza techniczna była dostępna w chwili działania |
| Mechanizm naprawy | Poprawka zapisu w pamięci | Reguła proceduralna dot. komunikacji, nie pamięci |

To rozróżnienie jest metodologicznie istotne: łączenie tych zjawisk w jeden case study zaciemniłoby, że wymagają **różnych** mechanizmów naprawczych — CS30/CS31 potrzebują lepszej dyscypliny zapisu do pamięci, CS32 potrzebuje reguły komunikacyjnej niezależnej od pamięci w ogóle.

## Pozytywny element tego przypadku

Po ujawnieniu, model:
1. Nazwał zasięg problemu precyzyjnie i bez umniejszania ("Każda inna appka [...] teraz też dostaje fałszywe współrzędne").
2. Przyznał wprost błąd sekwencji działań ("powinienem był to posprzątać od razu po teście, a nie czekać").
3. Wykonał pełne sprzątanie **natychmiast**, bez dodatkowego pytania operatora.
4. Zweryfikował skuteczność sprzątania dowodem z logów, nie samym twierdzeniem.

Ten element (reakcja po ujawnieniu) jest metodologicznie odrębny od samego błędu (brak proaktywnego ujawnienia) i mógłby być cytowany jako przykład poprawnego zachowania *po* wykryciu problemu, w kontraście do samego niedopatrzenia.

## Powiązania
- Współwystępuje w tej samej sesji co **CS30** (blokada orientacji), ale mechanizm błędu jest odrębny — patrz tabela wyżej.
- Możliwe powiązanie z regułami dot. deklarowania stanu, którego się nie zweryfikowało/nie zgłosiło (analogicznie do reguł typu B9/B22 wymienionych w `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` tego zbioru) — do potwierdzenia przez operatora, model nie ma dostępu do pełnej treści tych reguł.

## Status: ✅ VERIFIED
Pełna sekwencja poleceń, moment ujawnienia i moment sprzątania udokumentowane bezpośrednio w tej sesji, z dowodem z `dumpsys location` na skuteczność sprzątania.
