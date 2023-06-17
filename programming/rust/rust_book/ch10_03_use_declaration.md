---
tags: rust, modules
---
# `use`

The use declaration is used for binding a full module path to a new name for easier writing. Here is an example of how it is used.

```rust
use crate::deeply::nested::{
    my_first_function,
    my_second_function,
    AndATraitType
};

fn main() {
    my_first_function();
}
```

From what I understand here, it's like importing a specific function from a library in Python.

## `as`

There is a second portion to the `use` pipeline, and that is using `as` to bind those imports to a different name. Here are some examples of doing that.

```rust
// Bind the `deeply::nested::function` path to `other_function`.
use deeply::nested::function as other_function;

fn function() {
    println!("called `function()`");
}

mod deeply {
    pub mod nested {
        pub fn function() {
            println!("called `deeply::nested::function()`");
        }
    }
}

fn main() {
    // Easier access to `deeply::nested::function`
    other_function();

    println!("Entering block");
    {
        // This is equivalent to `use deeply::nested::function as function`.
        // This `function()` will shadow the outer one.
        use crate::deeply::nested::function;

        // `use` bindings have a local scope. In this case, the
        // shadowing of `function()` is only in this block.
        function();

        println!("Leaving block");
    }

    function();
}
```

Quick note with these. If you use `use` within a module, you are able to set it as public, and allow other functions to call the shortcut that is being used by the module. Think of it like Python's import as.

# Pointers

- [Home: Chapter 10](ch10_00_modules.md)
- [Next: `super` and `self`](ch10_04_super_and_self.md)
- [Previous: Struct Visibility](ch10_02_struct_visibility.md)
