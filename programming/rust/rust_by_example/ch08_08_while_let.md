# `while let`

`while let` is similar to `if let` in the ways where it converts awkward `match` statements into more readable and less verbose method.

## Rust by Example

There are two example given by the **Rust by Example** page that does the same thing, but demonstrate the use of `while let`.

```rust
// Make `optional` of type `Option<i32>`
let mut optional = Some(0);

// Repeatedly try this test.
loop {
    match optional {
        // If `optional` destructures, evaluate the block.
        Some(i) => {
            if i > 9 {
                println!("Greater than 9, quit!");
                optional = None;
            } else {
                println!("`i` is `{:?}`. Try again.", i);
                optional = Some(i + 1);
            }
            // ^ Requires 3 indentations!
        },
        // Quit the loop when the destructure fails:
        _ => { break; }
        // ^ Why should this be required? There must be a better way!
    }
}

```

Above is the implementation using a `loop` and `match`. It is somewhat verbose as you need to nest the `match` inside the `loop`.

```rust
fn main() {
    // Make `optional` of type `Option<i32>`
    let mut optional = Some(0);

    // This reads: "while `let` destructures `optional` into
    // `Some(i)`, evaluate the block (`{}`). Else `break`.
    while let Some(i) = optional {
        if i > 9 {
            println!("Greater than 9, quit!");
            optional = None;
        } else {
            println!("`i` is `{:?}`. Try again.", i);
            optional = Some(i + 1);
        }
        // ^ Less rightward drift and doesn't require
        // explicitly handling the failing case.
    }
    // ^ `if let` had additional optional `else`/`else if`
    // clauses. `while let` does not have these.
}
```

The second code block utilizes `while let` instead of `match` and `loop`. This implementation has less boilerplates and nesting. This is the entire point of it, as they do the same thing, and LLVM will likely convert and optimize them the same way.

## Rustlings example

After completing the Rustlings for this topic, there are some strange things to do with `while let` and vectors that I want to keep a reference of, so you can view it here.

```rust
 #[test]
    fn layered_option() {
        let mut range = 10;
        let mut optional_integers: Vec<Option<i8>> = Vec::new();
        for i in 0..(range + 1) {
            optional_integers.push(Some(i));
        }

        // You can stack `Option<T>`'s into while let and if let
        while let Some(Some(integer)) = optional_integers.pop() {
            assert_eq!(integer, range);
            range -= 1;
        }
    }
```

Biggest thing of note is the double `Some()` that is happening in the `while let`. It looks to be something that I will have to tackle multiple times.