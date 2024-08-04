### Praca z systemem plików

Zarządzanie plikami i katalogami jest kluczową częścią większości aplikacji. Go oferuje bogaty zestaw narzędzi w bibliotece standardowej, który pozwala na efektywne otwieranie, czytanie, zapisywanie i manipulowanie plikami. Ten rozdział przybliży, jak te operacje są realizowane w Go, dostarczając przykłady użycia i wskazówki najlepszych praktyk.

#### Otwieranie plików

Otwieranie plików w Go jest realizowane za pomocą funkcji `os.Open` i `os.OpenFile` z pakietu `os`. Różnica między nimi polega na tym, że `os.Open` jest ograniczone do otwierania plików tylko do odczytu, podczas gdy `os.OpenFile` umożliwia bardziej szczegółowe kontrolowanie dostępu poprzez flagi i tryby.

1. **Użycie `os.Open`:**
   ```go
   file, err := os.Open("filename.txt")
   if err != nil {
       log.Fatal(err)
   }
   defer file.Close()  // Pamiętaj, aby zawsze zamykać plik po zakończeniu operacji
   ```

   W tym przykładzie `os.Open` otwiera plik tylko do odczytu. Warto zwrócić uwagę na użycie `defer`, które zapewnia, że plik zostanie zamknięty, gdy funkcja, w której jest otwarty, zakończy działanie.

2. **Użycie `os.OpenFile`:**
   ```go
   file, err := os.OpenFile("filename.txt", os.O_RDWR|os.O_CREATE, 0666)
   if err != nil {
       log.Fatal(err)
   }
   defer file.Close()
   ```

   `os.OpenFile` pozwala na specyfikację trybu otwarcia pliku. Flaga `os.O_RDWR` pozwala na odczyt i zapis do pliku, `os.O_CREATE` tworzy plik, jeśli nie istnieje, a `0666` to standardowe uprawnienia pliku, które pozwalają wszystkim użytkownikom na odczyt i zapis.

#### Czytanie z plików

Do czytania z plików w Go używa się pakietu `io` lub `bufio`, które oferują różne metody dostosowane do potrzeb aplikacji, takie jak czytanie po linii, czytanie z bufora czy czytanie całego pliku na raz.

1. **Czytanie całego pliku:**
   ```go
   data, err := ioutil.ReadFile("filename.txt")
   if err != nil {
       log.Fatal(err)
   }
   fmt.Println(string(data))
   ```

   Funkcja `ioutil.ReadFile` czyta cały plik do pamięci, co jest proste, ale może być nieefektywne dla dużych plików.

2. **Buforowane czytanie linii po linii:**
   ```go
   file, err := os.Open("filename.txt")
   if err != nil {
       log.Fatal(err)
   }
   defer file.Close()

   scanner := bufio.NewScanner(file)
   for scanner.Scan() {
       fmt.Println(scanner.Text())
   }

   if err := scanner.Err(); err != nil {
       log.Fatal(err)
   }
   ```

   Użycie `bufio.Scanner` jest idealne do czytania plików linia po linii, co jest bardziej wydajne dla dużych plików.

#### Zapisywanie do plików

Zapisywanie do plików również może być realizowane na różne sposoby w zależności od wymagań aplikacji. Można użyć `ioutil.WriteFile` dla prostego zapisu całego bufora danych lub `os.File` dla bardziej złożonych operacji zapisu.

1. **Prosty zapis do pliku:**
   ```go
   data := []byte("Hello, world!\n")
   err := ioutil.WriteFile("filename.txt", data, 0644)
   if err != nil {
       log.Fatal(err)
   }
   ```

   Funkcja `ioutil.WriteFile` zapisuje dane z bufora `data` do pliku, tworząc plik lub nadpisując go, jeśli już istnie

niej. Funkcja przyjmuje trzy argumenty: ścieżkę do pliku, dane do zapisu i uprawnienia pliku, które określają, kto może odczytywać i zapisywać plik.

2. **Zapisywanie z większą kontrolą:**
   ```go
   file, err := os.OpenFile("filename.txt", os.O_WRONLY|os.O_CREATE|os.O_APPEND, 0644)
   if err != nil {
       log.Fatal(err)
   }
   defer file.Close()

   if _, err := file.Write([]byte("Hello again, world!\n")); err != nil {
       log.Fatal(err)
   }
   ```

   Użycie `os.OpenFile` z flagami `os.O_WRONLY` (tylko do zapisu), `os.O_CREATE` (utwórz, jeśli nie istnieje), i `os.O_APPEND` (dołącz do końca) pozwala na precyzyjne kontrolowanie, jak dane są zapisywane do pliku. Jest to przydatne w aplikacjach, które potrzebują dołączać dane do istniejącego pliku bez nadpisywania go.

### Zaawansowane operacje na plikach

Go oferuje również zaawansowane funkcje do pracy z plikami, w tym manipulację atrybutami plików, przechodzenie po strukturach katalogów i monitorowanie zmian w plikach za pomocą narzędzi takich jak `filepath.Walk` i `fsnotify`.

1. **Przechodzenie po katalogach:**
   ```go
   err := filepath.Walk("start_directory", func(path string, info os.FileInfo, err error) error {
       fmt.Println(path)
       return nil
   })
   if err != nil {
       log.Fatal(err)
   }
   ```

   Funkcja `filepath.Walk` przechodzi rekursywnie przez katalogi zaczynając od `start_directory`, wykonując podaną funkcję dla każdego pliku i katalogu, co jest przydatne do analizy struktury katalogów czy przetwarzania plików w batchu.

2. **Monitorowanie zmian w plikach:**
   - Biblioteka `fsnotify` pozwala na monitorowanie zmian w plikach i katalogach w czasie rzeczywistym.
   ```go
   watcher, err := fsnotify.NewWatcher()
   if err != nil {
       log.Fatal(err)
   }
   defer watcher.Close()

   done := make(chan bool)
   go func() {
       for {
           select {
           case event, ok := <-watcher.Events:
               if !ok {
                   return
               }
               fmt.Println("event:", event)
           case err, ok := <-watcher.Errors:
               if !ok {
                   return
               }
               log.Println("error:", err)
           }
       }
   }()

   err = watcher.Add("/tmp/fd")
   if err != nil {
       log.Fatal(err)
   }
   <-done
   ```

   Ta konstrukcja umożliwia reagowanie na zdarzenia takie jak tworzenie, modyfikacja, usunięcie plików, co jest nieocenione w aplikacjach, które muszą reagować na zmiany w systemie plików na żywo.

### Podsumowanie

Zarządzanie plikami w Go jest niezwykle elastyczne dzięki rozbudowanej bibliotece standardowej, która umożliwia łatwe i wydajne przetwarzanie plików i katalogów. Opanowanie tych technik jest kluczowe dla wielu aplikacji, szczególnie tych, które wymagają zaawansowanej obróbki danych, logowania, zarządzania konfiguracją, czy też obsługi danych użytkownika. Dzięki prostocie i potędze Go, programiści mogą efektywnie implementować skomplikowane zadania związane z systemem plików, zapewniając szybkość i niezawodność swoich aplikacji.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com