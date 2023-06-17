---
tags: rust, option
---
# Option

Options give the data the choice to either be a **`None`** enum or a **`Some`** enum. You can deal with them either by using `match` handling, or by using this thing called unwrap.

## Example code

```rust
// An integer division that doesn't `panic!`
fn checked_division(dividend: i32, divisor: i32) -> Option<i32> {
    if divisor == 0 {
        // Failure is represented as the `None` variant
        None
    } else {
        // Result is wrapped in a `Some` variant
        Some(dividend / divisor)
    }
}

// This function handles a division that may not succeed
fn try_division(dividend: i32, divisor: i32) {
    // `Option` values can be pattern matched, just like other enums
    // This is the method that we are used to.
    match checked_division(dividend, divisor) {
        None => println!("{} / {} failed!", dividend, divisor),
        Some(quotient) => {
            println!("{} / {} = {}", dividend, divisor, quotient)
        },
    }
}

fn main() {
    try_division(4, 2);
    try_division(1, 0);

    // Binding `None` to a variable needs to be type annotated
    let none: Option<i32> = None;
    let _equivalent_none = None::<i32>;

    let optional_float = Some(0f32);

    // Unwrapping a `Some` variant will extract the value wrapped.
    println!("{:?} unwraps to {:?}", optional_float, optional_float.unwrap());

    // Unwrapping a `None` variant will `panic!`
    // If unwrapping a `None` will cause a panic! then how are you supposed to deal with it??
    println!("{:?} unwraps to {:?}", none, none.unwrap());
}
```

## More about unwrap

Unlike `match`, which is the explicit handling of options, `.unwrap()` is the implicit handling of `Option`. `unwrap` will either return the element being held, or it will `panic!`. Panic can be handled by using [expect](https://doc.rust-lang.org/std/option/enum.Option.html#method.expect), but know that we are still losing control when compared to using explicit handling. <!--Still good to learn this to increase the knowledge of Rust features-->