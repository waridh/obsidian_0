# Recoverable Errors with Result

This is us installing error handling for easy errors that can be dealt with. So, `Result` is actually an `enum`, just like `Option`. It is defined as follows:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}

```

You can see it has two state, `Ok(T)` and `Err(E)`. Both `E` and `T` are just generic type parameters, it could really just be anything.

The success case will return an `Ok(T)` and a failure case will return an `Err(E)`.

Here is an example that uses a function that returns a `Result` type in the following code snippet.

```rust
use std::fs::File;

fn main() {
    let greeting_file_result = File::open("hello.txt");
}
```

`File::open()` returns a `Result<T, E>`. The `T` is `std::fs::File`, which is the standard file handle. The `E` in this case is a `std::io::Error` type. Using this system, functions will now have an error handling system that isn't just returning either a 0 or a -1. This makes the language more clear and concise.

So after making the 