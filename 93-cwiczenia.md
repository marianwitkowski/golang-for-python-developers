### Ćwiczenia i quizy

#### Zadania praktyczne do samodzielnego rozwiązania

Ćwiczenia praktyczne są kluczowe dla zrozumienia i efektywnego wykorzystania języka Go (Golang). Poniżej znajdziesz zestaw zadań, które pomogą ci wzmocnić Twoje umiejętności programistyczne bez korzystania z podstawowych przykładów typu "Hello, World!".

### Zadanie 1: Kalkulator

**Cel:** Stwórz prosty kalkulator, który wykonuje podstawowe operacje arytmetyczne (dodawanie, odejmowanie, mnożenie, dzielenie).

**Wymagania:**
- Użytkownik wprowadza dwie liczby i wybiera operację.
- Program wykonuje operację i wyświetla wynik.

**Przykładowy kod:**
```go
package main

import (
    "fmt"
    "log"
    "os"
)

func main() {
    var num1, num2 float64
    var operator string

    fmt.Print("Enter first number: ")
    if _, err := fmt.Scanln(&num1); err != nil {
        log.Println("Failed to read the first number:", err)
        os.Exit(1)
    }

    fmt.Print("Enter operator (+, -, *, /): ")
    if _, err := fmt.Scanln(&operator); err != nil {
        log.Println("Failed to read the operator:", err)
        os.Exit(1)
    }

    fmt.Print("Enter second number: ")
    if _, err := fmt.Scanln(&num2); err != nil {
        log.Println("Failed to read the second number:", err)
        os.Exit(1)
    }

    switch operator {
    case "+":
        fmt.Printf("Result: %.2f\n", num1+num2)
    case "-":
        fmt.Printf("Result: %.2f\n", num1-num2)
    case "*":
        fmt.Printf("Result: %.2f\n", num1*num2)
    case "/":
        if num2 == 0 {
            fmt.Println("Error: Division by zero.")
            return
        }
        fmt.Printf("Result: %.2f\n", num1/num2)
    default:
        fmt.Println("Invalid operator")
    }
}
```

### Zadanie 2: Sortowanie listy

**Cel:** Napisz funkcję, która sortuje listę liczb w porządku rosnącym.

**Wymagania:**
- Implementacja własnego algorytmu sortowania (np. sortowanie bąbelkowe).
- Wykorzystanie gotowej funkcji `sort` z pakietu `sort` dla porównania wyników.

**Przykładowy kod:**
```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    numbers := []int{4, 2, 7, 1, 3}
    fmt.Println("Original:", numbers)

    sort.Ints(numbers)
    fmt.Println("Sorted:", numbers)
}

func bubbleSort(numbers []int) {
    n := len(numbers)
    for i := 0; i < n; i++ {
        for j := 0; j < n-i-1; j++ {
            if numbers[j] > numbers[j+1] {
                numbers[j], numbers[j+1] = numbers[j+1], numbers[j]
            }
        }
    }
}
```

### Zadanie 3: Filtr liczb parzystych

**Cel:** Napisz program, który filtruje listę liczb i zwraca tylko te, które są parzyste.

**Wymagania:**
- Użyj `for` i `if` do iteracji i filtrowania listy.
- Wykorzystaj funkcję `filter` w Go.

**Przykładowy kod:**
```go
package main

import "fmt"

func main() {
    numbers := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
    evenNumbers := filterEvenNumbers(numbers)
    fmt.Println("Even numbers:", evenNumbers)
}

func filterEvenNumbers(numbers []int) []int {
    var result []int
    for _, number := range numbers {
        if number%2 == 0 {
            result = append(result, number)
        }
    }
    return result
}
```

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com