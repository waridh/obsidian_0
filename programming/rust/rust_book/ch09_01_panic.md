# Unrecoverable Errors with `panic!`

Rust's `panic!` macro is used for bad things that happened and you cannot do anything about it. It will print error messages, unwind, clean up the stack, and exit the  program. Rust has a feature where you could make it print the call stack so that you can find the source of the error.

## Aborting vs Unwinding
Unwinding and cleaning up the stack could be a lot of work, so the programmer could also choose to immediately abort. This will end the program without cleaning up, meaning that it will be the operating system's job to get rid of those leftover memories. To do this, you need to add `panic = 'abort'` to the appropriate `[profile]` section in the *Cargo.toml* file. Here is an example code snippet

```cargo
[profile.release]
panic = 'abort'
```

## Calling `panic!`

This is how you call `panic!` in a simple file.

```rust
fn main() {
    panic!("CRASH AND BURN!!!");
}
```

Which will result in the following output:

```
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished dev [unoptimized + debuginfo] target(s) in 0.25s
     Running `target/debug/panic`
thread 'main' panicked at 'crash and burn', src/main.rs:2:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace

```

## Using the `panic!` backtrace

Here is an example that is causing `panic!` to get called:

```rust
fn main() {
    let v = vec![1, 2, 3];

    v[99];
}
```

This will cause a compilation error because you are trying to access an index that has not been initialized. In Rust, we do not get an `undefined` behaviour like you would with C or C++. Instead Rust will just halt the program.