### Aplikacja bazodanowa

Tworzenie aplikacji bazodanowej w Go obejmuje integrację z różnymi systemami baz danych, zarówno relacyjnymi (takimi jak MySQL), jak i nierelacyjnymi (takimi jak MongoDB). W tym rozdziale omówimy, jak zintegrować aplikację Go z relacyjną bazą danych MySQL w celu wykonania operacji CRUD (Create, Read, Update, Delete), a także jak korzystać z bazy danych NoSQL, takiej jak MongoDB.

#### Integracja z relacyjną bazą danych MySQL

MySQL jest jednym z najpopularniejszych systemów zarządzania relacyjnymi bazami danych (RDBMS). Język Go oferuje wsparcie dla MySQL poprzez kilka bibliotek, z których jedną z najbardziej popularnych jest `go-sql-driver/mysql`.

##### Instalacja i konfiguracja

Aby rozpocząć, należy zainstalować pakiet MySQL:

```bash
go get -u github.com/go-sql-driver/mysql
```

##### Konfiguracja połączenia z bazą danych

Następnie, skonfigurujemy połączenie z bazą danych w naszym kodzie Go:

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

func main() {
    dsn := "user:password@tcp(127.0.0.1:3306)/dbname"
    db, err := sql.Open("mysql", dsn)
    if err != nil {
        fmt.Println("Error connecting to the database:", err)
        return
    }
    defer db.Close()

    err = db.Ping()
    if err != nil {
        fmt.Println("Error pinging the database:", err)
        return
    }
    fmt.Println("Successfully connected to the database.")
}
```

##### Operacje CRUD

###### Create (Tworzenie)

Aby dodać nowy rekord do bazy danych, używamy metody `Exec`:

```go
func createUser(db *sql.DB, name string, age int) {
    query := "INSERT INTO users (name, age) VALUES (?, ?)"
    _, err := db.Exec(query, name, age)
    if err != nil {
        fmt.Println("Error creating user:", err)
        return
    }
    fmt.Println("User created successfully.")
}
```

###### Read (Odczyt)

Aby odczytać dane z bazy danych, używamy metody `Query` lub `QueryRow`:

```go
func getUser(db *sql.DB, userID int) {
    query := "SELECT id, name, age FROM users WHERE id = ?"
    row := db.QueryRow(query, userID)

    var id int
    var name string
    var age int
    err := row.Scan(&id, &name, &age)
    if err != nil {
        if err == sql.ErrNoRows {
            fmt.Println("No user found with the given ID.")
        } else {
            fmt.Println("Error fetching user:", err)
        }
        return
    }
    fmt.Printf("User: %d, Name: %s, Age: %d\n", id, name, age)
}
```

###### Update (Aktualizacja)

Aby zaktualizować istniejący rekord, również używamy metody `Exec`:

```go
func updateUser(db *sql.DB, userID int, newName string, newAge int) {
    query := "UPDATE users SET name = ?, age = ? WHERE id = ?"
    _, err := db.Exec(query, newName, newAge, userID)
    if err != nil {
        fmt.Println("Error updating user:", err)
        return
    }
    fmt.Println("User updated successfully.")
}
```

###### Delete (Usuwanie)

Aby usunąć rekord z bazy danych, ponownie używamy metody `Exec`:

```go
func deleteUser(db *sql.DB, userID int) {
    query := "DELETE FROM users WHERE id = ?"
    _, err := db.Exec(query, userID)
    if err != nil {
        fmt.Println("Error deleting user:", err)
        return
    }
    fmt.Println("User deleted successfully.")
}
```

#### Korzystanie z bazy danych NoSQL (MongoDB)

MongoDB jest popularnym systemem zarządzania bazą danych NoSQL, który przechowuje dane w formie dokumentów JSON. Aby zintegrować Go z MongoDB, można użyć pakietu `mongo-go-driver`.

##### Instalacja i konfiguracja

Aby zainstalować pakiet MongoDB dla Go, użyjemy komendy:

```bash
go get go.mongodb.org/mongo-driver/mongo
```

##### Konfiguracja połączenia z bazą danych

Następnie, skonfigurujemy połączenie z bazą danych MongoDB:

```go
package main

import (
    "context"
    "fmt"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
    "time"
)

func main() {
    clientOptions := options.Client().ApplyURI("mongodb://localhost:27017")
    client, err := mongo.NewClient(clientOptions)
    if err != nil {
        fmt.Println("Error creating MongoDB client:", err)
        return
    }

    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()

    err = client.Connect(ctx)
    if err != nil {
        fmt.Println("Error connecting to MongoDB:", err)
        return
    }
    defer client.Disconnect(ctx)

    fmt.Println("Successfully connected to MongoDB.")
}
```

##### Operacje CRUD

###### Create (Tworzenie)

Aby dodać nowy dokument do kolekcji, używamy metody `InsertOne`:

```go
func createUser(client *mongo.Client, name string, age int) {
    collection := client.Database("dbname").Collection("users")
    user := bson.D{{"name", name}, {"age", age}}
    _, err := collection.InsertOne(context.Background(), user)
    if err != nil {
        fmt.Println("Error creating user:", err)
        return
    }
    fmt.Println("User created successfully.")
}
```

###### Read (Odczyt)

Aby odczytać dane z MongoDB, używamy metody `FindOne`:

```go
func getUser(client *mongo.Client, userID string) {
    collection := client.Database("dbname").Collection("users")
    filter := bson.D{{"id", userID}}

    var result bson.D
    err := collection.FindOne(context.Background(), filter).Decode(&result)
    if err != nil {
        if err == mongo.ErrNoDocuments {
            fmt.Println("No user found with the given ID.")
        } else {
            fmt.Println("Error fetching user:", err)
        }
        return
    }
    fmt.Println("User:", result)
}
```

###### Update (Aktualizacja)

Aby zaktualizować istniejący dokument, używamy metody `UpdateOne`:

```go
func updateUser(client *mongo.Client, userID string, newName string, newAge int) {
    collection := client.Database("dbname").Collection("users")
    filter := bson.D{{"id", userID}}
    update := bson.D{
        {"$set", bson.D{
            {"name", newName},
            {"age", newAge},
        }},
    }
    _, err := collection.UpdateOne(context.Background(), filter, update)
    if err != nil {
        fmt.Println("Error updating user:", err)
        return
    }
    fmt.Println("User updated successfully.")
}
```

###### Delete (Usuwanie)

Aby usunąć dokument z MongoDB, używamy metody `DeleteOne`:

```go
func deleteUser(client *mongo.Client, userID string) {
    collection := client.Database("dbname").Collection("users")
    filter := bson.D{{"id", userID}}
    _, err := collection.DeleteOne(context.Background(), filter)
    if err != nil {
        fmt.Println("Error deleting user:", err)
        return
    }
    fmt.Println("User deleted successfully.")
}
```

#### Podsumowanie

Tworzenie aplikacji bazodanowej w Go z integracją z relacyjnymi bazami danych, takimi jak MySQL, oraz bazami danych NoSQL, takimi jak MongoDB, jest prostym procesem dzięki bogatemu ekosystemowi bibliotek dostępnych w Go. Wykonywanie operacji CRUD w obu typach baz danych umożliwia programistom tworzenie skalowalnych i elastycznych aplikacji, które mogą przechowywać i przetwarzać dane w sposób efektywny.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com