### Narzędzia i biblioteki

#### Przegląd przydatnych narzędzi i bibliotek w ekosystemie Go

Ekosystem Go jest bogaty w narzędzia i biblioteki, które ułatwiają programowanie i zarządzanie projektami. Dzięki nim można znacząco zwiększyć efektywność pracy oraz jakość kodu. Poniżej znajduje się szczegółowy przegląd najważniejszych narzędzi i bibliotek, które warto znać.

### Narzędzia

#### 1. Go Modules

Go Modules to system zarządzania zależnościami w Go, który zastąpił wcześniejsze narzędzia takie jak `GOPATH` i `dep`. Pozwala on na łatwe zarządzanie wersjami bibliotek i izolację zależności dla poszczególnych projektów.

- **Inicjalizacja modułu**: `go mod init <module-name>`
- **Pobieranie zależności**: `go mod tidy`
- **Aktualizacja zależności**: `go get -u <module-name>`

Go Modules są kluczowe dla nowoczesnego zarządzania zależnościami i wersjami w projektach Go.

#### 2. GoLand

GoLand to zintegrowane środowisko programistyczne (IDE) stworzone przez JetBrains, specjalnie zaprojektowane dla programistów Go. Oferuje wiele funkcji ułatwiających programowanie, takich jak automatyczne uzupełnianie kodu, refaktoryzacja, debugowanie i integracja z systemami kontroli wersji.

#### 3. Visual Studio Code (VS Code)

VS Code to popularne, darmowe edytor tekstu od Microsoftu, który dzięki rozszerzeniom (takim jak Go extension) staje się potężnym narzędziem do programowania w Go. Oferuje funkcje takie jak podpowiedzi kodu, refaktoryzacja, debugowanie i wiele innych.

#### 4. Delve

Delve to potężne narzędzie do debugowania w Go. Pozwala na przeglądanie stanu programu, ustalanie punktów przerwań (breakpoints), śledzenie wartości zmiennych i wiele więcej.

- **Instalacja**: `go get -u github.com/go-delve/delve/cmd/dlv`
- **Uruchomienie**: `dlv debug`

#### 5. Gofmt

Gofmt to narzędzie do formatowania kodu Go zgodnie z oficjalnymi standardami stylu. Jest to niezbędne narzędzie do utrzymania spójności kodu w projektach zespołowych.

- **Użycie**: `gofmt -w .`

#### 6. Go Vet

Go Vet to narzędzie do analizy statycznej kodu Go, które wykrywa potencjalne błędy i problemy w kodzie. Jest to kluczowe narzędzie do zapewnienia jakości kodu.

- **Użycie**: `go vet ./...`

#### 7. Golint

Golint to narzędzie do analizy statycznej, które sprawdza zgodność kodu Go z zaleceniami stylu i najlepszymi praktykami.

- **Instalacja**: `go get -u golang.org/x/lint/golint`
- **Użycie**: `golint ./...`

#### 8. GoDoc

GoDoc to narzędzie do generowania dokumentacji dla pakietów Go. Umożliwia automatyczne tworzenie dokumentacji na podstawie komentarzy w kodzie źródłowym.

- **Użycie**: `godoc -http=:6060`

#### 9. Mockgen

Mockgen to narzędzie do generowania mocków dla interfejsów Go, co jest szczególnie przydatne podczas testowania jednostkowego.

- **Instalacja**: `go get -u github.com/golang/mock/mockgen`
- **Użycie**: `mockgen -source=your_source.go -destination=your_mock.go -package=your_package`

#### 10. Benchstat

Benchstat to narzędzie do analizy wyników testów wydajnościowych w Go. Pozwala na porównanie wyników testów i identyfikację regresji wydajności.

- **Instalacja**: `go get -u golang.org/x/perf/cmd/benchstat`
- **Użycie**: `benchstat old.txt new.txt`

### Biblioteki

#### 1. Gin

Gin to wysokowydajny framework webowy dla Go, który ułatwia tworzenie serwisów webowych. Oferuje takie funkcje jak routing, middleware, obsługa JSON i wiele innych.

- **Instalacja**: `go get -u github.com/gin-gonic/gin`

```go
package main

import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })
    r.Run() // listen and serve on 0.0.0.0:8080
}
```

#### 2. Echo

Echo to kolejny popularny framework webowy dla Go, znany z wysokiej wydajności i prostoty użycia.

- **Instalacja**: `go get -u github.com/labstack/echo/v4`

```go
package main

import (
    "net/http"
    "github.com/labstack/echo/v4"
)

func main() {
    e := echo.New()
    e.GET("/", func(c echo.Context) error {
        return c.String(http.StatusOK, "Hello, World!")
    })
    e.Start(":1323")
}
```

#### 3. Gorm

Gorm to ORM (Object-Relational Mapping) dla Go, który upraszcza pracę z bazami danych poprzez mapowanie struktur Go na tabele w bazach danych.

- **Instalacja**: `go get -u gorm.io/gorm`

```go
package main

import (
    "gorm.io/driver/sqlite"
    "gorm.io/gorm"
)

type Product struct {
    gorm.Model
    Code  string
    Price uint
}

func main() {
    db, _ := gorm.Open(sqlite.Open("test.db"), &gorm.Config{})
    db.AutoMigrate(&Product{})
    db.Create(&Product{Code: "D42", Price: 100})
}
```

#### 4. Cobra

Cobra to biblioteka do tworzenia aplikacji CLI (Command Line Interface) w Go. Jest często używana w połączeniu z Viperem do zarządzania konfiguracjami.

- **Instalacja**: `go get -u github.com/spf13/cobra`

```go
package main

import (
    "fmt"
    "github.com/spf13/cobra"
)

func main() {
    var rootCmd = &cobra.Command{Use: "app"}
    rootCmd.AddCommand(&cobra.Command{
        Use:   "hello",
        Short: "Prints Hello, World!",
        Run: func(cmd *cobra.Command, args []string) {
            fmt.Println("Hello, World!")
        },
    })
    rootCmd.Execute()
}
```

#### 5. Viper

Viper to elastyczna biblioteka do zarządzania konfiguracjami w Go, która obsługuje wiele formatów plików konfiguracyjnych, zmienne środowiskowe, flagi CLI i wiele innych.

- **Instalacja**: `go get -u github.com/spf13/viper`

```go
package main

import (
    "fmt"
    "github.com/spf13/viper"
)

func main() {
    viper.SetConfigName("config")
    viper.AddConfigPath(".")
    viper.ReadInConfig()

    fmt.Println("App Name:", viper.GetString("app.name"))
}
```

#### 6. Mux

Mux to wydajny router HTTP dla Go, który oferuje zaawansowane funkcje routingu, takie jak obsługa zmiennych ścieżek i middleware.

- **Instalacja**: `go get -u github.com/gorilla/mux`

```go
package main

import (
    "net/http"
    "github.com/gorilla/mux"
)

func main() {
    r := mux.NewRouter()
    r.HandleFunc("/", HomeHandler)
    http.ListenAndServe(":8080", r)
}

func HomeHandler(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("Hello, world!"))
}
```

#### 7. Chi

Chi to inny popularny router HTTP dla Go, który jest lekki i wydajny, idealny do budowania serwisów API.

- **Instalacja**: `go get -u github.com/go-chi/chi/v5`

```go
package main

import (
    "net/http"
    "github.com/go-chi/chi/v5"
)

func main() {
    r := chi.NewRouter()
    r.Get("/", func(w http.ResponseWriter, r *http.Request) {
        w.Write([]byte("Hello, world!"))
    })
    
    r.Get("/users/{userID}", func(w http.ResponseWriter, r *http.Request) {
        userID := chi.URLParam(r, "userID")
        w.Write([]byte("User ID: " + userID))
    })

    r.Post("/users", func(w http.ResponseWriter, r *http.Request) {
        w.Write([]byte("Create a new user"))
    })

    http.ListenAndServe(":8080", r)
}
```

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com