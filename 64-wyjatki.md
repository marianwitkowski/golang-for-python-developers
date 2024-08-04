### Rozdział: Wyjątki w Go

W języku programowania Go, podejście do obsługi błędów i sytuacji wyjątkowych różni się od tego, co można znaleźć w wielu innych językach programowania. Go nie posiada tradycyjnego mechanizmu wyjątków, jakie znamy na przykład z Java czy C#. Zamiast tego, Go używa dwóch głównych mechanizmów: typu `error` do obsługi błędów oraz par `panic` i `recover` do obsługi błędów krytycznych i kontroli przepływu programu. W tym rozdziale szczegółowo omówimy oba te mechanizmy.

#### Typ `error`

1. **Podstawy typu `error`**:
   - W Go, `error` jest wbudowanym interfejsem, który reprezentuje błąd działania. Jest to podstawowy sposób na zgłaszanie i obsługę błędów w Go. Interfejs `error` definiowany jest bardzo prosto:
     ```go
     type error interface {
         Error() string
     }
     ```
   - Każdy typ, który implementuje metodę `Error() string`, automatycznie spełnia interfejs `error`, co pozwala na zgłaszanie błędów.

2. **Zwracanie błędów z funkcji**:
   - Funkcje, które mogą napotkać błąd podczas wykonania, zazwyczaj zwracają błąd jako ostatnią wartość w swojej liście zwracanych wartości. To pozwala użytkownikowi funkcji na sprawdzenie, czy wystąpił błąd.
     ```go
     func readFile(filename string) ([]byte, error) {
         data, err := ioutil.ReadFile(filename)
         if err != nil {
             return nil, err
         }
         return data, nil
     }
     ```

3. **Obsługa zwróconych błędów**:
   - Sprawdzenie i obsługa zwróconego błędu jest kluczowym aspektem pisania niezawodnego kodu w Go:
     ```go
     data, err := readFile("config.json")
     if err != nil {
         log.Fatalf("Error reading file: %s", err)
     }
     fmt.Println("File read successfully:", data)
     ```

4. **Tworzenie niestandardowych błędów**:
   - Go umożliwia łatwe tworzenie niestandardowych błędów poprzez `errors.New` lub definiowanie typów, które implementują `error`.
     ```go
     import "errors"

     var ErrFileNotFound = errors.New("file not found")

     func openFile(name string) error {
         return ErrFileNotFound
     }
     ```

#### Panic i Recover

1. **Mechanizm `panic`**:
   - `Panic` jest funkcją wbudowaną w Go, która zatrzymuje normalne wykonanie bieżącej funkcji i zaczyna "windać" stos, aż do momentu, gdy zostanie przechwycona przez `recover` lub program zakończy działanie.
     ```go
     func processData(data []int) {
         if len(data) == 0 {
             panic("data cannot be empty")
         }
         // przetwarzanie danych
     }
     ```

2. **Używanie `recover`**:
   - `Recover` jest funkcją, która regeneruje kontrolę nad programem po `panic`. `Recover` musi być wywołane w tej samej gorutynie co `panic`, zwykle wewnątrz opóźnionej funkcji (`defer`).
     ```go
     func safeProcess() {
         defer func() {
             if r := recover(); r != nil {
                 fmt.Println("Recovered in safeProcess:", r)
             }
         }()
         processData([]int{})
     }
     ```

3. **Kiedy używać `panic` i `recover`**:
   - Użycie `panic` i `recover` zaleca się ograniczyć do sytuacji, gdy program napotyka błędy, których nie można obsłużyć w sposób konwencjonalny, lub gdy chcemy zabezpieczyć program przed awarią w wyniku nieprzewidzianych błędów.

#### Podsumowanie

Rozumienie i efektywne wykorzystanie typu `error` oraz mechanizmów `panic` i `recover` w Go jest kluczowe dla pisania odpornego i bezpiecznego kodu. Zarządzanie błędami w Go poprzez te mechanizmy umożliwia tworzenie aplikacji, które mogą skutecznie radzić sobie z nieoczekiwanymi i krytycznymi sytuacjami, zapewniając jednocześnie, że błędy są obsługiwane w przemyślany i kontrolowany sposób.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com