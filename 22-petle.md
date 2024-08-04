### Pętle

Pętle są kluczowym elementem programowania, umożliwiającym wielokrotne wykonywanie bloku kodu. W GoLang, główną konstrukcją do realizacji pętli jest `for`. Jest to bardzo elastyczne narzędzie, które może być używane do tworzenia różnych rodzajów pętli, w tym pętli z warunkami oraz pętli nieskończonych. Omówimy teraz składnię i zastosowanie pętli w Go.

#### `for`

Instrukcja `for` w GoLang jest jedyną konstrukcją pętli i może być używana na różne sposoby. Może zastąpić pętle `while` i `do-while`, które występują w innych językach programowania.

1. **Podstawowa składnia `for`**:
   - Składnia:
     ```go
     for initialization; condition; post {
         // kod do wykonania
     }
     ```
   - Przykład:
     ```go
     for i := 0; i < 10; i++ {
         fmt.Println(i)
     }
     ```

   W powyższym przykładzie pętla zaczyna się od inicjalizacji zmiennej `i` o wartości 0, sprawdza warunek `i < 10` przed każdą iteracją i zwiększa `i` o 1 po każdym wykonaniu bloku kodu. Pętla kończy się, gdy warunek `i < 10` przestaje być spełniony.

2. **Pętla z warunkiem**:
   - Pętle `for` mogą być używane podobnie do pętli `while` w innych językach, gdzie sprawdzany jest tylko warunek.
   - Składnia:
     ```go
     for condition {
         // kod do wykonania
     }
     ```
   - Przykład:
     ```go
     i := 0
     for i < 10 {
         fmt.Println(i)
         i++
     }
     ```

   W powyższym przykładzie pętla będzie się wykonywać, dopóki warunek `i < 10` jest spełniony. Wartość `i` jest zwiększana w każdej iteracji.

3. **Pętla nieskończona**:
   - Pętla nieskończona może być utworzona poprzez pominięcie wszystkich trzech części składni `for`.
   - Składnia:
     ```go
     for {
         // kod do wykonania
     }
     ```
   - Przykład:
     ```go
     for {
         fmt.Println("To jest pętla nieskończona")
     }
     ```

   W powyższym przykładzie pętla będzie się wykonywać bez końca, ponieważ nie ma warunku, który by ją zatrzymał. Tego rodzaju pętle mogą być użyteczne w serwerach lub innych długotrwałych procesach, gdzie zakończenie pętli jest zależne od zewnętrznych warunków lub sygnałów.

#### Pętle z warunkami i pętle nieskończone

Pętle z warunkami i pętle nieskończone są często używane w sytuacjach, gdy nie wiadomo z góry, ile razy pętla powinna się wykonać.

1. **Pętla z warunkiem sprawdzanym na początku**:
   - Przykład:
     ```go
     i := 0
     for i < 10 {
         fmt.Println(i)
         i++
     }
     ```

   Tego typu pętla będzie się wykonywać, dopóki warunek `i < 10` jest spełniony. Warunek jest sprawdzany na początku każdej iteracji.

2. **Pętla z warunkiem sprawdzanym na końcu**:
   - GoLang nie posiada bezpośredniej konstrukcji `do-while`, ale można uzyskać ten sam efekt, używając `for` i `break`.
   - Przykład:
     ```go
     i := 0
     for {
         fmt.Println(i)
         i++
         if i >= 10 {
             break
         }
     }
     ```

   W powyższym przykładzie pętla wykona się przynajmniej raz, a warunek jest sprawdzany na końcu każdej iteracji. Jeśli warunek `i >= 10` jest spełniony, pętla jest przerywana instrukcją `break`.

3. **Pętla nieskończona z wyjściem warunkowym**:
   - Czasami pętla powinna być nieskończona, ale musi posiadać warunki wyjścia.
   - Przykład:
     ```go
     for {
         var input string
         fmt.Scanln(&input)
         if input == "exit" {
             break
         }
         fmt.Println("Wprowadziłeś:", input)
     }
     ```

   W tym przykładzie pętla oczekuje na dane wejściowe od użytkownika. Jeśli użytkownik wprowadzi słowo "exit", pętla zostanie przerwana.

4. **Pętla z `continue`**:
   - Instrukcja `continue` powoduje przejście do następnej iteracji pętli, pomijając pozostały kod w aktualnej iteracji.
   - Przykład:
     ```go
     for i := 0; i < 10; i++ {
         if i%2 == 0 {
             continue
         }
         fmt.Println(i)
     }
     ```

   W powyższym przykładzie liczby parzyste są pomijane, a wypisywane są tylko liczby nieparzyste.

5. **Zagnieżdżone pętle**:
   - Pętle mogą być zagnieżdżane, co oznacza, że jedna pętla znajduje się wewnątrz innej.
   - Przykład:
     ```go
     for i := 0; i < 3; i++ {
         for j := 0; j < 3; j++ {
             fmt.Printf("i = %d, j = %d\n", i, j)
         }
     }
     ```

   W powyższym przykładzie każda iteracja zewnętrznej pętli powoduje pełny przebieg wewnętrznej pętli, co daje łącznie 9 wypisanych linii.

#### Podsumowanie

Pętle w GoLang, w szczególności konstrukcja `for`, oferują elastyczne i potężne narzędzie do iteracyjnego wykonywania kodu. Możliwość tworzenia pętli z warunkami, pętli nieskończonych oraz używanie instrukcji takich jak `break` i `continue` pozwala na precyzyjne sterowanie przepływem programu. Zrozumienie i umiejętne wykorzystanie pętli jest kluczowe dla efektywnego programowania w GoLang, umożliwiając tworzenie zarówno prostych, jak i bardzo złożonych aplikacji.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com