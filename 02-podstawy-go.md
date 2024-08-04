### Podstawy GoLang

#### Historia i filozofia języka

GoLang, często nazywany Golang, został stworzony przez Roberta Griesemera, Roba Pike'a i Kena Thompsona w firmie Google. Język został zaprezentowany publicznie w 2009 roku, a jego pierwsza stabilna wersja, Go 1.0, została wydana w marcu 2012 roku. 

Twórcy języka mieli na celu rozwiązanie problemów związanych z wydajnością i skalowalnością, które napotykali w codziennej pracy z dużymi systemami programistycznymi. Czerpiąc z doświadczeń w pracy nad systemami operacyjnymi (takimi jak Unix i Plan 9), stworzyli język, który łączy wydajność i bezpieczeństwo kompilowanych języków, takich jak C i C++, z łatwością użycia języków dynamicznych, takich jak Python i Ruby.

**Filozofia GoLang** koncentruje się na kilku kluczowych zasadach:

1. **Prostota i minimalizm**: Składnia języka jest prosta i intuicyjna, co ułatwia naukę i pisanie czytelnego kodu. GoLang unika złożonych funkcji i wzorców, które mogą prowadzić do trudności w zrozumieniu i utrzymaniu kodu.
   
2. **Wydajność**: GoLang jest kompilowany do kodu maszynowego, co zapewnia wysoką wydajność. Jest to szczególnie ważne w kontekście dużych systemów rozproszonych i serwerów obsługujących wiele jednoczesnych połączeń.
   
3. **Współbieżność**: Język posiada wbudowaną obsługę współbieżności za pomocą gorutyn i kanałów, co umożliwia efektywne zarządzanie wieloma zadaniami jednocześnie.
   
4. **Bezpieczeństwo i niezawodność**: Typowanie statyczne oraz brak implicitnych konwersji typów zapewniają bezpieczeństwo typów i zmniejszają ryzyko błędów. 

5. **Szybka kompilacja**: Kompilator GoLang jest szybki, co sprawia, że cykle kompilacji i testowania są krótsze, co przyspiesza rozwój oprogramowania.

#### Instalacja i konfiguracja środowiska

Aby zacząć programować w GoLang, należy przeprowadzić instalację i konfigurację środowiska programistycznego. Poniżej znajdują się kroki niezbędne do uruchomienia GoLang na systemach operacyjnych Windows, macOS i Linux.

1. **Pobranie GoLang**:
   - Wejdź na oficjalną stronę GoLang: [golang.org](https://golang.org)
   - Przejdź do sekcji „Download” i wybierz odpowiednią wersję dla Twojego systemu operacyjnego.

2. **Instalacja na Windows**:
   - Pobierz instalator Windows (`.msi`).
   - Uruchom instalator i postępuj zgodnie z instrukcjami, aby zainstalować GoLang na swoim komputerze.
   - Po zakończeniu instalacji upewnij się, że ścieżka do folderu `bin` GoLang została dodana do zmiennej środowiskowej PATH.

3. **Instalacja na macOS**:
   - Pobierz archiwum tarball (`.tar.gz`).
   - Otwórz terminal i rozpakuj archiwum do `/usr/local`:
     ```sh
     sudo tar -C /usr/local -xzf go1.x.x.darwin-amd64.tar.gz
     ```
   - Dodaj ścieżkę GoLang do swojego pliku `~/.bash_profile` lub `~/.zshrc`:
     ```sh
     export PATH=$PATH:/usr/local/go/bin
     ```
   - Zrestartuj terminal, aby zmiany weszły w życie.

4. **Instalacja na Linux**:
   - Pobierz archiwum tarball (`.tar.gz`).
   - Otwórz terminal i rozpakuj archiwum do `/usr/local`:
     ```sh
     sudo tar -C /usr/local -xzf go1.x.x.linux-amd64.tar.gz
     ```
   - Dodaj ścieżkę GoLang do swojego pliku `~/.bashrc` lub `~/.zshrc`:
     ```sh
     export PATH=$PATH:/usr/local/go/bin
     ```
   - Zrestartuj terminal, aby zmiany weszły w życie.

5. **Konfiguracja środowiska**:
   - Upewnij się, że GoLang został zainstalowany poprawnie, uruchamiając w terminalu polecenie:
     ```sh
     go version
     ```
   - Skonfiguruj zmienne środowiskowe GoLang:
     - `GOPATH`: Ścieżka do katalogu, w którym będą przechowywane pakiety Go.
       ```sh
       export GOPATH=$HOME/go
       ```
     - `GOBIN`: Ścieżka do katalogu, w którym będą przechowywane pliki wykonywalne Go.
       ```sh
       export GOBIN=$GOPATH/bin
       ```
   - Dodaj te zmienne do pliku konfiguracyjnego powłoki (`~/.bashrc` lub `~/.zshrc`).

6. **Tworzenie pierwszego programu**:
   - Utwórz katalog dla swojego projektu:
     ```sh
     mkdir -p $GOPATH/src/hello
     ```
   - Przejdź do tego katalogu i utwórz plik `hello.go`:
     ```go
     package main

     import "fmt"

     func main() {
         fmt.Println("Hello, World!")
     }
     ```
   - Skompiluj i uruchom program:
     ```sh
     go run hello.go
     ```

Instalacja i konfiguracja środowiska GoLang jest stosunkowo prosta i szybka. Dzięki temu można szybko rozpocząć naukę i tworzenie aplikacji w tym wydajnym i nowoczesnym języku programowania.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com