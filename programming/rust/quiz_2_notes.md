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

    /*The function takes a vector as an input. It was a little hard to figure out why it needed to be the way it is. Actually, doing a little reading on vectors would probably be a good idea*/
    pub fn transformer(input: Vec<(String, Command)>) -> Vec<String> {
        // TODO: Complete the output declaration!
        let mut output: Vec<String> = vec![]; // Declare a vector
        for (string, command) in input.iter() {
            // Here, we iterate over the vector and have two var for it.
            match command {  // Enum matching
                Command::Uppercase => {
                    string.as_str().to_uppercase(); // Simply make the thing uppercase
// The one thing that is important here is that whatever we do in the match, we just need to append to the output vector.
output.push(String::from(string.as_str().to_uppercase()));

                },
                Command::Trim => {
                    output.push(String::from(string.as_str().trim()));
                },
                /*For appending to the end of the string, we need to free the reference into a mutable string. I guess I did this in a really weird way. It's a little janky, but what is important is that I know that you need to basically either create a copy or take owndership of the value that was being pointed to by the string. I am not sure if this is copying or if it is passing. Let me go check. Look at the string page for more information, I went and read it*/
                Command::Append(num) => {
                    let mut buffer = String::from(string.as_str());
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
        // I guess I found some sort of solution that did not need this thing.
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