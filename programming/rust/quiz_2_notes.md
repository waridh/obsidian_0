---
tags: rust, rustlings, practice
---

# Quiz 2 Notes

## What did I learn?

```rust
pub enum Command {
/*This is an enumeration, it's pretty straight forward*/
    Uppercase,
    Trim,
    Append(usize),  // Has a value actually attached to this one
}

mod my_module {
    use super::Command;

    // TODO: Complete the function signature!
    pub fn transformer(input: Vec<(String, Command)>) -> Vec<String> {
        // TODO: Complete the output declaration!
        let mut output: Vec<String> = vec![];
        for (string, command) in input.iter() {
            // TODO: Complete the function body. You can do it!
            match command {
                Command::Uppercase => {
                    string.as_str().to_uppercase(); // Simply make the thing uppercase
                    output.push(String::from(string.as_str().to_uppercase()));

                },
                Command::Trim => {
                    output.push(String::from(string.as_str().trim()));
                },
                Command::Append(num) => {
                    string.as_str(); let mut buffer = String::from(string);
                    for _i in 0..*num {
                        buffer.push_str("bar");
                    }
                    output.push(buffer);
                }
            }
        }
        output
    }
    fn trim_func(victim: &String)  {
        // Not really sure what is going on in this one
    }
}

#[cfg(test)]
mod tests {
    // TODO: What do we need to import to have `transformer` in scope?
    use crate::my_module::transformer;
    use super::Command;

    #[test]
    fn it_works() {
        let output = transformer(vec![
            ("hello".into(), Command::Uppercase),
            (" all roads lead to rome! ".into(), Command::Trim),
            ("foo".into(), Command::Append(1)),
            ("bar".into(), Command::Append(5)),
        ]);
        assert_eq!(output[0], "HELLO");
        assert_eq!(output[1], "all roads lead to rome!");
        assert_eq!(output[2], "foobar");
        assert_eq!(output[3], "barbarbarbarbarbar");
    }
}

```

# Citation

- [String stuff](rust_string.md)