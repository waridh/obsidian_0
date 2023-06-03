# `String`

This is a standard class that points to a string literal stored on the heap and contain information about the string that is being pointed to. This page will describe some useful string methods for reference. Something of note about strings is that they are UTF-8 encoding by default, you can use `OsString` if you need to use a non UTF-8.

## Character format

Because Rust Strings are by default, UTF-8, there are some things you need to know. A character in a string that is ASCII will only take up a byte, but that same character as a `char` type would take up 4 bytes. Some non-ASCII characters in a string will also take up more than a byte. Because of the way that Rust indexing works, to get constant time indexing, it has to index by byte, and not by char. To attain char indexing, you would need to use a `char` array. Finally, because we are using byte indexing, when you index through a string, you will get a &u8. Here are some examples of the return of a string index in Rust.

```rust
let s = "hello";
assert_eq!(s.as_bytes()[0], 104);
// or
assert_eq!(s.as_bytes()[0], b'h');  // Neat that you can convert char to byte

// The emoji example

let s = "💖💖💖💖💖";
assert_eq!(s.as_bytes()[0], 240);   // We actually need 3 of the following bytes
									// To decode the value
```

A big note with Rust is that you cannot just index the string. It's forbidden to do it raw like that.

# Methods

## Initialization from pre-existing string

```rust
let s = String::from("hello!");
```

## Pushing to the end

There are two push methods for the `String` class, `::push()` for characters, and `::push_str()` for strings.

Example:

```rust
let s = String::from("Hello, ");

s.push('w');
s.push_str("orld!");
```

