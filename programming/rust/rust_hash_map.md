---
tag: rust, hash_map
---

# Rust Hash Maps

## Declaration

```rust
// Importing the HashMap
use std::collection::HashMap;

// Initiating the HashMap
let mut info: HashMap<i32, String> = HashMap::new();

// Here is an insertion example as well
info.insert(30, String::from("pain"));
```

## Accessing values stored in the Hash Map

Use the `get` method. Here is a little snippet of how to use this method.

```rust
let pain = info.get(&30);
```
It's a little weird that we need to put in a reference to get the value, but that's really because get returns a reference to the value and not the actual value stored by the Hash Map itself.

## Removing values stored in the Hash Map

To remove an item pair from a Hash Map, just use the `remove` method and use the key that you would use for `get` as the argument. Here is the example code:

```rust
info.remove(&30);
```

## How do you change an element in a Hash Map?

You just need to use the `insert` method again. Here is an example for it.

```rust
info.insert(29, String::from("love"));
info.insert(29, String::from("hate")); // The new value stored at 29 is now "hate"
```

## Entry

What is entry?? It's a quick method used to check if the key has a value in a Hash Map. You can use this in conjunction with `or_insert` to fill the Hash Map conditionally when it is either empty or full, and the syntax is much more readable than the `C` and `C++` version of the code. Here is an example by rust.

```rust
use std::collections::HashMap;

let mut map: HashMap<&str, u32> = HashMap::new();

map.entry("poneyland").or_insert(3);
assert_eq!(map["poneyland"], 3);

*map.entry("poneyland").or_insert(10) *= 2; // If the value already exists and needs to be edited
assert_eq!(map["poneyland"], 6);
```

### `or_insert`

To clarify, `or_insert` will only insert the default value given as the argument if the key leads to an empty value. It's better to say that the function is used to make sure that the key is not empty.

### [Other useful function related to `entry`](https://doc.rust-lang.org/std/collections/hash_map/enum.Entry.html)

## Other notes

Because `HashMap`s are not static, we have to format it like this on strings:

```rust
println!("HashMap = {:?}", info);
```

# Pointer