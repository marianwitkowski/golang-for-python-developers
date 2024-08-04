### Logowanie

#### Praktyki logowania w Go

Logowanie jest kluczowym elementem każdej aplikacji, umożliwiającym monitorowanie jej działania, diagnozowanie problemów i zbieranie informacji na temat użytkowania. W języku Go istnieje wiele technik i najlepszych praktyk dotyczących logowania, które mogą pomóc w tworzeniu bardziej niezawodnych i łatwych w utrzymaniu aplikacji.

##### Dlaczego logowanie jest ważne?

Logowanie dostarcza cennych informacji o działaniu aplikacji w czasie rzeczywistym. Pozwala na:

1. **Monitorowanie**: Śledzenie stanu aplikacji i jej wydajności.
2. **Diagnozowanie problemów**: Identyfikacja i rozwiązywanie błędów oraz problemów.
3. **Bezpieczeństwo**: Rejestrowanie prób nieautoryzowanego dostępu i innych zdarzeń związanych z bezpieczeństwem.
4. **Zarządzanie**: Analiza użycia aplikacji przez użytkowników i optymalizacja jej działania.

##### Najlepsze praktyki logowania

1. **Używanie poziomów logowania**: Dobre praktyki logowania obejmują użycie różnych poziomów logowania, takich jak `DEBUG`, `INFO`, `WARNING`, `ERROR`, i `FATAL`. Pozwala to na filtrowanie logów i skupienie się na najbardziej istotnych informacjach.

2. **Formatowanie logów**: Logi powinny być czytelne i zawierać niezbędne informacje, takie jak znaczniki czasu, poziomy logowania, identyfikatory wątków i szczegóły zdarzeń.

3. **Logowanie błędów z pełnymi śladami stosu (stack traces)**: W przypadku błędów, logi powinny zawierać pełne ślady stosu, aby ułatwić diagnozowanie problemów.

4. **Unikanie nadmiernego logowania**: Zbyt wiele logów może utrudnić znalezienie istotnych informacji i wpłynąć na wydajność aplikacji. Należy znaleźć odpowiednią równowagę.

5. **Bezpieczne logowanie**: Nigdy nie loguj poufnych informacji, takich jak hasła czy dane osobowe. Upewnij się, że logi są zgodne z przepisami dotyczącymi ochrony danych.

6. **Rotacja i archiwizacja logów**: Logi powinny być rotowane i archiwizowane, aby zapobiec zapełnieniu dysku i utracie danych. Używanie narzędzi do zarządzania logami, takich jak `logrotate`, może być pomocne.

7. **Testowanie logowania**: Regularnie testuj logowanie, aby upewnić się, że wszystkie istotne zdarzenia są rejestrowane, a logi są czytelne i zawierają niezbędne informacje.

### Przegląd bibliotek logowania w Go

W ekosystemie Go istnieje wiele bibliotek logowania, które ułatwiają implementację logowania w aplikacjach. Poniżej omówimy najpopularniejsze z nich:

#### 1. Log

`log` to standardowa biblioteka logowania w Go, która jest łatwa w użyciu i nie wymaga dodatkowych zależności. Oferuje podstawowe funkcje logowania, takie jak logowanie wiadomości, błędów oraz fatalnych błędów, które kończą działanie programu.

```go
package main

import (
    "log"
)

func main() {
    log.Println("This is a regular log message")
    log.Fatal("This is a fatal error message")
}
```

#### 2. Logrus

`Logrus` to zaawansowana biblioteka logowania, która oferuje wiele dodatkowych funkcji, takich jak kolorowe logowanie, strukturalne logi i wsparcie dla różnych poziomów logowania.

```go
package main

import (
    log "github.com/sirupsen/logrus"
)

func main() {
    log.SetFormatter(&log.JSONFormatter{})

    log.WithFields(log.Fields{
        "animal": "walrus",
        "number": 1,
    }).Info("A walrus appears")
}
```

#### 3. Zap

`Zap` to biblioteka logowania stworzona przez Ubera, która jest zoptymalizowana pod kątem wydajności. Oferuje szybkie i strukturalne logowanie.

```go
package main

import (
    "go.uber.org/zap"
)

func main() {
    logger, _ := zap.NewProduction()
    defer logger.Sync()

    logger.Info("This is an info message",
        zap.String("category", "example"),
        zap.Int("attempt", 3),
    )
}
```

#### 4. Zerolog

`Zerolog` to kolejna wydajna biblioteka logowania, która kładzie duży nacisk na szybkie i niskopoziomowe logowanie. Jest idealna do aplikacji, które wymagają wysokiej wydajności.

```go
package main

import (
    "github.com/rs/zerolog"
    "os"
)

func main() {
    logger := zerolog.New(os.Stdout).With().Timestamp().Logger()

    logger.Info().Msg("This is an info message")
    logger.Error().Err(err).Msg("This is an error message")
}
```

#### 5. Go-kit

`Go-kit` to biblioteka oferująca zestaw narzędzi do tworzenia mikroserwisów w Go, w tym funkcje logowania. Jest bardziej rozbudowana i zawiera wsparcie dla logowania w kontekście mikroserwisów.

```go
package main

import (
    "github.com/go-kit/kit/log"
    "os"
)

func main() {
    logger := log.NewLogfmtLogger(os.Stderr)

    logger.Log("msg", "This is a log message")
}
```

### Wybór odpowiedniej biblioteki

Wybór odpowiedniej biblioteki logowania zależy od specyficznych potrzeb projektu. Oto kilka wskazówek, które mogą pomóc w podjęciu decyzji:

- **Prostota**: Jeśli potrzebujesz prostego logowania bez dodatkowych funkcji, standardowa biblioteka `log` może być wystarczająca.
- **Wydajność**: Jeśli wydajność jest kluczowa, rozważ użycie bibliotek takich jak `Zap` lub `Zerolog`.
- **Strukturalne logowanie**: Jeśli chcesz logować strukturalne dane, `Logrus`, `Zap` i `Zerolog` oferują wsparcie dla takiego logowania.
- **Kolorowe logowanie**: Jeśli chcesz, aby logi były łatwiejsze do czytania dzięki kolorowym komunikatom, `Logrus` może być dobrym wyborem.
- **Mikroserwisy**: Jeśli tworzysz mikroserwisy, `Go-kit` oferuje wsparcie dla logowania w kontekście rozproszonych aplikacji.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com