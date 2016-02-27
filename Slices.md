Slices
======

- Dynamic length arrays
- Allocated in contiguous blocks

- Create a slice of 5 strings :
  ```go
    slice := make([]string, 5)
  ```

- Idiomatic way to create a slice :
  ```go
    slice := []string{"Red", "Blue", "Green", "Yellow", "Pink"}
  ```

- Create a nil slice of integers :
  ```go
    var slice []int
  ```

- Slice a slice :
  ```go
    slice := []int{10, 20, 30, 40, 50}

    newSlice := slice[1:3]
  ```

- Weirdly enough, first value is starting index (1 here), second value is the start index + the number of elements we want to include.
- So the above example just slices 1..2 from the slice

- Extra capacity of a slice can only be used to add new elements. Use `append` :
  ```go
    slice := []int{10, 20, 30, 40, 50}
    newSlice := slice[1:3]

    // Both slices will see the new value
    newSlice = append(newSlice, 60)
  ```

- How length and capacity are calculated :
  For slice[i:j:k]  or  [2:3:4]
  Length: j-i or 3-2=1 Capacity:k-i or 4-2=2

- Therefore slicing like that : `slice := source[2:3:3]` is safer because the new slice can just modify the values that were sliced.


- Append two slices together :
  ```go
    append(s1, s2...)
  ```

- Iterate over a slice :
  ```go
    for index, value := range slice {
      fmt.Printf("Index: %d  Value: %d\n", index, value)
    }
  ```

- **Caution: The value yielded by `range` is a copy of the value**

- Iterate using a traditional C-style `for` :
  ```go
    for index := 2; index < len(slice); index++ {
      fmt.Printf("Index: %d  Value: %d\n", index, slice[index])
    }
  ```

- Fetch length using `len(slice)`
- Fetch capacity using `cap(slice)`

- Passing a slice to a function requires nothing special since they are glorified pointers
- **Obviously the underlying array is not copied. Careful when modifying it**

- Overall, **use slices instead of arrays**
