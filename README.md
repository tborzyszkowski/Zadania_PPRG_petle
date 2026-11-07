# Lab 01: Zmienne, wyrażenia warunkowe i praca z IDE w C#

| Parametr | Szczegóły |
| --- | --- |
| **Termin oddania** | 18.10.2026, godz. 23:00 |
| **Suma punktów** | 10 pkt |
| **Język / Platforma** | C# (.NET 8+) |
| **Wymagane środowisko** | Visual Studio 2022 / VS Code (z C# Dev Kit) / JetBrains Rider |

---

### Zasady terminowości

Przekroczenie terminu o $n$ zajęć (lub tygodni) wiąże się ze zmniejszeniem maksymalnej liczby punktów zdobytych za zadanie według wzoru:


$$\text{Punkty końcowe} = \frac{\text{Punkty uzyskane}}{2^n}$$

---

## Wymagania techniczne i środowiskowe

1. **Struktura projektu**: Zadania należy zrealizować w ramach jednego rozwiązania (Solucji / Solution) zawierającego 3 osobne projekty konsolowe lub jednego projektu z menu wyboru zadania.
2. **Standardy C#**:
* Stosuj właściwe konwencje nazewnictwa C# (`camelCase` dla zmiennych lokalnych, `PascalCase` dla metod/klas).
* Do konwersji i walidacji danych wejściowych z konsoli używaj bezpiecznych metod (np. `double.TryParse(...)` lub `int.TryParse(...)`), aby program nie ulegał awarii po wpisaniu tekstu zamiast liczby.


3. **Funkcjonalność IDE**: Wykorzystaj narzędzia wbudowane w wybrane środowisko (Visual Studio, VS Code, Rider):
* Przetestuj działanie programu za pomocą debugera (stawianie punktów przerwania – *Breakpoints*, podgląd wartości zmiennych *Watch/Locals*).



---

## Zadanie 1: Liczby ściśle rosnące [2 pkt]

Napisz program konsolowy, który prosi użytkownika o podanie kolejno **pięciu liczb**.

### Wymagania:

* Program pobiera liczby pojedynczo (po każdej wprowadzonej liczbie zatwierdzonej klawiszem Enter).
* Po wprowadzeniu każdej kolejnej liczby (począwszy od drugiej) program sprawdza, czy jest ona **ściśle większa** od poprzedniej.
* Jeśli warunek rosnący zostanie naruszony (liczba jest mniejsza lub równa poprzedniej), program natychmiast kończy działanie i wyświetla stosowny komunikat (np. `Błąd: Liczba {x} nie jest większa od {y}. Program zakończony.`).
* Jeżeli wszystkie 5 liczb zostanie wprowadzonych w ciągu ściśle rosnącym, program wyświetla komunikat o sukcesie.

---

## Zadanie 2: Równanie liniowe [3 pkt]

Napisz program rozwiązujący równanie liniowe w postaci ogólnej:


$$a \cdot x + b = 0$$

### Wymagania:

* Program prosi użytkownika o podanie wartości współczynników $a$ oraz $b$ (typu `double`).
* Program analizuje i obsługuje wszystkie przypadki matematyczne:
1. **Jedno rozwiązanie**: $a \neq 0 \implies x = -\frac{b}{a}$.
2. **Równanie tożsamościowe** (nieskończenie wiele rozwiązań): $a = 0 \text{ oraz } b = 0$.
3. **Równanie sprzeczne** (brak rozwiązań): $a = 0 \text{ oraz } b \neq 0$.


* Wynik powinien zostać sformatowany i wyświetlony w czytelny sposób w konsoli.

---

## Zadanie 3: Równanie kwadratowe [5 pkt]

Napisz program rozwiązujący równanie kwadratowe w postaci ogólnej:


$$a \cdot x^2 + b \cdot x + c = 0$$

### Wymagania:

* Program pobiera od użytkownika współczynniki $a, b, c$ (typu `double`).
* Program weryfikuje warunek $a = 0$:
* Jeśli $a = 0$, program wyświetla informację, że równanie zredukowało się do równania liniowego i wyznacza jego rozwiązanie (zgodnie z logiką z Zadania 2).


* Jeśli $a \neq 0$, program oblicza wyróżnik równania kwadratowego ($\Delta = b^2 - 4ac$) i obsługuje trzy przypadki w zbiorze liczb rzeczywistych $\mathbb{R}$:
1. $\Delta > 0$: dwa rozwiązania $x_1 = \frac{-b - \sqrt{\Delta}}{2a}$, $x_2 = \frac{-b + \sqrt{\Delta}}{2a}$.
2. $\Delta = 0$: jedno rozwiązanie podwójne $x_0 = \frac{-b}{2a}$.
3. $\Delta < 0$: brak rozwiązań w zbiorze liczb rzeczywistych.


* Pierwiastki należy obliczać przy użyciu metody `Math.Sqrt(...)`.

---

## Uwagi formalne i ocena

1. **Konstrukcje warunkowe**:
* Przynajmniej w jednym ze sposobów wyboru/wyświetlania wyników (np. sprawdzanie znaku $\Delta$ lub statusu równania) użyj **trójargumentowego operatora wyrażenia warunkowego** (`condition ? trueExpr : falseExpr`).
* Pozostałą logikę rozgałęzień zrealizuj przy użyciu klasycznych instrukcji `if`, `else if`, `else`.


2. **Diagramy blokowe**:
* Do zadań dotyczących równania liniowego oraz kwadratowego należy dołączyć **diagramy blokowe** przedstawiające pełną logikę algorytmu (uwzględniające wszystkie odgałęzienia i przypadki szczególne).
* Diagramy należy wykonać w wybranym narzędziu graficznym (np. [diagrams.net / draw.io](https://app.diagrams.net/)) i załączyć jako pliki graficzne (`.png`, `.svg` lub `.pdf`) do oddawanego zadania.


3. **Walidacja wejścia**:
* Brak odporności na błędy konwersji znaków (np. wyrzucenie wyjątku `FormatException` po wpisaniu litery zamiast cyfry) skutkuje obniżeniem oceny z danego zadania o 20%.
