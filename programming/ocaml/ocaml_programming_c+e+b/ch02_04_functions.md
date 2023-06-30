# 2.4 Functions

## 2.4.1 Function Definitions

Let's do an analysis of some simple let definition:

```OCaml
let x = 42;;
```

This let command has the expression `(42)` in it, but it is itself not an expression. It is rather a definition, and it binds a value to a name. What you will need to understand is that definitions are not expressions nor expressions definitions. They are distinct syntactic classes.

Let's look at the function definition:

```OCaml
let f x = ...
```

Recursive functions need to be explicitly declared, like the following:

```OCaml
let rec f x = ...
```

This is done because most languages assume that the function is a recursive function, but OCaml does not make that assumption. Here is an example of a popular recursive function:

```OCaml
(** [fact n] is [n]!.
    Requires: [n >= 0]. *)
let rec fact n = if n = 0 then 1 else n * fact (n - 1)
val fact : int -> int = <fun>
```

*Note: The OCaml integers are not mathematical integers, but a computing integer with limited bits.* 


Here is another recursive function:

```OCaml
(** [pow x y] is [x] to the power of [y].
     Requires: [y >= 0]. *)
let rec pow x y = if y = 0 then 1 else x * pow x (y - 1)
```

I'll be honest, some of the syntax here is similar to rust. The recursive writing here is quite efficient, I am a big fan.