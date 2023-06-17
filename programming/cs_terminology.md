# Computer Science Terminologies

## Preface

This page talks about the uncommon terminologies that are used commonly in Computer Science that you might be unfamiliar with.

## Definitions

### Boilerplate code

These are codes that must be included in many places that would have little to no alterations. You see it often in verbose programming languages.

#### Example

```rust
    let config_max = Some(3u8);
    match config_max {
        Some(max) => println!("The maximum is configured to be {}", max),
        _ => (), // This is boilerplate code.
    }

```