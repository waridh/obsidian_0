---
tags: rust, error_handling, panic
---
# Panic!

## Overview

This is the simplest error handling mechanism `panic`. It will print an error message and start unwinding the stack. Usually it will exit the program as well.

### Example code

```rust
fn drink(beverage: &str) {
    // You shouldn't drink too much sugary beverages.
    if beverage == "lemonade" { panic!("AAAaaaaa!!!!"); }

    println!("Some refreshing {} is all I need.", beverage);
}

fn main() {
    drink("water");
    drink("lemonade");
}
```
