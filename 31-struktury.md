### Struktury

Struktury w GoLang są podstawowym elementem umożliwiającym definiowanie własnych typów danych. Dzięki nim można tworzyć złożone typy danych, które grupują pola o różnych typach. Struktury są często używane do modelowania rzeczywistych obiektów i ich właściwości. Omówimy teraz, jak definiować struktury, jak korzystać z metod i odbiorników, a także porównamy te mechanizmy z ich odpowiednikami w Pythonie.

#### Definiowanie struktur

Struktury w GoLang są definiowane przy użyciu słowa kluczowego `struct`, po którym następuje lista pól, z których każde ma nazwę i typ.

1. **Podstawowa definicja struktury**:
   - Składnia:
     ```go
     type StructName struct {
         field1 type1
         field2 type2
         // więcej pól
     }
     ```
   - Przykład:
     ```go
     type Person struct {
         Name string
         Age  int
     }
     ```

   W powyższym przykładzie zdefiniowano strukturę `Person`, która ma dwa pola: `Name` typu `string` i `Age` typu `int`.

2. **Tworzenie instancji struktury**:
   - Tworzenie nowej instancji struktury jest proste i odbywa się poprzez przypisanie wartości do pól.
   - Przykład:
     ```go
     p := Person{Name: "Alice", Age: 30}
     fmt.Println(p.Name) // Wyjście: Alice
     fmt.Println(p.Age)  // Wyjście: 30
     ```

   W powyższym przykładzie utworzono nową instancję `Person` i przypisano wartości do pól `Name` i `Age`.

3. **Domyślne wartości pól**:
   - Jeśli nie przypiszemy wartości do wszystkich pól struktury, GoLang użyje domyślnych wartości dla tych typów.
   - Przykład:
     ```go
     p := Person{Name: "Bob"}
     fmt.Println(p.Name) // Wyjście: Bob
     fmt.Println(p.Age)  // Wyjście: 0
     ```

   W powyższym przykładzie pole `Age` nie zostało zainicjalizowane, więc przyjęło domyślną wartość `0` dla typu `int`.

#### Metody i odbiorniki

Metody w GoLang są funkcjami, które mogą być przypisane do typów, w tym do struktur. Dzięki metodom struktury mogą mieć zdefiniowane zachowania, co czyni je bardziej użytecznymi i zbliżonymi do obiektów w językach obiektowo zorientowanych.

1. **Definiowanie metod**:
   - Metoda jest definiowana jak funkcja, ale z dodatkowym argumentem odbiornika między słowem kluczowym `func` a nazwą funkcji.
   - Składnia:
     ```go
     func (receiverType receiverName) methodName(parameters) returnType {
         // ciało metody
     }
     ```
   - Przykład:
     ```go
     func (p Person) Greet() string {
         return "Hello, " + p.Name
     }

     func main() {
         p := Person{Name: "Alice", Age: 30}
         fmt.Println(p.Greet()) // Wyjście: Hello, Alice
     }
     ```

   W powyższym przykładzie zdefiniowano metodę `Greet` dla struktury `Person`, która zwraca powitanie zawierające imię osoby.

2. **Odbiorniki wartość vs wskaźnik**:
   - Odbiorniki mogą być definiowane jako wartości lub wskaźniki, co wpływa na sposób przekazywania struktury do metody.
   - Przykład odbiornika wartości:
     ```go
     func (p Person) GetAge() int {
         return p.Age
     }
     ```
   - Przykład odbiornika wskaźnika:
     ```go
     func (p *Person) HaveBirthday() {
         p.Age++
     }

     func main() {
         p := Person{Name: "Alice", Age: 30}
         p.HaveBirthday()
         fmt.Println(p.Age) // Wyjście: 31
     }
     ```

   W powyższym przykładzie metoda `HaveBirthday` używa odbiornika wskaźnika `*Person`, co umożliwia modyfikację pola `Age` w oryginalnej strukturze.

#### Podobieństwa i różnice w stosunku do Pythona

Porównując GoLang z Pythonem, możemy zauważyć kilka kluczowych różnic i podobieństw w sposobie definiowania i używania struktur oraz metod.

1. **Definiowanie struktur vs klasy**:
   - W GoLang struktury (`struct`) są podstawowym sposobem definiowania złożonych typów danych.
   - W Pythonie klasy (`class`) pełnią podobną rolę, ale są bardziej wszechstronne, ponieważ wspierają dziedziczenie i polimorfizm.

   Przykład klasy w Pythonie:
   ```python
   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age

       def greet(self):
           return f"Hello, {self.name}"

   p = Person("Alice", 30)
   print(p.greet())  # Wyjście: Hello, Alice
   ```

2. **Metody i odbiorniki**:
   - W GoLang metody są funkcjami, które mają odbiornik (`receiver`), którym może być wartość lub wskaźnik.
   - W Pythonie metody są zdefiniowane wewnątrz klasy i zawsze mają jako pierwszy parametr `self`, który odnosi się do instancji klasy.

   Przykład metody w Pythonie:
   ```python
   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age

       def have_birthday(self):
           self.age += 1

   p = Person("Alice", 30)
   p.have_birthday()
   print(p.age)  # Wyjście: 31
   ```

3. **Zasięg i modyfikacja pól**:
   - W GoLang używając wskaźników, można bezpośrednio modyfikować pola struktury w metodach.
   - W Pythonie modyfikacja pól odbywa się bezpośrednio za pomocą `self`.

4. **Brak dziedziczenia w GoLang**:
   - GoLang nie wspiera dziedziczenia w tradycyjnym sensie, co odróżnia go od Pythona. Zamiast tego, GoLang wspiera kompozycję, która pozwala na tworzenie złożonych typów przez łączenie prostszych.

   Przykład kompozycji w GoLang:
   ```go
   type Address struct {
       City, State string
   }

   type Person struct {
       Name string
       Age  int
       Address
   }

   func main() {
       p := Person{Name: "Alice", Age: 30, Address: Address{City: "New York", State: "NY"}}
       fmt.Println(p.City)  // Wyjście: New York
   }
   ```

#### Podsumowanie

Struktury w GoLang są potężnym narzędziem do tworzenia złożonych typów danych, które grupują różne pola w jedną całość. Metody i odbiorniki umożliwiają definiowanie zachowań dla tych struktur, co zbliża GoLang do języków obiektowo zorientowanych, takich jak Python. Mimo że GoLang nie wspiera dziedziczenia, kompozycja umożliwia tworzenie złożonych struktur w sposób modułowy i elastyczny. Zrozumienie i umiejętne wykorzystanie struktur i metod w GoLang jest kluczowe dla efektywnego programowania w tym języku.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com