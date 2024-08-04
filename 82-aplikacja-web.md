### Rozdział: Aplikacja Webowa

#### Prosty serwer webowy realizujący funkcjonalność REST API

Tworzenie REST API to podstawowy sposób, w jaki nowoczesne aplikacje webowe komunikują się z klientami, takimi jak aplikacje mobilne, strony internetowe, lub inne usługi. W Go, prosty serwer webowy można skonfigurować przy użyciu standardowego pakietu `net/http`, który zapewnia niezbędne narzędzia do obsługi żądań HTTP.

##### 1. Podstawy REST API

REST API (Representational State Transfer Application Programming Interface) pozwala na interakcje z aplikacjami poprzez standardowe metody HTTP takie jak GET, POST, PUT, DELETE. Każda metoda odpowiada za inną operację na zasobach serwera, co ułatwia budowę skalowalnych i łatwych w utrzymaniu systemów.

##### 2. Konfiguracja serwera HTTP w Go

Implementacja serwera REST w Go rozpoczyna się od ustawienia routera, który kieruje żądania do odpowiednich handlerów funkcji. Poniżej znajduje się przykład prostego serwera:

```go
package main

import (
    "encoding/json"
    "log"
    "net/http"
)

type Product struct {
    ID    int    `json:"id"`
    Name  string `json:"name"`
    Price float64 `json:"price"`
}

var products = []Product{
    {ID: 1, Name: "Tea", Price: 1.99},
    {ID: 2, Name: "Coffee", Price: 2.49},
}

func getProducts(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "application/json")
    json.NewEncoder(w).Encode(products)
}

func main() {
    http.HandleFunc("/products", getProducts)
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

W powyższym kodzie, serwer obsługuje ścieżkę `/products`, zwracając listę produktów w formacie JSON. Użycie typu `Product` pozwala na łatwe zarządzanie i rozbudowę danych produktów.

#### Klient umożliwiający pobieranie danych z REST API

Aplikacja kliencka, która komunikuje się z REST API, może być wykonana w dowolnym języku programowania, który obsługuje żądania HTTP. W Go, klient wykorzystujący API mogłby wyglądać następująco:

##### 1. Tworzenie klienta HTTP

Klient HTTP w Go może łatwo wysyłać żądania do serwera API i interpretować odpowiedzi:

```go
package main

import (
    "encoding/json"
    "fmt"
    "net/http"
)

func main() {
    resp, err := http.Get("http://localhost:8080/products")
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    defer resp.Body.Close()

    var products []Product
    if err := json.NewDecoder(resp.Body).Decode(&products); err != nil {
        fmt.Println("Error decoding response data:", err)
        return
    }

    fmt.Println("Products:", products)
}
```

W tym przykładzie, klient wysyła żądanie GET do serwera, aby pobrać listę produktów. Odpowiedź jest następnie deserializowana z JSON na slice struktur `Product`.

#### Podsumowanie

Tworzenie aplikacji webowej z REST API w Go wymaga zrozumienia zarówno konstrukcji serwera, jak i klienta. Go zapewnia wydajne i proste narzędzia, które umożliwiają szybką implementację zarówno serwera, jak i klienta API. Używanie standardowego pakietu `net/http` dla serwera i klienta pozwala na szybką rozbudowę aplikacji oraz integrację z innymi usługami i systemami. Staranne planowanie, implementacja i testowanie są kluczowe dla budowy bezpiecznych, wydajnych i łatwych w utrzymaniu aplikacji webowych opartych na architekturze REST.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com