### Operatory i wyrażenia

W GoLang, operatory i wyrażenia odgrywają kluczową rolę w manipulowaniu danymi i sterowaniu przepływem programu. Operatory są symbolami, które instruują kompilator do wykonania określonej operacji matematycznej, logicznej lub relacyjnej. Wyrażenia to kombinacje zmiennych, wartości i operatorów, które są oceniane i zwracają wynik. W tej części omówimy operatory arytmetyczne, logiczne, relacyjne oraz tworzenie wyrażeń w Go.

#### Operatory arytmetyczne

Operatory arytmetyczne są używane do wykonywania podstawowych operacji matematycznych na liczbach.

1. **Dodawanie (`+`)**:
   - Dodaje dwie liczby.
   - Przykład:
     ```go
     result := 5 + 3 // result = 8
     ```

2. **Odejmowanie (`-`)**:
   - Odejmuje jedną liczbę od drugiej.
   - Przykład:
     ```go
     result := 10 - 4 // result = 6
     ```

3. **Mnożenie (`*`)**:
   - Mnoży dwie liczby.
   - Przykład:
     ```go
     result := 7 * 2 // result = 14
     ```

4. **Dzielenie (`/`)**:
   - Dzieli jedną liczbę przez drugą. Wynik dzielenia liczb całkowitych jest również liczbą całkowitą (część ułamkowa jest odrzucana).
   - Przykład:
     ```go
     result := 8 / 3 // result = 2
     ```

5. **Modulo (`%`)**:
   - Zwraca resztę z dzielenia jednej liczby przez drugą.
   - Przykład:
     ```go
     result := 10 % 3 // result = 1
     ```

#### Operatory logiczne

Operatory logiczne są używane do wykonywania operacji logicznych na wartościach boolowskich.

1. **AND (`&&`)**:
   - Zwraca `true` tylko wtedy, gdy oba operandy są `true`.
   - Przykład:
     ```go
     result := true && false // result = false
     ```

2. **OR (`||`)**:
   - Zwraca `true`, jeśli przynajmniej jeden z operandów jest `true`.
   - Przykład:
     ```go
     result := true || false // result = true
     ```

3. **NOT (`!`)**:
   - Neguje wartość logiczną (zamienia `true` na `false` i odwrotnie).
   - Przykład:
     ```go
     result := !true // result = false
     ```

#### Operatory relacyjne

Operatory relacyjne porównują dwie wartości i zwracają wartość boolowską (`true` lub `false`).

1. **Równość (`==`)**:
   - Sprawdza, czy dwie wartości są równe.
   - Przykład:
     ```go
     result := (5 == 5) // result = true
     ```

2. **Nierówność (`!=`)**:
   - Sprawdza, czy dwie wartości są różne.
   - Przykład:
     ```go
     result := (5 != 3) // result = true
     ```

3. **Mniejszość (`<`)**:
   - Sprawdza, czy jedna wartość jest mniejsza od drugiej.
   - Przykład:
     ```go
     result := (3 < 5) // result = true
     ```

4. **Większość (`>`)**:
   - Sprawdza, czy jedna wartość jest większa od drugiej.
   - Przykład:
     ```go
     result := (5 > 3) // result = true
     ```

5. **Mniejszość lub równość (`<=`)**:
   - Sprawdza, czy jedna wartość jest mniejsza lub równa drugiej.
   - Przykład:
     ```go
     result := (3 <= 3) // result = true
     ```

6. **Większość lub równość (`>=`)**:
   - Sprawdza, czy jedna wartość jest większa lub równa drugiej.
   - Przykład:
     ```go
     result := (5 >= 3) // result = true
     ```

#### Tworzenie wyrażeń

Wyrażenia w GoLang to kombinacje wartości, zmiennych, operatorów i funkcji, które są oceniane i zwracają wynik. Mogą być proste, jak arytmetyczne obliczenia, lub bardziej złożone, wykorzystujące logikę i porównania.

1. **Proste wyrażenia arytmetyczne**:
   - Przykład dodawania i mnożenia:
     ```go
     a := 5
     b := 10
     result := (a + b) * 2 // result = 30
     ```

2. **Wyrażenia logiczne**:
   - Przykład użycia operatorów logicznych:
     ```go
     isAdult := true
     hasID := false
     canEnter := isAdult && hasID // canEnter = false
     ```

3. **Wyrażenia relacyjne**:
   - Przykład porównania wartości:
     ```go
     age := 20
     isTeenager := age >= 13 && age <= 19 // isTeenager = false
     ```

4. **Kombinacja różnych operatorów**:
   - Przykład bardziej złożonego wyrażenia:
     ```go
     a := 5
     b := 10
     c := 3
     result := (a + b > c) && (b - c < a) // result = true
     ```

5. **Wyrażenia z funkcjami**:
   - Przykład użycia funkcji w wyrażeniach:
     ```go
     func add(x int, y int) int {
         return x + y
     }

     func main() {
         result := add(5, 3) * 2 // result = 16
         fmt.Println(result)
     }
     ```

6. **Inkrementacja i dekrementacja**:
   - Operatory `++` i `--` są używane do zwiększania lub zmniejszania wartości zmiennej o 1.
   - Przykład:
     ```go
     a := 5
     a++ // a = 6
     a-- // a = 5
     ```

#### Podsumowanie

Operatory i wyrażenia w GoLang są niezbędnymi narzędziami do tworzenia funkcjonalnego i wydajnego kodu. Operatory arytmetyczne, logiczne i relacyjne pozwalają na wykonywanie podstawowych i złożonych operacji na danych. Tworzenie wyrażeń umożliwia programistom łączenie tych operacji w celu rozwiązania konkretnych problemów i realizacji zadań. Dzięki prostocie i przejrzystości składni Go, operatory i wyrażenia są intuicyjne i łatwe do nauki, co czyni GoLang idealnym wyborem dla zarówno początkujących, jak i doświadczonych programistów.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com