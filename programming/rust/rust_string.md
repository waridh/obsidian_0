# `String`

This is a standard class that points to a string literal stored on the heap and contain information about the string that is being pointed to. This page will describe some useful string methods for reference. Something of note about strings is that they are UTF-8 encoding by default, you can use `OsString` if you need to use a non UTF-8. The documentation on this specific type is deep and vast, so it will be updated as I learn more about this language.

### Trim

You can remove the surrounding whitespaces in a `String` by using the `::trim()` method. Here is an example

```rust
let string = "Hello,    ";
let trim = s.trim();
```

### `::replace()`

This method allows us to replace a substring with a different string. This actually works with the string literal, and not the `String` class. Here is the syntax for it.

```rust
string.replace(match, substring);
```

Now for an example

```rust
let string = "Rust is boring";
string.replace("boring", "interesting");
```

## string slice vs String

Here is a code snippet that shows you which is which after running through a function.

```rust
fn string_slice(arg: &str) {
    println!("{}", arg);
}
fn string(arg: String) {
    println!("{}", arg);
}

fn main() {
    string_slice("blue"); // Actual string literal
    string("red".to_string()); // Converts to string struct
    string(String::from("hi")); // Initializing string struct
    string("rust is fun!".to_owned()); // Gives the literal an owner
    string_slice("nice weather".into()); // I have no idea what this method does
    string(format!("Interpolation {}", "Station")); // format returns struct
    string_slice(&String::from("abc")[0..1]); // String slice returns slice
    string_slice("  hello there ".trim()); // trim also returns a slice
    string("Happy Monday!".to_string().replace("Mon", "Tues"));
    string("mY sHiFt KeY iS sTiCkY".to_lowercase()); // This was surprising
}
```

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

A big note with Rust is that you cannot just index the string. It's forbidden to do it raw like that. Okay, here is the weird bit. You should be able to do a range index to get a string return. This is really what they mean by string slicing.

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

## Dereferencing

`String` inherits all of `str`'s method because it implements `Deref<Target = str>` meaning that it will just dereference into a `str`. You are thus allowed to pass a `String` as a `&str` in a function. This is a very inexpensive operation, so generally, it's not a bad idea to make your functions take `&str` as an argument.

```rust
fn take_str(string: &str)  {}
let s = String::from("hello");
take_str(&s);
```

## Representation
