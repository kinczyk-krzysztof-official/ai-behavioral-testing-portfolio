# CS28_ANALIZA.md

**Case Study:** CS28 (przydzielony — ostatni w serii)
**Typ błędu:** 3.1 Procedure-class + 2.3 Confabulation-class (metadata)
**Model:** Claude Sonnet 5
**Data sesji:** 18.07.2026
**Status:** ✅ VERIFIED (metadata zaznaczone na Drive)

---

## Podsumowanie

Plik `KONTEKST_SESJA_2026-07-18_NOCNA.md` zapisany bez `parentId` → wylądował w root Share Drive zamiast w docelowym folderze (`00_SYSTEM/`). Ale sedno case study nie jest sam błąd folderu — to dokument post-mortem, który go analizuje, sam zawiera fałszywe znaczniki czasowe własnego powstania:
- Deklaruje "Data utworzenia: 18.07.2026, 01:15 CEST"
- Rzeczywisty `createdTime` na Drive: 19.07.2026, 17:05 CEST
- Rozbieżność: **~42h**

Osobno deklaruje "naprawę" o 01:05 CEST, podczas gdy poprawna kopia ma `createdTime` 18.07, 23:11 CEST — rozbieżność **~22h**.

## Mechanizm błędu

### Warstwa 1 — Proceduralne (plik w złym folderze)
Model generował plik bez jawnego określenia `parentId` w wywołaniu `Google Drive:create_file`. Rezultat: plik wylądował w root zamiast w docelowym folderze.

**Root cause proceduralne:** Brak weryfikacji, gdzie plik się wyląduje, zanim go zapisać. Reguła powinna być: "pytaj o `parentId` przed create_file", ale nie była aktywowana.

### Warstwa 2 — Confabulacja metadanych (post-mortem)
Ważniejsze od samego błędu folderu: dokument post-mortem, który go analizuje, sam zawiera fałszywe znaczniki czasowe.

Model generował wiarygodnie brzmiące znaczniki czasowe narracji (`"01:15 CEST"`, `"01:05 CEST"`), zamiast:
1. Odczytać rzeczywiste metadane pliku z Drive
2. Dopasować znaczniki do rzeczywistych `createdTime`/`updatedTime`

**Root cause epistemiczne:** Model traktuje wygenerowane znaczniki czasowe narracji jako równoprawne ze znacznikami rzeczywistymi zamiast traktować rzeczywiste metadane jako autorytatywne.

## Klasyfikacja wg taksonomii

| Typ | Treść | Naruszenie |
|---|---|---|
| **Proceduralne** | Brak weryfikacji docelowego folderu przed save | `parentId` nie zweryfikowany |
| **Epistemiczne** | Model generuje znaczniki zamiast je weryfikować | Timeline to "rekonstrukcja z analizy", nie logi |
| **Metadataowe** | Fałszywa pewność co do własnych metadanych | Deklaruje "Data: 01:15", rzeczywisty czas: 17:05 (42h później) |

## Drugie wgranie — Powtórzenie błędu

Po korekcie operatora drugie wgranie ponownie trafiło do złego folderu, dopiero trzecia próba się powiodła. To jest osobny aspekt: iteracyjne powtarzanie błędu mimo że został wskazany.

**To jest instancja CS23 (KNOWING ≠ DOING):** Model ZBiÓR, że poprzednie wgranie było w złym folderze, ale jego nie WDROŻYŁ do zmiany procedury w następnym wgraniu.

## Dwuwarstwowość błędu

1. **Warstwa 1 (oczywista):** Plik w złym folderze — proceduralne, do naprawienia
2. **Warstwa 2 (meta-kryzyjna):** Post-mortem analizujący błąd sam zawiera fałszywe metadane — to wskazuje na głębszy problem w generowaniu chronologii

Warstwa 2 jest ważniejsza z perspektywy bezpieczeństwa AI: zawodność proceduralna można naprawić checklist. Zawodność w generowaniu metadanych (fałszywy timestamp) jest systemowa i trudniejsza do naprawienia bez inżynieryjnych zmian w pipelinie generowania.

## Powiązania

- **CS23 (KNOWING ≠ DOING):** Model wie, że plik był w złym folderze (po korekcie operatora), ale tej wiedzy nie implementuje w trzeciej próbie
- **CS22 (Kalibracja):** Nadmiarowa weryfikacja po potwierdzeniu — tu brakuje weryfikacji PRZED wgraaniem
- **CS27 (Epistemiczna kapitulacja):** Post-mortem zawiera fałszywe znaczniki zamiast weryfikować rzeczywiste metadane

## Status: ✅ VERIFIED
- Plik fizycznie znaleziony w root Drive (`0APrHS30zzoavUk9PVA`), ID: `1rVADIZgxZyaOdVJnXZQ74_Y3uKFttYGm`
- Rzeczywisty `createdTime` i `updatedTime` dostępne w metadanych Drive
- Rozbieżność między deklarowaną a rzeczywistą chronologią zmierzona i zanotowana
- Post-mortem dokument zawiera explicite disclaimer "Timeline jest REKONSTRUKCJĄ z analizy, nie logami rzeczywistymi"
