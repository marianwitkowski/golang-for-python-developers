### Instrukcje warunkowe

Instrukcje warunkowe pozwalają programowi podejmować decyzje i wykonywać różne bloki kodu w zależności od określonych warunków. W GoLang, głównymi konstrukcjami do realizacji tej funkcjonalności są `if`, `else` oraz `switch`. Omówimy teraz te instrukcje, ich składnię i przykłady użycia.

#### `if`, `else`

Instrukcja `if` jest podstawową konstrukcją warunkową, która pozwala na wykonanie bloku kodu tylko wtedy, gdy określony warunek jest spełniony. Instrukcja `else` może być użyta do określenia alternatywnego bloku kodu, który zostanie wykonany, gdy warunek `if` nie jest spełniony.

1. **Podstawowa składnia `if`**:
   - Składnia:
     ```go
     if condition {
         // kod do wykonania, jeśli warunek jest spełniony
     }
     ```
   - Przykład:
     ```go
     age := 20
     if age >= 18 {
         fmt.Println("Jesteś pełnoletni.")
     }
     ```

2. **Instrukcja `else`**:
   - Składnia:
     ```go
     if condition {
         // kod do wykonania, jeśli warunek jest spełniony
     } else {
         // kod do wykonania, jeśli warunek nie jest spełniony
     }
     ```
   - Przykład:
     ```go
     age := 16
     if age >= 18 {
         fmt.Println("Jesteś pełnoletni.")
     } else {
         fmt.Println("Nie jesteś pełnoletni.")
     }
     ```

3. **Instrukcja `else if`**:
   - Składnia:
     ```go
     if condition1 {
         // kod do wykonania, jeśli condition1 jest spełniony
     } else if condition2 {
         // kod do wykonania, jeśli condition2 jest spełniony
     } else {
         // kod do wykonania, jeśli żaden warunek nie jest spełniony
     }
     ```
   - Przykład:
     ```go
     score := 75
     if score >= 90 {
         fmt.Println("Ocena: A")
     } else if score >= 80 {
         fmt.Println("Ocena: B")
     } else if score >= 70 {
         fmt.Println("Ocena: C")
     } else {
         fmt.Println("Ocena: D")
     }
     ```

4. **Deklaracja w `if`**:
   - W GoLang, możliwe jest zadeklarowanie zmiennej bezpośrednio w instrukcji `if`.
   - Składnia:
     ```go
     if variable := expression; condition {
         // kod do wykonania, jeśli warunek jest spełniony
     }
     ```
   - Przykład:
     ```go
     if x := 42; x > 40 {
         fmt.Println("x jest większe niż 40")
     }
     ```

#### `switch`

Instrukcja `switch` jest bardziej elegancką alternatywą dla wielokrotnych instrukcji `if else`. Umożliwia ona sprawdzanie wartości zmiennej względem wielu warunków (case).

1. **Podstawowa składnia `switch`**:
   - Składnia:
     ```go
     switch variable {
     case value1:
         // kod do wykonania, jeśli variable == value1
     case value2:
         // kod do wykonania, jeśli variable == value2
     default:
         // kod do wykonania, jeśli żaden z warunków nie jest spełniony
     }
     ```
   - Przykład:
     ```go
     day := "Monday"
     switch day {
     case "Monday":
         fmt.Println("Poniedziałek")
     case "Tuesday":
         fmt.Println("Wtorek")
     default:
         fmt.Println("Inny dzień")
     }
     ```

2. **Zastosowanie wielu warunków w jednym `case`**:
   - Składnia:
     ```go
     switch variable {
     case value1, value2:
         // kod do wykonania, jeśli variable == value1 lub variable == value2
     }
     ```
   - Przykład:
     ```go
     day := "Saturday"
     switch day {
     case "Saturday", "Sunday":
         fmt.Println("Weekend")
     default:
         fmt.Println("Dzień roboczy")
     }
     ```

3. **Instrukcja `switch` bez zmiennej**:
   - Można użyć `switch` bez zmiennej do sprawdzania różnych warunków.
   - Składnia:
     ```go
     switch {
     case condition1:
         // kod do wykonania, jeśli condition1 jest spełniony
     case condition2:
         // kod do wykonania, jeśli condition2 jest spełniony
     }
     ```
   - Przykład:
     ```go
     number := 15
     switch {
     case number%2 == 0:
         fmt.Println("Liczba parzysta")
     case number%2 != 0:
         fmt.Println("Liczba nieparzysta")
     }
     ```

#### Przykłady zastosowania instrukcji warunkowych

1. **Prosty kalkulator**:
   - Użycie instrukcji `if` i `else` do wykonania operacji matematycznych.
     ```go
     func calculator(a float64, b float64, operator string) float64 {
         if operator == "+" {
             return a + b
         } else if operator == "-" {
             return a - b
         } else if operator == "*" {
             return a * b
         } else if operator == "/" {
             if b != 0 {
                 return a / b
             } else {
                 fmt.Println("Błąd: Dzielenie przez zero")
                 return 0
             }
         } else {
             fmt.Println("Błędny operator")
             return 0
         }
     }
     ```

2. **Ocena wieku**:
   - Użycie `switch` do oceny wieku i przypisania kategorii.
     ```go
     func categorizeAge(age int) {
         switch {
         case age < 13:
             fmt.Println("Dziecko")
         case age >= 13 && age < 20:
             fmt.Println("Nastolatek")
         case age >= 20 && age < 65:
             fmt.Println("Dorosły")
         default:
             fmt.Println("Senior")
         }
     }
     ```

3. **Wykrywanie dnia tygodnia**:
   - Użycie `switch` z zmienną do wyświetlania dnia tygodnia.
     ```go
     func dayOfWeek(day int) {
         switch day {
         case 1:
             fmt.Println("Poniedziałek")
         case 2:
             fmt.Println("Wtorek")
         case 3:
             fmt.Println("Środa")
         case 4:
             fmt.Println("Czwartek")
         case 5:
             fmt.Println("Piątek")
         case 6:
             fmt.Println("Sobota")
         case 7:
             fmt.Println("Niedziela")
         default:
             fmt.Println("Nieprawidłowy dzień")
         }
     }
     ```

#### Podsumowanie

Instrukcje warunkowe w GoLang, takie jak `if`, `else` i `switch`, umożliwiają programowi podejmowanie decyzji i wykonywanie różnych bloków kodu w zależności od spełnienia określonych warunków. `if` i `else` są idealne do prostych decyzji i warunków, natomiast `switch` oferuje bardziej przejrzysty i zorganizowany sposób obsługi wielu warunków. Poprawne stosowanie tych konstrukcji pozwala na tworzenie bardziej złożonych i dynamicznych aplikacji.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com