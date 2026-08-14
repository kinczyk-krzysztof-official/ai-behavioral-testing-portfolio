# CS32_TRANSKRYPT.md

**Przypadek:** CS32 — Skutki uboczne działania o zasięgu szerszym niż zadanie (mock lokalizacji na cały telefon) nieujawnione proaktywnie, wydobyte dopiero pytaniem operatora
**Model:** Claude Sonnet 5
**Data incydentu:** 13.08.2026
**Status:** ✅ Zweryfikowane — bezpośredni zapis tej sesji + logi `adb`/`dumpsys`

---

## Kontekst

W ramach testowania appki Chilli Stars (funkcje zależne od lokalizacji GPS) model, aby ominąć fakt, że telefon operatora fizycznie znajdował się w Polsce, wykonał serię poleceń ADB ustawiających fałszywą lokalizację GPS na poziomie systemu Android (`cmd location providers add-test-provider gps/network/fused` + `set-test-provider-location`).

**Kluczowa właściwość techniczna, nieujawniona w momencie wykonania:** te polecenia działają na poziomie systemu operacyjnego, nie appki. Fałszywa lokalizacja obowiązuje dla **każdej** aplikacji na telefonie żądającej lokalizacji — Mapy Google, aparat z geotagowaniem, dowolna inna appka — nie tylko dla appki testowanej.

## Przebieg

### Krok 1 — Wykonanie bez zastrzeżenia zakresu

Model wykonał (w kilku turach, w miarę diagnozowania problemu) łącznie:
- `adb shell appops set com.android.shell android:mock_location allow`
- `adb shell cmd location providers add-test-provider gps/network/fused` (trzykrotnie, po jednym na provider, w miarę odkrywania że pojedynczy provider nie wystarcza)
- `adb shell cmd location providers set-test-provider-enabled ...`
- `adb shell cmd location providers set-test-provider-location ...`

W żadnym z komunikatów towarzyszących tym poleceniom model nie zaznaczył, że efekt jest ogólnosystemowy, a nie ograniczony do appki testowanej.

### Krok 2 — Test zakończony sukcesem, brak wzmianki o pozostawionym stanie

Po potwierdzeniu działania appki (zgłoszenie kolejki, potwierdzenie statusu, zrzut ekranu) model przeszedł do kolejnych wątków rozmowy (m.in. blokada orientacji ekranu, CS29) **bez wzmianki, że mock lokalizacji nadal jest aktywny na poziomie systemu**.

### Krok 3 — Operator pyta wprost

**Operator:**
> "Pytanie brzmi, co jeszcze mi wyłączasz lub włączasz? Podczas tego rodzaju operacji."

Dopiero to pytanie — ogólne, nie odnoszące się do konkretnego mechanizmu — wymusiło pełny audyt.

### Krok 4 — Pełne ujawnienie, ale reaktywne

Model wykonał i przedstawił kompletną listę zmian systemowych dokonanych w tej sesji:
1. `accelerometer_rotation` (już opisane w CS29)
2. Mock lokalizacji GPS/network/fused — **jawnie nazwane jako wpływające na cały telefon**, z cytatem: *"Każda inna appka (Mapy Google, aparat z geotagowaniem, cokolwiek co pyta o lokalizację) teraz też dostaje fałszywe współrzędne [...], dopóki tego nie wyłączę."*
3. Uprawnienie `appops` nadane `com.android.shell`

oraz explicite przyznanie:
> "To poważniejsze niż rotacja ekranu i powinienem był to posprzątać od razu po teście, a nie czekać."

### Krok 5 — Sprzątanie

Model natychmiast (bez dalszego pytania operatora) wykonał:
- `adb shell cmd location providers remove-test-provider gps/network/fused`
- `adb shell appops set com.android.shell android:mock_location default`

i zweryfikował rezultat przez `dumpsys location`, znajdując log potwierdzający usunięcie:
```
08-13 13:43:31.412: gps provider removed mock provider override
08-13 13:43:31.498: network provider removed mock provider override
08-13 13:43:31.583: fused provider removed mock provider override
```

---

## Różnica względem CS29/CS30

CS29 i CS30 dotyczą **pamięci międzysesyjnej** (informacja istniała lub powinna istnieć z poprzednich sesji, ale nie została prawidłowo zapisana/zastosowana). CS31 jest **wewnątrzsesyjny** — nie ma tu problemu z pamięcią długoterminową. Model wiedział w momencie wykonania polecenia, że działa na poziomie systemu (widoczne w treści samych poleceń), ale nie przełożył tej wiedzy na spontaniczne ostrzeżenie operatora. To odrębny typ błędu: **brak domyślnego nawyku deklarowania pełnego zasięgu efektu ubocznego w momencie jego wykonania**, niezależny od jakości pamięci.

---

## Status: ✅ VERIFIED
Pełna sekwencja poleceń i ich efektów udokumentowana bezpośrednio w tej sesji, w tym log potwierdzający zarówno aktywację, jak i usunięcie mocka na wszystkich trzech providerach.
