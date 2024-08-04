### Pierwszy program w Go

Tworzenie pierwszego programu w Go jest krokiem, który pozwala zrozumieć podstawową strukturę i składnię języka. GoLang, znany ze swojej prostoty, wymaga jedynie kilku elementów, aby zbudować działający program. W tej części omówimy strukturę programu w Go oraz dwa kluczowe elementy: `package main` i `func main()`.

#### Struktura programu

Każdy program w Go ma określoną strukturę, która jest spójna i ułatwia czytelność oraz organizację kodu. Podstawowe elementy struktury programu to:

1. **Pakiet (`package`)**: Każdy plik źródłowy Go musi zaczynać się od deklaracji pakietu. Dla programów wykonywalnych zawsze używa się pakietu `main`.
   
2. **Importy (`import`)**: Sekcja importów pozwala na włączenie zewnętrznych bibliotek i pakietów, które są potrzebne do działania programu.
   
3. **Funkcja główna (`func main()`)**: Funkcja `main` jest punktem wejścia programu. Jest to miejsce, w którym zaczyna się wykonywanie kodu.

Poniżej znajduje się przykładowy, najprostszy program w Go:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

#### `package main` i `func main()`

**`package main`**: 
Pakiety są podstawową jednostką organizacyjną w Go. Każdy plik źródłowy należy do jakiegoś pakietu. Istnieją dwa główne typy pakietów w Go: pakiety biblioteczne i pakiety główne (main). Pakiety biblioteczne zawierają kod, który można zaimportować i używać w innych pakietach. Natomiast `package main` jest specjalnym typem pakietu, który kompiluje się do pliku wykonywalnego.

Kiedy Go kompiluje pakiet `main`, oczekuje, że zawiera on funkcję `main`, która jest punktem wejścia do programu. Bez tej funkcji kompilator zgłosi błąd.

**`func main()`**:
Funkcja `main` jest punktem startowym każdego programu w Go. Jest to funkcja bez parametrów i wartości zwracanej, która inicjuje wykonywanie programu. Każdy program wykonawczy musi mieć dokładnie jedną funkcję `main` w pakiecie `main`. 

W przykładzie:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

- `package main` określa, że kod znajduje się w pakiecie głównym, który zostanie skompilowany jako program wykonywalny.
- `import "fmt"` włącza pakiet `fmt`, który jest standardowym pakietem w Go używanym do formatowania i wyświetlania tekstu.
- `func main()` definiuje funkcję `main`, która zostanie uruchomiona po rozpoczęciu programu. Wewnątrz tej funkcji, `fmt.Println("Hello, World!")` wywołuje funkcję `Println` z pakietu `fmt`, która drukuje tekst "Hello, World!" na standardowe wyjście.

#### Dalsze kroki

Po napisaniu pierwszego programu należy go skompilować i uruchomić. Aby to zrobić, można użyć poleceń w wierszu poleceń (CLI).

1. **Kompilacja**:
   - W terminalu przejdź do katalogu, w którym znajduje się plik źródłowy (np. `hello.go`).
   - Użyj polecenia:
     ```sh
     go build hello.go
     ```
   - To polecenie utworzy plik wykonywalny w tym samym katalogu.

2. **Uruchomienie**:
   - Po skompilowaniu programu, uruchom plik wykonywalny:
     ```sh
     ./hello
     ```
   - W systemie Windows będzie to:
     ```sh
     hello.exe
     ```
   - Program wypisze "Hello, World!" na konsolę.

#### Rozszerzenie programu

Aby lepiej zrozumieć możliwości Go, warto rozszerzyć nasz prosty program. Możemy dodać więcej importów, funkcji i zmiennych.

Przykład bardziej rozbudowanego programu:

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    fmt.Println("Program rozpoczęty")
    fmt.Println("Aktualna data i czas:", time.Now())

    message := createMessage("GoLang")
    fmt.Println(message)
}

func createMessage(name string) string {
    return "Witaj w " + name + "!"
}
```

W powyższym przykładzie:
- Importujemy dodatkowy pakiet `time`, aby uzyskać aktualną datę i godzinę.
- Dodajemy funkcję `createMessage`, która przyjmuje argument typu string i zwraca powitanie.
- Używamy zmiennych i wywołujemy funkcję `time.Now()` w `main`, aby wyświetlić aktualny czas.

#### Podsumowanie

Pierwszy program w Go jest prosty do napisania, a jego struktura jest przejrzysta. `package main` oraz `func main()` są niezbędnymi elementami każdego programu wykonywalnego w Go. Po opanowaniu podstawowej struktury programu można rozszerzać swoje umiejętności, dodając więcej funkcji, importując różne pakiety i tworząc bardziej złożone programy. Dzięki prostocie Go, proces nauki i rozwoju oprogramowania staje się efektywny i przyjemny.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com