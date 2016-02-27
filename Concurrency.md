Concurrency
==========

- The Go scheduler orchestrates execution of goroutines and directly dicates which one is running, on which logical processor.
- Synchronization and communication between goroutines is done using Channels
- Each logical processor is bound to a single OS thread
- Starting with Go 1.5, one logical processor per CPU is created


### Goroutines

- Choose how many logical processors at max the scheduler can use :
  ```go
    import "runtime"
    runtime.GOMAXPROCS(1)
    runtime.GOMAXPROCS(runtime.NumCPU()) // Matches the number of cores on the system.
  ```

- Prevent the program from exiting and spawn start 2 goroutines
  ```go
    import "sync"
    var wg sync.WaitGroup
    wg.Add(2)             // This wait group (a counting sempahore) will have to wait for 2 goroutines to be completed

    go func() {
      defer wg.Done() // Will tell the main thread this goroutine is done at the end of the execution of the method.
      // Do some stuff
    }

    go func() {
      defer wg.Done() // Will tell the main thread this goroutine is done at the end of the execution of the method.
      // Do some stuff
    }

    wg.Wait() // Actually block the main thread execution here and wait for goroutines to be done
  ```

- Force a goroutine during execution to be placed back in the queue :
  ```go
    runtime.Gosched()
  ```

- `go build -race` allows to print warnings at execution time when potential race conditions are found

- Atomic operations on integers and pointers are available :
  ```go
    import(
      "sync"
      "sync/atomic"
    )

    atomic.AddInt64(&counter, 1)   // Exclusive add
    atomic.StoreInt64(&counter, 1) // Exclusive write
    atomic.LoadInt64(&counter)     // Exclusive read
  ```

- Mutexes are also available :
  ```go
    import "mutex"
    var mutex sync.Mutex // Declaration

    mutex.Lock()
    {
    // Execute exclusive code here
    }
    mutex.Unlock()
  ```

- Channels however are the preferred way to deal with those issues.
  ```go
    unbuffered := make(chan int) // Create un unbuffered channel of ints
    buffered := make(chan string, 10) // Create a buffered channel of strings. Buffer size is 10.

    buffered <- "Gopher" // Send the string through the channel

    value, ok := <-buffered // Receive the value in another goroutine. !ok means the channel was closed.

    close(buffered) // Closes the channel. Closing a buffered channel still allows to receive, but we can't send to it anymore.
  ```


- Unbuffered channels require both a sender goroutine and a receiver goroutine be ready at the same time to be able to complete.
- Otherwise, either of those operations will be blocked while waiting for the other operation to take place.

- Buffered channels can be written to while no one is receiving.
- Reads are blocking only when there is nothing to read from the channel.
- Writes are blocking when buffer is full.
- There is therefore no guarantee that a send + receive will happen

- For both types, reading from a channel consumes the message. It's not multicast.
