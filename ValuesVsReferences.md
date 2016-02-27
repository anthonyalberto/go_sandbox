When to use values vs references
================================

- Use value receivers/params when you want to create a copy of the object and modify it
- Use reference receivers/params when you want to mutate the original object

- Generally, for primitive types (string, bool, int), pass values
- For reference types (slice, map, channel, interface, function), pass values too. They are designed to be copied over and carry a pointer internally to the underlying values
- For struct types, it depends. If the struct has a primitive nature, pass a value, otherwise a reference. Even if no change has to be made.
- The decision ultimately depends on the type of the variable, and not if the variable needs mutation.
