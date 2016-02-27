Structs
=======

- Declaration :
  ```go
    type user struct {
      name       string
      email      string
      ext        int
      privileged bool
    }
  ```

- Create a var of that type : `var bill user`
- Create a var of that type while providing init values :
  ```go
    lisa := user{
      name:       "Lisa",
      email:      "lisa@email.com",
      ext:        123,
      privileged: true,
    }

    // OR :
    lisa := user{"Lisa", "lisa@email.com", 123, true}
  ```

- Compose a struct with another struct type :
  ```go
    type admin struct {
      person user
      level  string
    }

    fred := admin{
      person: user{"Fred", "fr@ed.com", 124, true}
      level: "super"
    }
  ```


- Aliasing a type : `type Duration int64`
