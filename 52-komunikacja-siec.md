### Programowanie sieciowe

Programowanie sieciowe w Go jest zaawansowanym tematem, który obejmuje tworzenie serwerów HTTP, implementację klientów HTTP oraz pracę z gRPC. W każdym z tych obszarów Go oferuje nie tylko skuteczne narzędzia, ale także wydajne podejście do zarządzania współbieżnością i komunikacją sieciową.

#### Tworzenie serwerów HTTP

1. **Podstawy tworzenia serwera HTTP:**
   - Funkcja `http.ListenAndServe` z pakietu `net/http` jest podstawowym narzędziem do uruchamiania serwera HTTP. Serwer można skonfigurować do obsługi różnych ścieżek za pomocą handlerów.
   ```go
   http.HandleFunc("/home", func(w http.ResponseWriter, r *http.Request) {
       fmt.Fprintf(w, "Welcome to the Home Page")
   })
   log.Fatal(http.ListenAndServe(":8080", nil))
   ```
   Ten kod uruchamia serwer na porcie 8080, obsługujący żądania na ścieżce `/home`.

2. **Używanie muxów do zaawansowanego routingu:**
   - Dla zaawansowanego routingu, biblioteka `gorilla/mux` jest bardziej elastycznym rozwiązaniem, pozwalającym na definicję zmiennych w ścieżkach, ograniczenia metod HTTP i wiele innych.
   ```go
   r := mux.NewRouter()
   r.HandleFunc("/books/{title}/page/{page}", func(w http.ResponseWriter, r *http.Request) {
       vars := mux.Vars(r)
       title := vars["title"]
       page := vars["page"]
       fmt.Fprintf(w, "You've requested the book: %s on page %s", title, page)
   })
   http.ListenAndServe(":8080", r)
   ```
   Tutaj `mux.Router` pozwala na dynamiczne reagowanie na elementy ścieżki URL.

#### Klient HTTP

1. **Wykonywanie prostych żądań HTTP:**
   - Go umożliwia łatwe tworzenie klientów HTTP, które mogą wysyłać żądania do serwerów. Użycie `http.Get` jest jednym z najprostszych sposobów na wysłanie żądania GET.
   ```go
   response, err := http.Get("http://example.com")
   if err != nil {
       log.Fatal(err)
   }
   defer response.Body.Close()
   body, err := ioutil.ReadAll(response.Body)
   if err != nil {
       log.Fatal(err)
   }
   fmt.Println(string(body))
   ```
   To żądanie pobiera treść z podanego URL i wyświetla ją.

2. **Zaawansowane żądania z `http.Client`:**
   - Dla bardziej skomplikowanych żądań, można użyć struktury `http.Client`, która oferuje większą kontrolę nad procesem wysyłania żądań, w tym zarządzanie nagłówkami, timeoutami i innymi.
   ```go
   client := &http.Client{
       Timeout: time.Second * 10,
   }
   request, err := http.NewRequest("POST", "http://example.com", strings.NewReader("data"))
   request.Header.Set("Content-Type", "application/json")
   response, err := client.Do(request)
   if err != nil {
       log.Fatal(err)
   }
   defer response.Body.Close()
   // Obsługa odpowiedzi
   ```

#### Praca z gRPC

1. **Definiowanie usług gRPC:**
   - gRPC wykorzystuje język definicji interfejsu (IDL), aby zdefiniować struktury danych i usługi, które mogą być wywoływane zdalnie. Te definicje są zapisywane w plikach `.proto`.
   ```proto
   syntax = "proto3";

   service Greeter {
       rpc SayHello (HelloRequest) returns (HelloReply);
   }

   message HelloRequest {
       string name = 1;
   }

   message HelloReply {
       string message = 1;
   }
   ```

2. **Implementacja serwera gRPC:**
   - Serwer gRPC w Go jest tworzony przez implementację funkcji zdefiniowanych w plikach `.proto`.
   ```go
   type server struct {
       pb.UnimplementedGreeterServer
   }

   func (s *server) SayHello(ctx context.Context, in *pb.HelloRequest) (*pb.HelloReply, error) {
       return &pb.HelloReply{Message: "Hello " + in.Name}, nil
   }

   func main() {
       lis, err := net.Listen("tcp", ":50051")
       if err != nil {
           log.Fatalf("failed to listen: %v", err)
       }
       s := grpc.NewServer()
       pb.RegisterGreeterServer(s, &server{})
       if err := s.Serve(lis); err != nil {
           log.Fatalf("failed to serve: %v", err)
       }
   }
   ```

### Podsumowanie

Programowanie sieciowe w Go, od prostych serwerów HTTP po zaawansowane usługi gRPC, pozwala na budowanie wydajnych, skalowalnych i łatwych w utrzymaniu systemów. Współbieżność w Go, jej prostota i wydajność sprawiają, że jest on doskonałym wyborem dla nowoczesnych aplikacji sieciowych, zarówno na potrzeby wewnętrzne, jak i zewnętrzne. Wykorzystanie tych zaawansowanych technik pozwala na tworzenie aplikacji, które mogą skutecznie komunikować się w rozproszonych środowiskach.

---
© 2024 Marian Witkowski marian.witkowski[at]gmail.com