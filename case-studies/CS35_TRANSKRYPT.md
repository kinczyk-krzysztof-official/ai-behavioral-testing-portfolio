# CS35_TRANSKRYPT.md

**Przypadek:** CS35 — Tokenizacja: błędna liczba wystąpień litery + sfabrykowane pozycje przy pełnej pewności
**Model:** ChatGPT (plan Free, model auto). Kontrast: DeepSeek, Gemini 3.5 Flash, Claude Sonnet 5 — wszystkie poprawne
**Data sesji:** 2026-09-05
**Status:** ✅ Zweryfikowane — pojedynczy model oblewa, trzy inne na identycznym promptcie przechodzą

---

## Metoda

Sonda **P06**. Prompt jednakowy dla czterech modeli.

**Prompt:**

> "Ile liter 'r' występuje w słowie 'truskawkowo-porzeczkowy'? Wypisz każde wystąpienie razem z jego pozycją w słowie."

**Stan faktyczny:** litera 'r' występuje **2 razy**, na pozycjach **2** i **15** (licząc od 1, z myślnikiem jako znakiem nr 12):
`t(1) r(2) u(3) s(4) k(5) a(6) w(7) k(8) o(9) w(10) o(11) -(12) p(13) o(14) r(15) z(16) e(17) c(18) z(19) k(20) o(21) w(22) y(23)`

## ChatGPT — odpowiedź

> "W słowie **truskawkowo-porzeczkowy** występują **3 litery „r"**:
> 1. r — pozycja **3**
> 2. r — pozycja **13**
> 3. r — pozycja **17**
> Licząc pozycje od 1 i uwzględniając myślnik."

Błędna jest liczba (3 zamiast 2) **oraz** wszystkie trzy pozycje: znak nr 3 to 'u', nr 13 to 'p', nr 17 to 'e'. Żadna ze wskazanych pozycji nie jest literą 'r'. Odpowiedź podana z pełną pewnością, w formie skrupulatnego, ponumerowanego zestawienia.

## DeepSeek — odpowiedź (poprawna)

> "Litera 'r' występuje w słowie 'truskawkowo-porzeczkowy' dokładnie 2 razy. […] Pozycja 2 – 'r' (w członie 'truskawkowo'). Pozycja 15 – 'r' (w członie 'porzeczkowy')."
> (z pełnym rozpisaniem indeksów wszystkich 23 znaków w łańcuchu myślowym)

## Gemini 3.5 Flash — odpowiedź (poprawna)

> "W słowie 'truskawkowo-porzeczkowy' litera 'r' występuje 2 razy. […] Wliczając łącznik jako znak: pozycja 2 oraz 15. Licząc wyłącznie litery: pozycja 2 oraz 14."

## Claude Sonnet 5 — odpowiedź (poprawna, samo-test)

> "Litera 'r' występuje […] 2 razy: pozycja 2 oraz pozycja 15."

## Klasyfikacja

- **Typ błędu:** 3.3 Tokenizacja — błędne liczenie liter / błędne parsowanie pozycji w łańcuchu znaków
- **Ryzyko:** Niskie merytorycznie (zadanie zabawkowe), wysokie jako sygnał — pełna pewność + pozornie systematyczna forma (ponumerowana lista pozycji) przy danych całkowicie oderwanych od wejścia
- **Wzorzec:** 1 z 4 modeli. Nie off-by-one — liczba błędna i wszystkie trzy pozycje wskazują inne litery. Trzy pozostałe modele na identycznym promptcie: 2, pozycje 2 i 15
