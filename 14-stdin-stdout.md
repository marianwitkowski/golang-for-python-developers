### Standardowe Wejście i Wyjście

Standardowe wejście i wyjście (stdin i stdout) są podstawowymi mechanizmami interakcji między użytkownikiem a programami działającymi w konsoli. W języku Go, obsługa wejścia i wyjścia jest prosta i efektywna, umożliwiając tworzenie interaktywnych aplikacji konsolowych. W tym rozdziale omówimy techniki odczytu danych z klawiatury, ich walidacji oraz zaawansowane formatowanie wyświetlanych danych.

#### Odczyt wartości z klawiatury i ich walidacja

##### Odczyt danych z klawiatury

Odczyt danych z klawiatury w Go można zrealizować przy użyciu pakietu `fmt` oraz `bufio`. Podstawowe odczytywanie danych za pomocą `fmt.Scanln()` jest bardzo proste:

```go
package main

import "fmt"

func main() {
    fmt.Println("Jak masz na imię?")
    var name string
    fmt.Scanln(&name)
    fmt.Println("Witaj, ", name)
}
```

W tym kodzie użytkownik jest proszony o wprowadzenie imienia, które następnie jest odczytywane do zmiennej `name` za pomocą `fmt.Scanln()`.

##### Użycie `bufio.Scanner` do odczytu danych

Dla bardziej zaawansowanych scenariuszy, takich jak odczytywanie wielu linii lub większych ilości danych, można użyć `bufio.Scanner`:

```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    scanner := bufio.NewScanner(os.Stdin)
    fmt.Print("Podaj swoje imię: ")
    scanner.Scan()
    name := scanner.Text()
    fmt.Printf("Witaj, %s!\n", name)
}
```

`bufio.Scanner` oferuje bardziej elastyczne i wydajne metody odczytywania danych z klawiatury, zwłaszcza przy pracy z dużymi ilościami danych.

##### Walidacja danych wejściowych

Walidacja danych wejściowych jest kluczowa, aby zapewnić poprawność i bezpieczeństwo aplikacji. Poniżej przedstawiono kilka przykładów walidacji danych:

###### Walidacja adresu email

```go
package main

import (
    "bufio"
    "fmt"
    "os"
    "regexp"
)

func main() {
    scanner := bufio.NewScanner(os.Stdin)
    fmt.Print("Podaj swój adres email: ")
    scanner.Scan()
    email := scanner.Text()

    match, _ := regexp.MatchString(`^[a-z0-9._%+\-]+@[a-z0-9.\-]+\.[a-z]{2,4}$`, email)
    if match {
        fmt.Println("Adres email jest poprawny.")
    } else {
        fmt.Println("Adres email jest niepoprawny.")
    }
}
```

W powyższym kodzie, wyrażenie regularne jest używane do sprawdzenia, czy wprowadzony adres email jest w poprawnym formacie.

###### Sprawdzanie, czy wprowadzony tekst jest liczbą całkowitą lub zmiennoprzecinkową

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    fmt.Print("Podaj wartość: ")
    var input string
    fmt.Scanln(&input)

    if _, err := strconv.Atoi(input); err == nil {
        fmt.Println("Podano liczbę całkowitą.")
    } else if _, err := strconv.ParseFloat(input, 64); err == nil {
        fmt.Println("Podano liczbę zmiennoprzecinkową.")
    } else {
        fmt.Println("Podana wartość nie jest liczbą.")
    }
}
```

W tym przykładzie używamy `strconv.Atoi` do sprawdzenia, czy wprowadzony tekst jest liczbą całkowitą, oraz `strconv.ParseFloat` do sprawdzenia, czy jest liczbą zmiennoprzecinkową.

#### Wyświetlanie danych oraz ich formatowanie

Wyświetlanie danych w przejrzysty sposób jest równie ważne jak ich odczyt. Pakiet `fmt` w Go oferuje wiele funkcji do formatowania tekstu, które mogą być użyte do poprawy czytelności danych wyjściowych.

##### Podstawowe formatowanie tekstu

Pakiet `fmt` pozwala na użycie różnych specyfikatorów formatu, które umożliwiają precyzyjne kontrolowanie wyglądu danych wyjściowych:

1. **%v** - Domyślny format dla wartości zmiennej.
2. **%+v** - Rozszerzony format, pokazuje również pola struktur.
3. **%#v** - Drukuje wartość w formie, która może być bezpośrednio użyta do ponownego utworzenia elementu.
4. **%T** - Drukuje typ wartości.
5. **%d** - Formatuje liczby całkowite (dla typów bazujących na liczbach całkowitych).
6. **%s** - Dla stringów.
7. **%f** - Dla liczb zmiennoprzecinkowych.
8. **%p** - Drukuje wartość wskaźnika.
9. **%c** - Znak o określonym numerze ASCII.
10. **%q** - Cytuje stringi i znaki.

##### Zaawansowane formatowanie

Do zaawansowanego formatowania należy między innymi ustawienie szerokości i precyzji, co jest szczególnie użyteczne przy prezentacji tabelarycznej danych lub przy wyświetlaniu wyników finansowych:

```go
package main

import "fmt"

func main() {
    fmt.Printf("Nazwa: %10s | Cena: %5.2f zł\n", "Chleb", 3.49)
    fmt.Printf("Nazwa: %10s | Cena: %5.2f zł\n", "Masło", 7.55)
}
```

W tym przykładzie, użyto `%10s` do wyrównania tekstu do lewej z zachowaniem stałej szerokości kolumn, oraz `%5.2f` do formatowania liczb zmiennoprzecinkowych z dokładnością do dwóch miejsc po przecinku.

##### Inne przydatne specyfikatory formatowania

1. **%x / %X** - Formatuje liczby w systemie szesnastkowym (małe / wielkie litery).
2. **%b** - Formatuje liczby w systemie binarnym.
3. **%e / %E** - Formatuje liczby zmiennoprzecinkowe w notacji naukowej (małe / wielkie litery).
4. **%t** - Formatuje wartości boolowskie.
5. **%o** - Formatuje liczby w systemie ósemkowym.
6. **%U** - Formatuje wartości Unicode.
7. **%#x / %#X** - Formatuje liczby w systemie szesnastkowym z prefiksem `0x` / `0X`.
8. **%+d** - Dodaje znak plusa dla liczb dodatnich.
9. **%0*d** - Wyrównanie liczb całkowitych do określonej szerokości z wiodącymi zerami.

#### Przykłady zastosowań

##### Formatowanie tabelaryczne

```go
package main

import "fmt"

func main() {
    header := fmt.Sprintf("%-10s | %-10s | %-10s", "Nazwa", "Kategoria", "Cena")
    row1 := fmt.Sprintf("%-10s | %-10s | %-10.2f", "Chleb", "Spożywcze", 3.49)
    row2 := fmt.Sprintf("%-10s | %-10s | %-10.2f", "Masło", "Nabiał", 7.55)
    fmt.Println(header)
    fmt.Println(row1)
    fmt.Println(row2)
}
```

##### Formatowanie liczb zmiennoprzecinkowych w notacji naukowej

```go
package main

import "fmt"

func main() {
    pi := 3.141592653589793
    fmt.Printf("Pi in scientific notation: %e\n", pi)
    fmt.Printf("Pi in scientific notation (capital E): %E\n", pi)
}
```

##### Formatowanie wartości boolowskich

```go
package main

import "fmt"

func main() {
    flag := true
    fmt.Printf("The value of flag is %t\n", flag)
}
```

#### Podsumowanie

Zarządzanie standardowym wejściem i wyjściem w Go jest kluczowe dla tworzenia interaktywnych aplikacji CLI. Użycie pakietów takich jak `fmt` do odczytu, walidacji i formatowania danych wejściowych i wyjściowych zapewnia użytkownikom końcowym płynne i intuicyjne doświadczenie. Go oferuje potężne narzędzia, które upraszczają te procesy, czyniąc je nie tylko efektywne, ale i przyjemne dla programistów.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com