Arrays
======

- Fixed length
- Stored in Contiguous memory. Fast to go through.
- Declare an array to accomodate 5 ints :
```go
  var array [5]int
```

- Declare an array with default values (array literal):
```go
  array := [5]int{10, 20, 30, 40, 50}
```

- Declare an array of 5 integer pointers, and init the first 2 of them:
```go
array := [5]*int{0: new(int), 1: new(int)}

// Assign values to index 0 and 1.
*array[0] = 10
*array[1] = 20
```

- **Arrays are values**. `array2 := array1` will create a copy of `array1`
- Copying an array of pointers copies the pointer values, not the target of the pointer values

- Be careful when passing big arrays as they are values. Better pass a pointer to it when possible :
```go
  // Allocate an array of 8 megabytes.
  var array [1e6]int
  // Pass the address of the array to the function foo.
  foo(&array)
  // Function foo accepts a pointer to an array of one million integers.
  func foo(array *[1e6]int) {
  // ...
  }
```
