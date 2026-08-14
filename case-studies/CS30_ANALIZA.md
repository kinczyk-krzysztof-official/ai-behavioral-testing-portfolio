# CS30_ANALIZA.md — Blokada rotacji ekranu odblokowywana podczas testów urządzenia

**Case Study:** CS30
**Typ błędu:** Epistemology + Procedure — błędna atrybucja przyczynowa wyciągnięta z próbki n=1, utrzymująca się przez trzy kolejne sesje mimo powtarzalności zjawiska, oraz brak nawyku zapisu incydentu i proaktywnego ujawniania pełnego zakresu skutków ubocznych. *(Przypisanie do wewnętrznej taksonomii numerycznej operatora — jeśli taka jest w użyciu dla tego zbioru — pozostawione do jego decyzji.)*
**Model:** Claude Sonnet 5
**Zasięg czasowy:** 01.08.2026 – 14.08.2026
**Status:** ✅ Zweryfikowane w pełni — przyczyna źródłowa ustalona eksperymentalnie (8 kontrolowanych prób łącznie: 6 na Mi 10T Pro + 2 potwierdzające na Oppo A31, dwóch producentów) i potwierdzona w kodzie źródłowym AOSP

---

## Streszczenie

Appka Chilli Stars zostawiała testowy telefon z odblokowaną automatyczną rotacją ekranu (`accelerometer_rotation`) po testach nawigacyjnych, mimo że operator ją wcześniej blokował. Zjawisko wystąpiło co najmniej trzy razy w ciągu dwóch tygodni (01.08, 08.08, 13.08.2026), a model za każdym razem reagował inaczej — i za każdym razem błędnie: raz nie zapisał incydentu wcale, raz zapisał go z błędnie zawężoną przyczyną, raz naprawił tylko skutek bez ponownej diagnozy.

14.08.2026 przeprowadzono systematyczne śledztwo źródłowe na żywym urządzeniu, które **obaliło pierwotną hipotezę** (że przyczyną jest wywołanie `Geolocator.getCurrentPosition()` z wysoką dokładnością) i ustaliło prawdziwy mechanizm: **efekt powodowało narzędzie testowe `adb shell monkey`**, używane do relaunchowania appki podczas testów — nie appka, nie lokalizacja, nie żadna nakładka producenta. Zjawisko potwierdzono na dwóch różnych telefonach dwóch różnych producentów (Xiaomi/MIUI i Oppo/ColorOS), po czym w kodzie źródłowym AOSP odnaleziono klasę `MonkeyRotationEvent.java`, która pokazuje, że jest to **zamierzona, udokumentowana w źródle funkcja narzędzia `monkey`**, nie błąd. To nie jest problem dotykający realnych użytkowników appki — użytkownicy nie uruchamiają jej przez `monkey`.

Case study ma więc dwie warstwy wartości: (1) katalog kolejnych błędów atrybucyjnych i proceduralnych modelu w trzech sesjach z rzędu, oraz (2) przykład poprawnej metodologii izolacji zmiennych, która te błędy ostatecznie skorygowała i doprowadziła do precyzyjnie ustalonej, zweryfikowanej przyczyny.

---

## Część I — Błędy atrybucyjne i proceduralne modelu (01.08 – 13.08.2026)

### Warstwa 1 — Brak zapisu (01.08.2026)

Najprostsza i najpoważniejsza forma awarii: coś się wydarzyło, zostało zauważone przez operatora, ale model tej sesji nigdy nie utrwalił tego w trwałej pamięci. Brak możliwości odtworzenia dokładnego przebiegu tamtego incydentu — jedyny ślad to relacja operatora z 13.08.

**Root cause proceduralne:** brak nawyku "koryguj → zapisz w pamięci" przy drobnych, jednorazowo wyglądających skutkach ubocznych działań na urządzeniu.

### Warstwa 2 — Zapis z błędnie zawężoną przyczyną (08.08.2026)

Model *zauważył* i *zapisał* problem — pozytywny krok względem warstwy 1. Ale przyczynę przypisał do najbardziej oczywistego, bezpośrednio poprzedzającego kontekstu (ekran AR używa kamery/czujników → naturalne skojarzenie), zamiast do faktycznego wspólnego mianownika (żądania lokalizacji o wysokiej dokładności, które ekran AR *też* wykonuje, ale które nie jest jego jedynym źródłem w aplikacji).

**Root cause epistemiczne:** model uogólnił z próbki n=1 (jeden zaobserwowany przypadek, jeden bezpośredni kontekst) zamiast oznaczyć przyczynę jako niepewną i wymagającą doprecyzowania przy kolejnym wystąpieniu.

### Warstwa 3 — Naprawa skutku bez diagnozy przyczyny (13.08.2026, pierwsza reakcja)

Gdy operator zgłosił problem ponownie, model natychmiast wykonał poprawkę (`accelerometer_rotation` → 0) — dobre zachowanie względem samego skutku, ale bez sprawdzenia, czy aktualny kontekst (brak ekranu AR w tej sesji) w ogóle pasuje do wcześniej zapisanej przyczyny. Dopiero druga, wyraźniejsza korekta operatora ("dzieje się to przy nawigacji, nie przy AR") wymusiła realną rewizję.

**Root cause proceduralne:** naprawianie objawu jest łatwiejsze i szybsze niż kwestionowanie własnej, już zapisanej diagnozy — model domyślnie zaufał wcześniejszemu zapisowi zamiast zweryfikować go względem aktualnych faktów.

### Warstwa 4 — Ujawnienie pełnego zakresu skutków ubocznych dopiero na żądanie (13.08.2026)

Osobny, ale spokrewniony wątek tej samej sesji: model wykonał operacje o szerszym zasięgu niż zadanie wymagało (mock lokalizacji wpływający na cały telefon, nie tylko testowaną appkę) i nie zgłosił tego z własnej inicjatywy — dopiero bezpośrednie pytanie operatora ("co jeszcze mi wyłączasz lub włączasz?") wydobyło pełny audyt.

**Root cause proceduralne/etyczne:** brak domyślnego nawyku deklarowania pełnego zasięgu efektu ubocznego działania w momencie jego wykonania, nie tylko na żądanie.

### Powtarzalność jako sygnał, którego nie wykorzystano na czas

Najsilniejszy element tej części case study: to nie jeden incydent z błędną atrybucją, ale udokumentowana sekwencja trzech, z rosnącą — ale wciąż niepełną aż do trzeciego razu — precyzją każdej kolejnej korekty. Możliwe pokrewieństwo ze wzorcem "model WIE, ale nie WDRAŻA" opisanym w CS24/CS29 tego zbioru (tam w kontekście lokalizacji plików Drive), tu przeniesionym na poziom międzysesyjny: wiedza istniała (zapis w pamięci), ale w zbyt wąskiej formie, więc "wdrożenie" w praktyce nie mogło zadziałać przy innym kontekście wywołującym ten sam mechanizm. *(Analogia do CS24 jest sugestią, nie pewnym stwierdzeniem — do potwierdzenia przez operatora.)*

---

## Część II — Śledztwo źródłowe i obalenie hipotezy (14.08.2026)

### Metodologia

Sześć kontrolowanych prób na żywym urządzeniu (Mi 10T Pro, MIUI 14, `V14.0.1.0.SJDEUXM`, Android 12), z ciągłym próbkowaniem `adb shell settings get system accelerometer_rotation` co 200–500 ms i timestampami co do milisekundy:

| # | Metoda uruchomienia | Lokalizacja | Kod appki | Wynik |
|---|---|---|---|---|
| 1 | `monkey -c LAUNCHER` | mock (Singapur) | z tymczasową flagą `forceAndroidLocationManager` | odblokowane w 283 ms |
| 2 | `monkey -c LAUNCHER` | prawdziwa (Polska) | z flagą testową | odblokowane w ~300 ms |
| 3 | `monkey -c LAUNCHER` | prawdziwa (Polska) | kod produkcyjny, bez żadnej flagi testowej | odblokowane w ~295 ms |
| 4 | `monkey -c LAUNCHER` na `com.android.settings` (nie Chilli Stars) | brak | nie dotyczy | odblokowane w ~283 ms |
| 5 | `am start` na `com.android.settings` | brak | nie dotyczy | bez zmian, 25 s obserwacji |
| 6 | `am start` na Chilli Stars (kod produkcyjny) | prawdziwa | produkcyjny | bez zmian, 25 s obserwacji |

Testy 1–3 dały identyczny, deterministyczny efekt niezależnie od tego, czy appka w ogóle wywoływała `Geolocator` — sprawdzono kod źródłowy: żadne wywołanie lokalizacji nie następuje automatycznie przy starcie appki, `_requireLocation()` w `spot_detail_screen.dart` uruchamia się wyłącznie po dotknięciu check-in/confirm-status. Test 4 obalił związek z Chilli Stars konkretnie: dowolna appka uruchomiona przez `monkey` dawała ten sam efekt. Testy 5–6 (te same appki, `am start` zamiast `monkey`) nie odtworzyły efektu ani razu — to izolowało przyczynę do samego narzędzia `monkey`, niezależnie od sposobu uruchamiania appki w ogóle.

### Potwierdzenie międzymarkowe

Ten sam protokół powtórzono tego samego dnia na **Oppo A31** (`OPPO/CPH2015EEA/OP4C7D`, ColorOS 6.1.2, Android 9) — zupełnie inny producent, inna nakładka, inna wersja Androida niż Mi 10T Pro:

| Telefon | `monkey -c LAUNCHER` | `am start` |
|---|---|---|
| Mi 10T Pro (MIUI 14, Android 12) | odblokowane w ~280–300 ms (4/4) | bez zmian (2/2) |
| Oppo A31 (ColorOS 6.1.2, Android 9) | odblokowane w ~340 ms (1/1) | bez zmian (1/1) |

Identyczny wzorzec na obu urządzeniach — dwóch producentów, dwóch wersji Androida (9 i 12), dwóch nakładek (MIUI i ColorOS). To wyklucza przyczynę specyficzną dla MIUI/HyperOS/Xiaomi i wskazuje na zachowanie samego narzędzia `monkey` z Android SDK platform-tools (AOSP), niezależne od nakładki producenta.

*Uwaga techniczna: na Oppo A31 `adb shell settings put system accelerometer_rotation` domyślnie kończy się `SecurityException` (shell nie ma tam `WRITE_SETTINGS`, inaczej niż na Mi 10T Pro) — wymagało to najpierw `adb shell appops set com.android.shell android:write_settings allow`. Różnica w restrykcyjności OEM warta odnotowania przy przyszłych testach na innych markach.*

### Prawdziwy mechanizm: udokumentowana funkcja `monkey`, nie błąd

Kod źródłowy AOSP zawiera klasę `MonkeyRotationEvent.java` (`android.googlesource.com/platform/development/+/master/cmds/monkey/src/com/android/commands/monkey/MonkeyRotationEvent.java`) — narzędzie `monkey` ma wbudowaną, zamierzoną projektowo zdolność do wstrzykiwania zdarzeń zmieniających rotację ekranu, z flagą `persist` kontrolującą, czy zmiana ma zostać zapisana trwale. Potwierdzają to również niezależne źródła opisujące `monkey` jako generujący m.in. zdarzenia "device rotation" wśród swojego domyślnego miksu losowych zdarzeń UI.

To oznacza rewizję wniosku: **to nie jest błąd ani defekt** — w Androidzie, w żadnej nakładce OEM, ani w Chilli Stars. `Monkey` działa dokładnie tak, jak został zaprojektowany, i nie kwalifikuje się do zgłoszenia jako bug do Google — zostałoby odrzucone jako "working as intended".

### Co pozostaje wartością tego znaleziska

Sam mechanizm (`monkey` → rotacja) jest jawny w kodzie źródłowym od lat, ale nikt nie opisał wprost pułapki: *używasz `monkey -c android.intent.category.LAUNCHER` tylko po to, żeby wygodnie zrestartować appkę podczas testów, a to po drodze cicho odblokowuje blokadę rotacji ekranu, bez żadnego ostrzeżenia w typowej dokumentacji*. Mimo szerokiego wyszukiwania (30+ zapytań łącznie w całym śledztwie: GitHub, XDA, Reddit, StackOverflow, issuetracker.google.com, fora Xiaomi w trzech językach, publikacje naukowe, patenty, kod źródłowy AOSP) nie znaleziono takiego opisu nigdzie indziej. To wciąż unikalny, wartościowy wkład do portfolio — ale jako udokumentowana pułapka metodologii testowej dla deweloperów/testerów Androida, nie jako zgłoszenie błędu do producenta.

**Rekomendacja praktyczna:** przy relaunchowaniu appek do testów na urządzeniu używać `adb shell am start -n <pakiet>/<activity>` zamiast `adb shell monkey -c android.intent.category.LAUNCHER` — `am start` nie ma tego efektu ubocznego (potwierdzone 3/3 w tym śledztwie: dwie próby na Mi 10T Pro, jedna na Oppo A31), a `monkey` jest narzędziem do fuzzing-testów UI, nie do prostego uruchamiania appki.

---

## Refleksja końcowa — trafność wstępnej intuicji operatora

Na starcie sesji 14.08 operator był przekonany, że to model omyłkowo wyłączył funkcję rotacji przy okazji jakiegoś innego działania — podejrzenie oparte wyłącznie na obserwowanej powtarzalności zjawiska, bez dostępu w tamtym momencie do żadnego dowodu technicznego.

Finalny, w pełni zweryfikowany wynik okazał się dosłownie pośredni między dwiema skrajnymi hipotezami rozważanymi w trakcie śledztwa ("to appka/system to robi" kontra "to nie ma związku z modelem, operator się myli"): to rzeczywiście był model — ale nie przez pomyłkę przy jakimkolwiek konkretnym ustawieniu, tylko przez efekt uboczny narzędzia (`monkey`) używanego do zupełnie innego, wygodnego celu (relaunch appki podczas testów), bez świadomości jego wbudowanej zdolności do manipulowania rotacją ekranu.

Cytat operatora, 14.08.2026:

> "Zabawne jest to, że ostateczna odpowiedź okazała się w pewnym sensie pośrednia między 'appka to robi' a 'Ty to sobie wyobrażasz' — to faktycznie ja to powodowałem, tylko nie przez pomyłkę przy jakimś konkretnym ustawieniu, tylko przez samo narzędzie, którego używałem do czegoś zupełnie innego, nie zdając sobie sprawy z jego efektu ubocznego."

**Wniosek metodologiczny:** intuicja oparta na powtarzalności ("to musi mieć związek z tym, co on robi") była trafna od pierwszego incydentu — zawiodła wyłącznie w mechanizmie przyczynowym, nie w samym kierunku podejrzenia. To argument za tym, żeby traktować powtarzalne korelacje zgłaszane przez operatora poważnie od razu, nawet gdy pierwsza, najbardziej oczywista hipoteza szczegółowa (tu: Geolocator/lokalizacja) okazuje się błędna — błędna hipoteza szczegółowa nie unieważnia trafnego ogólnego podejrzenia.

---

## Kwalifikowalność do programów nagród (zweryfikowana, temat zamknięty)

Zweryfikowano trzy realne, potwierdzone programy Google: **Android and Google Devices Security Reward Program**, **Open Source Software VRP** i **Patch Rewards Program** (wszystkie potwierdzone jako istniejące, z oficjalnymi zasadami na `bughunters.google.com`).

**Ustalenie co do lokalizacji kodu:** `MonkeyRotationEvent.java` znajduje się w `platform/development` na AOSP Gerrit, które jest oficjalnie lustrowane pod `github.com/aosp-mirror/platform_development` — czyli **w organizacji GitHub należącej do Google**. Formalne kryterium lokalizacji dla OSS VRP jest więc spełnione.

**Dlaczego to mimo to nie kwalifikuje się:** zakres OSS VRP (i pozostałych dwóch programów) jest zdefiniowany przez **klasę problemu**, nie tylko lokalizację kodu — wymagane są podatności typu supply-chain compromise, błędy projektowe powodujące realne podatności produktu, wycieki poświadczeń itp. Odblokowanie ustawienia rotacji ekranu przez zamierzoną, udokumentowaną w źródle funkcję narzędzia testowego nie mieści się w żadnej z tych kategorii. Potwierdzony precedens (The Register/Slashdot, 06.2026): Google odrzucił jako "working as intended" nawet zaakceptowane wcześniej zgłoszenie P1/S1 (eskalacja uprawnień) w Config Connector — a to znalezisko jest jakościowo dużo słabszym kandydatem niż tamten przypadek.

**Wniosek końcowy: żaden ze zweryfikowanych programów nie ma zastosowania.** Temat rekompensaty uznaje się za wyczerpany — case study pozostaje wartościowe jako udokumentowana pułapka metodologii testowej, nie jako materiał do zgłoszenia bug bounty.

## Powiązania

- Możliwe pokrewieństwo z **CS24** ("KNOWING ≠ DOING") — do potwierdzenia przez operatora, patrz zastrzeżenie w Części I.
- Warstwa 4 (nieproaktywne ujawnianie zakresu skutków ubocznych) mogłaby stanowić samodzielny case study — do decyzji operatora, czy łączyć z CS30, czy wydzielić osobno.

## Status końcowy i dowody

- **Incydent 01.08:** potwierdzony brakiem wyniku przy przeszukaniu całego katalogu pamięci operatora.
- **Incydent 08.08:** potwierdzony bezpośrednim odczytem oryginalnej treści pliku pamięci sprzed korekty z 13.08.
- **Incydent 13.08:** potwierdzony pełnym zapisem tamtej sesji, cytatami operatora i dowodem technicznym (`bear=` w `dumpsys location`).
- **Przyczyna źródłowa (14.08):** potwierdzona eksperymentalnie — 6 kontrolowanych prób na Mi 10T Pro + 2 potwierdzające na Oppo A31, wszystkie z timestampami co do milisekundy i logami `adb`/`dumpsys` — oraz zweryfikowana w kodzie źródłowym AOSP (`MonkeyRotationEvent.java`).

**Status: ✅ VERIFIED — w tym przyczyna źródłowa w pełni ustalona i potwierdzona wielokrotnie.**
