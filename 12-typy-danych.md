### Podstawowe typy danych

GoLang, znany ze swojej prostoty i efektywności, oferuje szeroki zakres typów danych, które można podzielić na dwie główne kategorie: typy proste i typy złożone. Znajomość tych typów jest kluczowa do efektywnego programowania w Go.

#### Typy proste: int, float, string, bool

1. **int**:
   - Typ całkowity, używany do przechowywania liczb całkowitych.
   - W Go mamy kilka wariantów typu `int`:
     - `int` oraz `uint` (długość zależna od architektury systemu, zazwyczaj 32 lub 64 bity).
     - `int8`, `int16`, `int32`, `int64` (całkowite o stałej długości).
     - `uint8`, `uint16`, `uint32`, `uint64` (całkowite bez znaku o stałej długości).
   - Przykład:
     ```go
     var a int = 10
     var b uint = 20
     var c int64 = -100
     ```

2. **float**:
   - Typ zmiennoprzecinkowy, używany do przechowywania liczb rzeczywistych.
   - W Go dostępne są dwa typy zmiennoprzecinkowe:
     - `float32`
     - `float64` (częściej używany ze względu na większą precyzję).
   - Przykład:
     ```go
     var x float32 = 3.14
     var y float64 = 2.71828
     ```

3. **string**:
   - Typ ciągu znaków, używany do przechowywania tekstu.
   - Ciągi znaków w Go są niemodyfikowalne (immutable).
   - Przykład:
     ```go
     var greeting string = "Hello, World!"
     ```

4. **bool**:
   - Typ logiczny, używany do przechowywania wartości prawda/fałsz.
   - Przyjmuje jedną z dwóch wartości: `true` lub `false`.
   - Przykład:
     ```go
     var isGoLangFun bool = true
     ```

#### Typy złożone: arrays, slices, maps

1. **arrays**:
   - Tablice są uporządkowanymi zbiorami elementów o tym samym typie.
   - Rozmiar tablicy jest z góry ustalony i nie może być zmieniony po jej utworzeniu.
   - Przykład:
     ```go
     var nums [5]int
     nums[0] = 1
     nums[1] = 2
     fmt.Println(nums) // Output: [1 2 0 0 0]
     ```
   - Inicjalizacja z wartościami:
     ```go
     primes := [5]int{2, 3, 5, 7, 11}
     fmt.Println(primes) // Output: [2 3 5 7 11]
     ```

2. **slices**:
   - Slices są dynamicznymi, elastycznymi widokami na tablice.
   - Slices mogą zmieniać rozmiar w czasie działania programu.
   - Przykład tworzenia slice:
     ```go
     var nums []int
     nums = append(nums, 1)
     nums = append(nums, 2)
     fmt.Println(nums) // Output: [1 2]
     ```
   - Inicjalizacja z wartościami:
     ```go
     primes := []int{2, 3, 5, 7, 11}
     fmt.Println(primes) // Output: [2 3 5 7 11]
     ```

3. **maps**:
   - Mapy są kolekcjami par klucz-wartość.
   - Klucze muszą być unikalne i mogą być różnych typów.
   - Przykład tworzenia mapy:
     ```go
     var personAge map[string]int
     personAge = make(map[string]int)
     personAge["Alice"] = 30
     personAge["Bob"] = 25
     fmt.Println(personAge) // Output: map[Alice:30 Bob:25]
     ```
   - Inicjalizacja z wartościami:
     ```go
     personAge := map[string]int{"Alice": 30, "Bob": 25}
     fmt.Println(personAge) // Output: map[Alice:30 Bob:25]
     ```

#### Przykłady użycia typów złożonych

Aby lepiej zrozumieć, jak działają typy złożone w Go, spójrzmy na kilka praktycznych przykładów.

1. **Tablice**:
   - Tworzenie tablicy liczb całkowitych i iterowanie po niej:
     ```go
     nums := [5]int{1, 2, 3, 4, 5}
     for i, num := range nums {
         fmt.Printf("Element %d: %d\n", i, num)
     }
     ```

2. **Slices**:
   - Tworzenie slice z elementów i dodawanie nowych elementów:
     ```go
     fruits := []string{"Apple", "Banana", "Cherry"}
     fruits = append(fruits, "Date")
     fmt.Println(fruits) // Output: [Apple Banana Cherry Date]
     ```
   - Slicing (wycinanie) części slice:
     ```go
     subset := fruits[1:3]
     fmt.Println(subset) // Output: [Banana Cherry]
     ```

3. **Maps**:
   - Tworzenie mapy z danymi kontaktowymi:
     ```go
     contacts := map[string]string{
         "Alice": "alice@example.com",
         "Bob":   "bob@example.com",
     }
     fmt.Println(contacts["Alice"]) // Output: alice@example.com
     ```

   - Dodawanie i usuwanie elementów z mapy:
     ```go
     contacts["Charlie"] = "charlie@example.com"
     delete(contacts, "Bob")
     fmt.Println(contacts) // Output: map[Alice:alice@example.com Charlie:charlie@example.com]
     ```

#### Podsumowanie

Typy proste i złożone w GoLang pozwalają na efektywne przechowywanie i manipulowanie danymi. Typy proste, takie jak `int`, `float`, `string` i `bool`, są podstawą każdego programu. Typy złożone, takie jak tablice, slice i mapy, oferują elastyczne i potężne mechanizmy do zarządzania bardziej złożonymi strukturami danych. Znajomość i umiejętność korzystania z tych typów jest kluczowa dla każdego programisty Go, pozwalając na tworzenie wydajnych i dobrze zorganizowanych aplikacji.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com