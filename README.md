# Lab 02: Pętle i sterowanie przebiegiem programu w C#

| Parametr | Szczegóły |
| --- | --- |
| **Termin oddania** | 22.11.2026, godz. 23:00 |
| **Suma punktów** | 20 pkt |
| **Język / Platforma** | C# (.NET 8+) |
| **Wymagane środowisko** | Visual Studio 2022 / VS Code (z C# Dev Kit) / JetBrains Rider |

---

### Zasady terminowości

Przekroczenie terminu o $n$ zajęć (lub tygodni) wiąże się ze zmniejszeniem maksymalnej liczby punktów zdobytych za zadanie według wzoru:

$$\text{Punkty końcowe} = \frac{\text{Punkty uzyskane}}{2^n}$$

---

## Wymagania techniczne i środowiskowe

1. **Struktura projektu**: Zadania należy zrealizować w ramach jednego rozwiązania (Solucji / Solution) zawierającego 3 osobne projekty konsolowe lub jednego projektu z menu wyboru zadania. Zadania tworzą spójną historię tekstowej gry turowej typu RPG **„Walka z potworem”**.
2. **Standardy C#**:
* Stosuj właściwe konwencje nazewnictwa C# (`camelCase` dla zmiennych lokalnych, `PascalCase` dla metod i klas).
* Do konwersji i walidacji danych wejściowych z konsoli używaj bezpiecznych metod, np. `int.TryParse(...)`, aby program nie ulegał awarii po wpisaniu nieprawidłowej wartości.
* Losowe obrażenia generuj za pomocą klasy `Random`.
3. **Funkcjonalność IDE**: Wykorzystaj narzędzia wbudowane w wybrane środowisko:
* Przetestuj działanie programu za pomocą debugera (stawianie punktów przerwania — *Breakpoints* — oraz podgląd wartości zmiennych *Watch/Locals*).

---

## Zadanie 1: Pierwsze starcie [4 pkt]

Napisz program konsolowy symulujący pierwszą walkę bohatera z goblinem. Gracz i potwór zadają sobie obrażenia na zmianę, dopóki jeden z nich nie zginie.

### Wymagania:

1. Zdefiniuj zmienne początkowe: `zdrowieGracza = 100` oraz `zdrowiePotwora = 50`.
2. Użyj pętli `while`, która trwa dopóty, dopóki zarówno gracz, jak i potwór mają zdrowie większe od zera (`> 0`).
3. W każdej turze:
* Gracz zadaje potworowi losowe obrażenia, np. od 10 do 20, korzystając z klasy `Random`.
* Jeżeli potwór nadal żyje, oddaje atak, zadając graczowi losowe obrażenia, np. od 5 do 15.
* Wyświetl aktualny stan zdrowia (HP) obu postaci.
4. Po zakończeniu pętli sprawdź, kto przeżył, i wyświetl komunikat o zwycięstwie gracza lub jego porażce.

### Uwagi dotyczące jakości kodu

* Warunek pętli powinien jasno opisywać, kiedy walka trwa, a wartości zdrowia muszą zmieniać się w każdej iteracji. Dzięki temu pętla zawsze ma możliwość zakończenia i nie staje się pętlą nieskończoną.
* Utwórz jedną instancję `Random` przed rozpoczęciem pętli, zamiast tworzyć nową instancję przy każdym ataku.
* Nie wykonuj ataku potwora po jego śmierci. Po każdym ataku sprawdzaj aktualny stan HP, aby wynik tury był logiczny.
* Unikaj „magicznych liczb” — wartości początkowego zdrowia i zakresy obrażeń przechowuj w nazwanych stałych albo zmiennych.
* Przetestuj co najmniej przypadki: potwór ginie po pierwszym ataku, gracz ginie po ataku potwora oraz walka trwa przez wiele iteracji. W debugerze obserwuj wartości HP krok po kroku.

---

## Zadanie 2: Menu akcji i uniki [6 pkt]

Rozbuduj grę z Zadania 1. W każdej turze gracz powinien wybrać akcję, a program musi poprawnie obsługiwać nieprawidłowe wybory.

### Wymagania:

1. Zastosuj pętlę `do-while` do obsługi wyboru akcji przez gracza w jednej turze.
2. Wyświetl menu:
* `[1]` Atak mieczem — zadaje stałe lub losowe obrażenia.
* `[2]` Mikstura lecznicza — przywraca 25 punktów zdrowia. Gracz może użyć maksymalnie 2 mikstur w całej walce.
* `[3]` Ucieczka — natychmiast przerywa walkę.
3. Jeżeli użytkownik wpisze wartość inną niż 1, 2 lub 3, wewnętrzna pętla `do-while` musi poprosić o ponowny wybór. Błędny wpis nie może powodować utraty tury przez potwora.
4. Główna pętla walki powinna działać do momentu zwycięstwa gracza, jego śmierci albo ucieczki.

### Uwagi dotyczące jakości kodu

* Pętla `do-while` jest właściwa dla menu, ponieważ menu musi wyświetlić się co najmniej raz. Warunek powtórzenia powinien obejmować wyłącznie nieprawidłowe wybory.
* Wczytanie wyboru zabezpiecz metodą `int.TryParse(...)`. Nie dopuszczaj do sytuacji, w której błędny tekst kończy program albo powoduje wykonanie przypadkowej akcji.
* Nie twórz osobnych, zduplikowanych fragmentów kodu dla każdej tury. Zmiana HP, liczby wykorzystanych mikstur i informacji o ucieczce powinna być kontrolowana w jednym, czytelnym miejscu.
* Pętla walki musi mieć jasno określone warunki zakończenia. Sprawdź, czy błędny wybór nie zmienia zdrowia, nie zużywa mikstury i nie uruchamia ataku potwora.
* Przetestuj wybory `1`, `2` i `3`, wartość spoza zakresu, tekst zamiast liczby, próbę użycia trzeciej mikstury oraz sytuację, w której gracz ucieka z minimalnym i maksymalnym HP.

---

## Zadanie 3: Wyprawa do lochu i system poziomów [10 pkt]

Rozbuduj grę o wyprawę do lochu składającego się z kolejnych fal przeciwników. Bohater powinien pokonać trzy potwory pod rząd i zdobywać doświadczenie.

### Wymagania:

1. Zastosuj zagnieżdżone pętle: zewnętrzna pętla ma sterować kolejnymi potworami w lochu, a wewnętrzna — turową walką z aktualnym przeciwnikiem.
2. Zaprogramuj walkę z trzema potworami po kolei. Każdy kolejny przeciwnik powinien być silniejszy, np. mieć zdrowie obliczone według wzoru `30 + i * 15`, gdzie `i` oznacza numer potwora.
3. Po pokonaniu potwora, przed przejściem do następnego:
* Przywróć graczowi część zdrowia, np. 20 punktów.
* Wyświetl podsumowanie statystyk, w tym liczbę pokonanych wrogów i aktualny poziom postaci.
4. Jeżeli gracz zginie podczas dowolnej walki, natychmiast przerwij obie pętle za pomocą `break` i wyświetl komunikat **Game Over**.

### Uwagi dotyczące jakości kodu

* Użyj pętli `for` jako pętli zewnętrznej, ponieważ liczba potworów jest znana z góry, oraz pętli `while` jako wewnętrznej, ponieważ liczba tur potrzebnych do pokonania potwora nie jest znana.
* Licznik potworów i zmienne dotyczące bieżącej walki powinny mieć jednoznaczne zakresy. Nie zmieniaj licznika pętli zewnętrznej wewnątrz pętli walki.
* `break` stosuj tylko do jasno określonego celu — zakończenia aktualnej pętli po śmierci gracza. Jeżeli do przerwania obu pętli potrzebujesz dodatkowej zmiennej stanu, jej nazwa powinna jednoznacznie wskazywać przyczynę zakończenia, np. `gameOver`.
* Regeneracja nie powinna przekraczać maksymalnego zdrowia gracza. Aktualizację poziomu i statystyk wykonuj w jednym miejscu po zakończeniu walki z przeciwnikiem.
* Przetestuj loch z trzema przeciwnikami, śmierć podczas pierwszej i kolejnych walk oraz przejście do następnego przeciwnika po zwycięstwie. W debugerze obserwuj jednocześnie licznik pętli zewnętrznej, HP i liczbę pokonanych wrogów.

---

## Uwagi formalne i ocena

1. **Pętle i sterowanie przepływem**:
* W Zadaniu 1 obowiązkowo użyj pętli `while`.
* W Zadaniu 2 użyj pętli `do-while` do walidacji wyboru akcji oraz pętli sterującej walką.
* W Zadaniu 3 użyj zagnieżdżonych pętli i instrukcji `break` do zakończenia walki po śmierci gracza.
* Rozgałęzienia warunkowe zrealizuj za pomocą instrukcji `if`, `else if`, `else`. W co najmniej jednym miejscu możesz dodatkowo zastosować operator warunkowy (`condition ? trueExpr : falseExpr`).

2. **Dokumentacja algorytmu**:
* Do każdego zadania należy dołączyć diagram blokowy przedstawiający pełną logikę algorytmu, w tym warunki zakończenia pętli i wszystkie istotne odgałęzienia.
* Diagramy należy wykonać w wybranym narzędziu graficznym (np. [diagrams.net / draw.io](https://app.diagrams.net/)) i załączyć jako pliki graficzne (`.png`, `.svg` lub `.pdf`) do oddawanego zadania.

3. **Walidacja wejścia**:
* Program nie może przerywać działania po wpisaniu tekstu zamiast liczby ani po podaniu wartości spoza dostępnego menu.
* Brak odporności na błędy konwersji lub brak walidacji wyboru skutkuje obniżeniem oceny z danego zadania o 20%.
