Concurrency
==========

- The Go scheduler orchestrates execution of goroutines and directly dicates which one is running, on which logical processor.
- Synchronization and communication between goroutines is done using Channels
- Each logical processor is bound to a single OS thread
- Starting with Go 1.5, one logical processor per CPU is created


### Goroutines
