Standard Library
================

### Logging

```go
  log.SetPrefix("TRACE: ") // Set the prefix of each log line
  log.SetFlags(log.Ldate | log.Lmicroseconds | log.Llongfile) // Will automatically log this info for each log line

  log.Println("message") // Write the message.
  log.Fatalln("fatal message") // log and exits with code 1
  log.Panicln("panic message") // log and call panic


  // Declare additional loggers:
  Info := log.New(os.Stdout,
    "INFO: ",
    log.Ldate|log.Ltime|log.Lshortfile)

  // Multi-logger :
  Error = log.New(io.MultiWriter(file, os.Stderr), "ERROR: ", log.Ldate|log.Ltime|log.Lshortfile)
```


### Encoding / Decoding

  - Fetch and Parse the following json :
  ```json
    {
      "responseData": {
        "results": [
          { "field1": "1", "field2": "2" },
          { "field1": "3", "field2": "4" }
        ]
      }
    }
  ```

  ```go
    import (
      "encoding/json"
      "http"
      "log"
      "fmt"
    )

    type (
      result struct {
        Field1 string `json:"field1"`
        Field2 string `json:"field2"`
      }

      response struct {
        ResponseData struct {
          Results []result `json:"results"`
        } `json:"responseData"`
      }

    func main() {
      uri := "http://localhost/testJson"
      resp, err := http.Get(uri)
      if err != nil {
        log.Println("ERROR:", err)
        return
      }
      defer resp.Body.Close()

      // Here the magic happens :
      var res result
      err = json.NewDecoder(resp.Body).Decode(&res)

      if err != nil {
        log.Println("ERROR:", err)
        return
      }

      fmt.Println(res)
    }
  ```

- Encode to json :
  ```go
    // Create a map of key/value pairs.
    c := make(map[string]interface{})
    c["name"] = "Gopher"
    c["title"] = "programmer"
    c["contact"] = map[string]interface{}{
      "home": "415.333.3333",
      "cell": "415.555.5555",
    }

    // Marshal the map into a JSON string.
    data, err := json.MarshalIndent(c, "", "    ")
    if err != nil {
      log.Println("ERROR:", err)
      return
    }

    fmt.Println(string(data))
  ```
