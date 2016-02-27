Interfaces
==========

- An interface defines methods without implementation, a la Java
- A type that implements an interface is called a concrete type
- **When implementing an interface on a pointer receiver, only pointers of that type will implement it**
- This is because it's not always possible to get the address of a value (looks like you can't get the address of primitive types?)
- Look at `interface.go` for an example.

- Inner type identifiers of a struct are promoted to the outer type of the struct.
- This means that for `type admin struct {user}`, we can call `adminInstance.userMethod()` as well as `adminInstance.user.userMethod()`
- Therefore, the admin struct also implements interfaces implemented by the user struct.
- You can prevent that by overriding the interface method with an outer struct receiver
