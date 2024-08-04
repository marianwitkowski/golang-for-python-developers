### Funkcje

Funkcje są fundamentalnym elementem programowania, umożliwiającym modularność i wielokrotne wykorzystanie kodu. W języku GoLang, funkcje są wszechstronne i oferują wiele możliwości, w tym zwracanie wielu wyników oraz tworzenie funkcji anonimowych i zamknięć. Omówimy teraz szczegółowo definiowanie i wywoływanie funkcji, funkcje zwracające wiele wyników oraz funkcje anonimowe i zamknięcia.

#### Definiowanie i wywoływanie funkcji

Funkcje w GoLang są definiowane przy użyciu słowa kluczowego `func`, po którym następuje nazwa funkcji, lista parametrów w nawiasach, typ(y) zwracanych wartości oraz ciało funkcji.

1. **Podstawowa składnia funkcji**:
   - Składnia:
     ```go
     func functionName(parameter1 type1, parameter2 type2) returnType {
         // ciało funkcji
     }
     ```
   - Przykład:
     ```go
     func add(a int, b int) int {
         return a + b
     }
     ```

   W powyższym przykładzie funkcja `add` przyjmuje dwa parametry typu `int` i zwraca wartość typu `int`, która jest sumą tych parametrów.

2. **Wywoływanie funkcji**:
   - Funkcję wywołuje się, podając jej nazwę oraz argumenty w nawiasach.
   - Przykład:
     ```go
     result := add(3, 4)
     fmt.Println(result) // Wyjście: 7
     ```

   W powyższym przykładzie funkcja `add` jest wywoływana z argumentami `3` i `4`, a wynik jest przypisany do zmiennej `result` i wypisany.

3. **Funkcje bez parametrów i wartości zwracanej**:
   - Funkcje mogą nie przyjmować żadnych parametrów ani nie zwracać wartości.
   - Przykład:
     ```go
     func greet() {
         fmt.Println("Hello, world!")
     }

     greet() // Wyjście: Hello, world!
     ```

#### Funkcje z wieloma wynikami

Jedną z unikalnych cech GoLang jest możliwość zwracania wielu wyników z funkcji. Jest to szczególnie użyteczne w przypadku funkcji, które mogą zwracać wyniki oraz błędy.

1. **Definiowanie funkcji zwracającej wiele wyników**:
   - Składnia:
     ```go
     func functionName(parameter1 type1) (returnType1, returnType2) {
         // ciało funkcji
         return value1, value2
     }
     ```
   - Przykład:
     ```go
     func divide(a, b float64) (float64, error) {
         if b == 0 {
             return 0, errors.New("division by zero")
         }
         return a / b, nil
     }
     ```

   W powyższym przykładzie funkcja `divide` zwraca dwie wartości: wynik dzielenia i ewentualny błąd.

2. **Wywoływanie funkcji zwracającej wiele wyników**:
   - Przykład:
     ```go
     result, err := divide(4, 2)
     if err != nil {
         fmt.Println("Error:", err)
     } else {
         fmt.Println("Result:", result) // Wyjście: Result: 2
     }
     ```

   W powyższym przykładzie funkcja `divide` jest wywoływana z argumentami `4` i `2`, a zwracane wartości są przypisane do zmiennych `result` i `err`.

#### Funkcje anonimowe i zamknięcia

Funkcje anonimowe (anonimowe funkcje) to funkcje bez nazwy, które można definiować i wywoływać w locie. Zamknięcia (closures) to funkcje, które mają dostęp do zmiennych spoza swojego zakresu.

1. **Funkcje anonimowe**:
   - Funkcje anonimowe są definiowane podobnie jak zwykłe funkcje, ale bez nazwy.
   - Przykład:
     ```go
     add := func(a, b int) int {
         return a + b
     }

     result := add(3, 4)
     fmt.Println(result) // Wyjście: 7
     ```

   W powyższym przykładzie funkcja anonimowa jest przypisana do zmiennej `add` i wywoływana za pomocą tej zmiennej.

2. **Natychmiastowe wywołanie funkcji anonimowej**:
   - Przykład:
     ```go
     result := func(a, b int) int {
         return a + b
     }(3, 4)

     fmt.Println(result) // Wyjście: 7
     ```

   W powyższym przykładzie funkcja anonimowa jest definiowana i wywoływana natychmiast z argumentami `3` i `4`.

3. **Zamknięcia (closures)**:
   - Zamknięcia mają dostęp do zmiennych spoza swojego zakresu.
   - Przykład:
     ```go
     func main() {
         x := 10
         increment := func() int {
             x++
             return x
         }

         fmt.Println(increment()) // Wyjście: 11
         fmt.Println(increment()) // Wyjście: 12
     }
     ```

   W powyższym przykładzie funkcja anonimowa `increment` ma dostęp do zmiennej `x` zdefiniowanej poza jej zakresem i może ją modyfikować.

4. **Zastosowanie zamknięć w praktyce**:
   - Zamknięcia są często używane do enkapsulacji stanu w funkcjach.
   - Przykład:
     ```go
     func adder() func(int) int {
         sum := 0
         return func(x int) int {
             sum += x
             return sum
         }
     }

     func main() {
         pos, neg := adder(), adder()
         for i := 0; i < 10; i++ {
             fmt.Println(pos(i), neg(-2*i))
         }
     }
     ```

   W powyższym przykładzie funkcja `adder` zwraca funkcję anonimową, która enkapsuluje zmienną `sum`, umożliwiając tworzenie niezależnych liczników.

#### Podsumowanie

Funkcje w GoLang są kluczowym narzędziem do organizacji i modularności kodu. Możliwość definiowania funkcji zwracających wiele wyników zwiększa elastyczność i czytelność kodu, szczególnie w przypadku obsługi błędów. Funkcje anonimowe i zamknięcia pozwalają na bardziej zaawansowane techniki programistyczne, takie jak enkapsulacja stanu i dynamiczne definiowanie zachowań. Poprawne zrozumienie i wykorzystanie tych mechanizmów jest niezbędne do efektywnego programowania w GoLang.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com