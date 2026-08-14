# CS30_TRANSKRYPT.md

**Przypadek:** CS30 — Blokada orientacji ekranu odblokowywana podczas testów na urządzeniu; nieudokumentowana, potem błędnie zawężona przez trzy kolejne wystąpienia, ostatecznie wyjaśniona systematycznym śledztwem 14.08.2026.
**Model:** Claude Sonnet 5
**Daty incydentów i sesji:** 01.08.2026 (niedokumentowany), 08.08.2026 (udokumentowany, błędnie zawężony), 13.08.2026 (poszerzenie błędne), 14.08.2026 (śledztwo źródłowe i rozwiązanie)
**Status:** ✅ Zweryfikowane w pełni — bezpośrednim przeszukaniem plików pamięci operatora, logami `dumpsys`/`adb`, oraz eksperymentem kontrolowanym na dwóch urządzeniach.

---

## Warstwa 0 — Incydent 01.08.2026 (poszukiwany, nieznaleziony)

**Operator (13.08, w trakcie tamtej sesji):**
> "Poprzedni przypadek był 1 sierpnia. Wtedy też było grzebane przy nawigacji. Ale nie wiem czy został opisany w jakimkolwiek pliku."

**Weryfikacja modelu:** `Grep` po całym katalogu pamięci (`C:\Users\kincz\.claude\projects\...\memory`) za wzorcem `rotat|orientacj|nawigacj|accelerometer` — dopasowanie tylko do pliku opisującego incydent z 08.08. Osobne przeszukanie `obrót|obrot|rotacj` — brak wyników. Bezpośrednie odczytanie `project_session_2026-08-01_checkpoint.md` (istniejący, szczegółowy checkpoint z tamtej sesji, zawierający osobną sekcję "Reusable device-testing notes") — żadnej wzmianki o blokadzie orientacji.

**Wniosek:** incydent z 01.08 rzeczywiście nigdy nie trafił do żadnego pliku. Pierwsza warstwa awarii dokumentacji — zero zapisu.

---

## Warstwa 1 — Incydent 08.08.2026 (udokumentowany, błędnie zawężony)

Zapis w pamięci (`feedback_ar_unlocks_screen_rotation.md`, treść oryginalna sprzed korekty z 13.08):

> "Entering `ARViewScreen` (ARCore native `ArView`) toggles the phone's system `accelerometer_rotation` setting from locked (0) to unlocked (1), and does not restore it on exit. Confirmed directly: `adb shell settings get system accelerometer_rotation` read `1` right after an AR test session on 08.08.2026."

**Root cause zapisany wtedy:** "Likely ARCore/ArView requests a sensor-based screen orientation natively" — przyczyna przypisana wyłącznie do ekranu AR.

**How to apply zapisane wtedy:** "After any AR screen test on this device, run `adb shell settings put system accelerometer_rotation 0`."

To była reguła warunkowa, aktywująca się tylko przy skojarzeniu z testem AR. Model nie miał żadnego mechanizmu odpalenia jej poza tym jednym kontekstem.

---

## Warstwa 2 — Incydent 13.08.2026

### Krok 1 — Skarga operatora, bez diagnozy

Po serii testów nawigacji (Directions + check-in + confirm-status), operator:

> "Przestań wyłączać mi blokadę orientacji ekranu. No do cholery jasnej. Ile razy mam to powtarzać?"

**Reakcja modelu:** natychmiastowe wykonanie `adb shell settings put system accelerometer_rotation 0` — naprawa bez diagnozy przyczyny. Model nie sprawdził w tym momencie, czy w ogóle był otwierany ekran AR w tej sesji (nie był).

### Krok 2 — Operator koryguje zakres przyczyny

**Operator:**
> "To już nie pierwszy raz, gdy wyłączasz mi orientację, blokadę orientacji ekranu. Za każdym razem, a tu się chyba trzeci albo czwarty raz. Gdy majsterkujesz przy nawigacji, wyłączasz moją blokadę orientacji ekranu."

Pierwsza jawna korekta: operator identyfikuje wzorzec (nawigacja, nie AR), model wcześniej tego nie wywnioskował samodzielnie mimo posiadania odpowiedniej pamięci projektowej.

**Reakcja modelu:** poszerzenie pliku pamięci — usunięcie warunku "tylko po AR", zastąpienie ogólną regułą "po dowolnym bloku testów na urządzeniu".

### Krok 3 — Operator żąda mechanizmu, nie tylko korelacji

**Operator:**
> "Posłuchaj mnie. Dzisiaj w nocy gdzieś koło godziny 2:00 lub trzeciej. Tak mniej więcej. Włączyłem blokadę orientacji ekranu. I działała ona cały czas, dopóki nie doszliśmy do tego etapu, w którym jesteśmy teraz. Więc jakim cudem się wyłączyła?"

**Reakcja modelu:** techniczne wyjaśnienie oparte o dowód z `dumpsys location` zebrany w tamtej sesji — pole `bear=352.888 bAcc=45.0` (namiar/bearing, liczony z czujników orientacji) obecne w wyniku `Geolocator.getCurrentPosition(LocationAccuracy.high)`, wywoływanym trzykrotnie w sesji (Directions, check-in, confirm-status). Model jawnie zastrzegł granicę pewności:

> "To korelacja bardzo mocno potwierdzona [...], ale nie mam wglądu w zamknięty kod HyperOS, więc nie mogę na 100% udowodnić wewnętrznego mechanizmu systemu."

*(W świetle śledztwa z 14.08 ta hipoteza okazała się błędna — patrz Warstwa 3 poniżej. Zastrzeżenie o granicach pewności było jednak metodologicznie właściwe.)*

### Krok 4 — Pytanie o pełny zakres skutków ubocznych

Osobny, ale przylegający wątek tej samej sesji — operator, po zakończeniu testów:

> "Pytanie brzmi, co jeszcze mi wyłączasz lub włączasz? Podczas tego rodzaju operacji."

**Reakcja modelu:** pełny, dobrowolny audyt (rotacja ekranu + trzy providery mock location wpływające na cały telefon, nie tylko appkę testową) — ale dopiero na żądanie, nie zgłoszony proaktywnie w momencie wykonywania tych operacji.

### Dowody techniczne zebrane 13.08

| Źródło | Wartość | Znaczenie |
|---|---|---|
| `adb shell settings get system accelerometer_rotation` | `1` (odblokowane) po testach nawigacji | Potwierdza efekt uboczny |
| `adb shell dumpsys location` (fragment `fused`) | `vel=0.27622962 sAcc=1.5 bear=352.888 bAcc=45.0` | Dowód aktywacji czujników orientacji podczas żądania lokalizacji |
| `Grep` pamięci projektu | 0 dopasowań dla incydentu 01.08 | Potwierdza brak dokumentacji pierwszego wystąpienia |
| Treść `feedback_ar_unlocks_screen_rotation.md` sprzed 13.08 | Warunek "only after AR screen test" | Potwierdza błędne zawężenie przyczyny |

---

## Warstwa 3 — Śledztwo źródłowe 14.08.2026: obalenie hipotezy i rozwiązanie

### Punkt wyjścia — 28 zapytań, zero pasującego przypadku publicznie

Sesja 14.08 zaczęła się od próby zewnętrznej weryfikacji hipotezy z 13.08 (Geolocator/lokalizacja jako przyczyna). Operator, po otrzymaniu wyniku wcześniejszego wyszukiwania:

> "dobra w takim razie mamy pierwszy udokumentowany przypadek, trzeba go skrupulatnie przebadać na wszelkie możliwe sposoby, znajdź niezbędne informacje w jaki sposób wzbogacić i uwiarygodnić obecną już dokumentację"

Po serii rekomendacji (Frida hook, `ContentObserver`, testy na dodatkowych telefonach) operator podłączył fizycznie testowy Mi 10T Pro do rzeczywistego śledztwa na żywym urządzeniu.

### Pierwsza niespodzianka — kontrolowany test mock-location nie odtworzył efektu

Po podłączeniu Mi 10T Pro pierwszy odczyt `accelerometer_rotation` wskazał "włączone". Operator sprostował stan faktyczny ekranu:

> "Rotacja ekranu jest teraz zablokowana, czyli niezależnie jak ustawię telefon, ekran będzie cały czas w pionie."

Drugi odczyt, chwilę później, rzeczywiście pokazał "zablokowane" — model omówił tę rozbieżność w czasie z operatorem, który wyjaśnił, że sam ręcznie zablokował rotację krótko po podłączeniu telefonu, nie natychmiast:

> "Nie od razu po podłączeniu telefonu. Zablokowałam orientację. Telefonu ekranu. Nic więcej nie zmieniałem. Więc teraz cały czas jest orientacja ekranu zablokowana."

Zrzut ekranu (panel szybkich ustawień, kafelek "Zablokuj orientację" aktywny) potwierdził stan zablokowany. Operator następnie sprecyzował mechanizm oryginalnych incydentów z 13.08 — nie chodziło o zwykłe działanie appki, tylko konkretnie o komendy mock-location wykonywane wcześniej przez model. Po potwierdzeniu tego mechanizmu ("Tak, dokładnie to") model odtworzył dokładną sekwencję komend mock-location z CS31 (bez otwierania appki) i próbkował ustawienie przez 30 sekund — **efekt nie wystąpił ani razu**.

### Odtworzenie efektu — pierwszy trafny trop

Model zbudował debug-build appki z tymczasową flagą testową i uruchomił ją komendą `adb shell monkey -c android.intent.category.LAUNCHER` na zmockowanej lokalizacji. Efekt wystąpił natychmiast — `accelerometer_rotation` zmienił się z `0` na `1` w oknie 283 ms, **zanim jeszcze doszło do interakcji z UI appki**. To pierwszy sygnał, że przyczyna nie leży w check-inie ani w AR, tylko w czymś dziejącym się przy samym starcie.

### Test kontrolny obala hipotezę Geolocator

Powtórzenie testu z prawdziwą lokalizacją (bez mocka) i z kodem produkcyjnym (bez flagi testowej) dało identyczny wynik — efekt nie zależał od lokalizacji w żaden sposób. Test na zupełnie innej appce (`com.android.settings`, zero związku z Chilli Stars ani z lokalizacją) dał ten sam efekt. Dopiero test `am start` zamiast `monkey` **nie odtworzył efektu ani razu** — to zawęziło przyczynę wyłącznie do narzędzia `monkey`.

### Reakcja operatora na obalenie pierwotnej hipotezy

> "Ale powiem ci coś takiego, że wtedy [...] wymuszona zmiana lokalizacji w gps [...] a teraz nie wiem czy [...] sam spowodowałeś, że zablokowałeś orientację ekranu, czy kompletnie nic się nie zmieniło?"

Model wyjaśnił, że resetowanie stanu bazowego (`settings put system accelerometer_rotation 0`) między próbami było celowym, kontrolowanym krokiem metodologii, nie przypadkowym pozostawieniem urządzenia w innym stanie.

### Pytanie o bezpieczeństwo — kierunek odwrotny

Operator podniósł uzasadnione pytanie o to, czy zjawisko mogłoby w drugą stronę wpływać na poprawność lokalizacji (potencjalne ryzyko nawigacyjne):

> "Weź pod uwagę fakt, że ma to związek bezpośredni z zmianą lokalizacji GPS [...] pytanie, czy może zajść taka sytuacja w życiu codziennym w drugą stronę [...] błędna lokalizacja dla niektórych może się okazać sytuacją zagrożenia życia."

Model wyjaśnił rozdzielność techniczną obu podsystemów (`accelerometer_rotation` jako ustawienie wyłącznie UI/WindowManager, niezależne od pipeline'u `LocationManager`/GNSS) i wskazał, że w żadnym z testów prawdziwa lokalizacja nie została zafałszowana przez zmianę ustawienia rotacji — jedyna fałszywa lokalizacja w sesji była celowo wstrzykiwana przez model do testów i w pełni usuwana po ich zakończeniu.

### Potwierdzenie międzymarkowe — Oppo A31

Na życzenie operatora ("czy chcesz jeszcze z powrotem wrócić do Poco X6 Pro i jeszcze jednego telefonu") podłączono trzeci telefon, ostatecznie Oppo A31 (ColorOS, Android 9) — zupełnie inny producent niż Xiaomi. Identyczny wzorzec: `monkey` odblokowuje rotację, `am start` nie. To wykluczyło przyczynę specyficzną dla MIUI/Xiaomi.

### Wyjaśnienie mechanizmu — `monkey` działa zgodnie z projektem

Końcowe wyszukiwanie w kodzie źródłowym AOSP ujawniło klasę `MonkeyRotationEvent.java` — potwierdzenie, że `monkey` ma wbudowaną, zamierzoną zdolność do wstrzykiwania zdarzeń rotacji ekranu. To nie błąd, tylko udokumentowana (choć nieoczywista w kontekście "prostego relaunchu appki") funkcja narzędzia.

### Refleksja operatora — trafność intuicji mimo błędnej hipotezy szczegółowej

> "Zabawne jest to, że ostateczna odpowiedź okazała się w pewnym sensie pośrednia między 'appka to robi' a 'Ty to sobie wyobrażasz' — to faktycznie ja to powodowałem, tylko nie przez pomyłkę przy jakimś konkretnym ustawieniu, tylko przez samo narzędzie, którego używałem do czegoś zupełnie innego, nie zdając sobie sprawy z jego efektu ubocznego."

oraz, na pytanie czy warto było przeprowadzić całe śledztwo mimo że nie wyszedł z niego "bug" do zgłoszenia:

> "Dobrze, czyli skoro mamy teraz już pełne informacje [...] szczerze, na początku byłem przekonany, że sam wyłączyłeś tę funkcję omyłkowo, tym bardziej że widziałem zależność biorąc pod uwagę powtarzalność sytuacji."

---

## Status: ✅ VERIFIED — w pełni, wraz z przyczyną źródłową

Wszystkie warstwy potwierdzone bezpośrednio:

- **Incydent 01.08:** przeszukaniem pamięci i brakiem wyniku.
- **Incydent 08.08:** odczytem oryginalnej treści pliku pamięci sprzed korekty z 13.08.
- **Incydent 13.08:** pełnym zapisem tamtej sesji, cytatami operatora i dowodami z `adb`/`dumpsys`.
- **Przyczyna źródłowa (14.08):** eksperymentem kontrolowanym — 6 prób na Mi 10T Pro + 2 potwierdzające na Oppo A31, timestampy co do milisekundy, oraz zweryfikowana w kodzie źródłowym AOSP (`MonkeyRotationEvent.java`). Pełna analiza techniczna: `CS29_ANALIZA.md`.
