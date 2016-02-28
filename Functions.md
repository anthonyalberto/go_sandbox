Functions
=========
- Equivalent of a ruby splat :
  ```go
    func (r *Runner) Add(tasks ...func(int)) { // Takes any number of functions that accept an int param
      r.tasks = append(r.tasks, tasks...)      // Access all params
    }

    // Given a method like :
    func doStuff(int id) {
      // ...
    }
    // TODO: check that it actually works
    // Can be called like :
    r.Add(doStuff, doStuff, doStuff)
  ```
