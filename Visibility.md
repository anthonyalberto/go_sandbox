Visibility rules
================
- In a package, identifiers beginning with a lower case letter are not accessible outside of the package
- In a package, identifiers beginning with an upper case letter are accessible outside of the package
- Conventionally, factory methods are called `New`. This will allow to instantiate an unexported type of the package.
- Those rules also apply to fields within a struct.
  ```go
    type User struct { // Can be used outside of the scope of the package
      Name string      // Can be used outside of the scope of the package
      email string     // Can't be used outside of the scope of the package
    }
  ```

- With embedded types, things get trickier due to inner to outer class promotion :
```go
  type user struct { // Unexported
    Name string      // Exported
    Email string     // Exported
  }

  type Admin struct { // Exported
    user              // Unexported
    Rights int        // Exported
  }

  // All valid outside the scope of the package :
  adminInstance.Name
  adminInstance.Email
  adminInstance.Rights

  // Not valid
  adminInstance.user
```
