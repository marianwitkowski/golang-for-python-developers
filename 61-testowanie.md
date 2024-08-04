### Testowanie

Testowanie oprogramowania jest nieodłącznym elementem rozwoju aplikacji, które pozwala na zapewnienie jakości i stabilności oprogramowania przed jego wdrożeniem. W ekosystemie Go, szczególnie istotne jest wykorzystanie testów jednostkowych, które pozwalają na systematyczną weryfikację działania poszczególnych części programu. Ten rozdział poświęcony jest pisanym testom jednostkowym w Go, ze szczególnym uwzględnieniem pakietu `testing`.

#### Pisanie testów jednostkowych

Testy jednostkowe to testy, które koncentrują się na pojedynczych funkcjach lub metodach - najmniejszych testowalnych częściach aplikacji. W Go, mechanizm testowania jest głęboko zintegrowany z językiem i oferowany jest przez standardowy pakiet `testing`. Pozwala on na łatwe tworzenie i uruchamianie testów.

1. **Struktura testów jednostkowych w Go**:
   - Każdy test jednostkowy w Go powinien być zapisany w pliku o nazwie zakończonej `_test.go`.
   - Testy pisze się jako funkcje o nazwach zaczynających się od `Test` z argumentem `*testing.T`. To właśnie ten argument pozwala na kontrolowanie przebiegu testu.

   ```go
   package mypackage

   import "testing"

   func TestSum(t *testing.T) {
       total := Sum(5, 5)
       if total != 10 {
           t.Errorf("Sum was incorrect, got: %d, want: %d.", total, 10)
       }
   }
   ```

   W powyższym przykładzie, `TestSum` jest testem jednostkowym dla funkcji `Sum`. Test sprawdza, czy wynik funkcji jest zgodny z oczekiwaniami. Jeśli wynik się nie zgadza, test zgłasza błąd za pomocą `t.Errorf`.

2. **Uruchamianie testów**:
   - Testy jednostkowe można uruchomić za pomocą narzędzia wiersza poleceń `go test`. Narzędzie to automatycznie wykrywa wszystkie pliki z testami w katalogu, kompiluje pakiet wraz z testami i wykonuje testy.
   ```bash
   go test
   ```

   Wywołanie `go test` w katalogu projektu uruchomi wszystkie testy jednostkowe w tym katalogu, a wyniki zostaną wyświetlone w terminalu.

#### Używanie pakietu `testing`

Pakiet `testing` dostarcza nie tylko framework do tworzenia testów jednostkowych, ale również narzędzia do dokładniejszego monitorowania i kontroli ich wykonania.

1. **Aserty i logowanie w testach**:
   - `t.Log()` i `t.Logf()` pozwalają na logowanie informacji, które mogą być pomocne podczas diagnozowania problemów, gdy testy nie przechodzą.
   - `t.Fail()`, `t.Errorf()`, `t.Fatalf()` to metody pozwalające zasygnalizować niepowodzenie testu w różnych scenariuszach.

   ```go
   func TestDivide(t *testing.T) {
       _, err := Divide(10, 0)
       if err == nil {
           t.Errorf("Expected an error for division by zero")
       }
   }
   ```

2. **Testy tabelaryczne**:
   - Często stosowaną techniką w testowaniu jednostkowym jest użycie testów tabelarycznych, gdzie testy są uruchamiane wielokrotnie z różnymi zestawami danych.
   ```go
   func TestMultiply(t *testing.T) {
       var tests = []struct {
           a, b, expected int
       }{
           {1, 2, 2},
           {2, 2, 4},
           {3, 2, 6},
       }

       for _, tt := range tests {
           testname := fmt.Sprintf("%d,%d", tt.a, tt.b)
           t.Run(testname, func(t *testing.T) {
               ans := Multiply(tt.a, tt.b)
               if ans != tt.expected {
                   t.Errorf("got %d, want %d", ans, tt.expected)
               }
           })
       }
   }
   ```

#### Podsumowanie

Pisanie skutecznych testów jednostkowych w Go jest fundamentalnym elementem zapewnienia jakości kodu. Pakiet `testing` jest potężnym narzędziem, które ułatwia pisanie, organizację i wykonanie testów. Wykorzystując te techniki, programiści mogą skutecznie testować i weryfikować każdą funkcjonalność swojego oprogramowania, co prowadzi do tworzenia bardziej niezawodnych i utrzymywalnych systemów. Dobre praktyki testowania i ciągła integracja są kluczem do sukcesu w każdym projekcie programistycznym, a Go oferuje wszystkie narzędzia niezbędne do ich realizacji.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com