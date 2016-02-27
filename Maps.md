Maps
====

- Maps are unordered
- Idiomatic way to create a map :
  ```go
    // map[keyType]valueType
    dict := map[string]string{"Red": "#da1337", "Orange": "#e95a22"}

    // Create an empty map to store colors and their color codes.
    colors := map[string]string{}
    // Add the Red color code to the map.
    colors["Red"] = "#da1337"
  ```

- Slices, functions, and struct types that contain slices can’t be used as map keys

- Checking if a key existed is important because otherwise you'll get the default init value of the type
  ```go
    // Retrieve the value for the key "Blue".
    value, exists := colors["Blue"]
    // Did this key exist?
    if exists {
        fmt.Println(value)
    }
  ```

- Iteration :
  ```go
    // Display all the colors in the map.
    for key, value := range colors {
        fmt.Printf("Key: %s  Value: %s\n", key, value)
    }
 ```

- Delete a key/value pair :
  ```go
    delete(colors, "Coral")
  ```

- Passing a map to a function is by reference. No copy is made.
- `len` works on maps
