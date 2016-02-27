Methods
=======

- Functions that are invoked on a specific object type
  ```go
    // Receiver is a value. Will create a copy of user.
    func (u user) notify() {}

    // Receiver is a pointer. Will work on the original object passed.
    // This is the traditional behaviour in OO languages
    func (u *user) changeEmail(email string) {}

    // Value
    bill := user{"Bill", "bill@email.com"}
    // Pointer
    lisa := &user{"Lisa", "lisa@email.com"}

    // Regardless of the type of the struct instance (Value vs Pointer),
    // we can invoke methods that expect a value or pointer Receiver.

    // All are OK and working on values/references as they should.
    // The go compiler just references/deferences as needed.
    bill.notify()
    bill.changeEmail("yo@yo.com")
    lisa.notify()
    lisa.changeEmail("yo@yo.com")

    // For the record: Dereference a pointer:
    (*lisa)
    // Reference a value :
    (&bill)
