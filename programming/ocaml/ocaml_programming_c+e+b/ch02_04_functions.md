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

*Note: When you are annotating the type of a variable in OCaml, you also need to include the bracket. Sometimes, it is simpler to just let the compiler infer the type as to not leave clutter.*

### Syntax

```OCaml
let rec f x1 x2 ... xn = e
```

`f` is a metavariable for function. `rec` is required if the function will be recursive, else it is not needed.

### Mutually recursive functions can be defined with the `and` keyword:

```OCaml
let rec f x1 x2 .. xn = e1
and g y1 ... yn = e2
```

What does this mean? It seems unclear from just the syntax, but the example provided below might shed some more light on what it means:

```OCaml
(** [even n] is whether [n] is even.
    Requires: [n >= 0]. *)
let rec even n =
  n = 0 || odd (n - 1)

(** [odd n] is whether [n] is odd.
    Requires: [n >= 0]. *)
and odd n =
  n <> 0 && even (n - 1);;
```

So you are essentially defining two functions that are both calling each other.

### Function type syntax

```OCaml
t -> u
t1 -> t2 -> u
t1 -> ... -> tn -> u
```

Where `t` is the input type and `u` is the output type. `t1 -> t2 -> u` is a function that takes two inputs.

### Static Semantics

For non-recursive functions, assuming that `x1 : t1`, and `x2 : t2` and ... `xn : tn`, we can conclude that `e : u`, then `f : t1 -> t2 -> ... -> tn -> u`.

## 2.4.2 Anonymous Functions

We often see values that are not bound to a name, like the following:

```OCaml
# 42;;
- : int = 42
```

Or we can choose to bind it to a name where we get:

```OCaml
# let x = 42;;
val x : int = 42
```

Similar to this, OCaml will let you do the same things with functions. Here is an example:

```OCaml
fun x -> x + 1
```

So the `fun` keyword is used to signify an anonymous function. x is the argument, and x + 1 is the expression in the function.

Now we have two ways to write the same function:

```OCaml
let incr x = x + 1;;
let incr = fun x -> x + 1;;
```

Although syntactically different, they have the same semantics.

Anonymous functions are also called Lambda expressions, after Lambda calculus. In lambda calculus, the expression `fun x -> e` would be written $\lambda x.e$. where the $\lambda$ represents an anonymous function.

### Syntax

```OCaml
fun x1 ... xn -> e
```

### Dynamic Semantics

The anonymous function is already a value so no computation needs to be performed.

### Static Semantics

If we assume that `x1 : t1`, `x2 : t2`, and `xn : tn`,  we conclude that `e : u`, then `fun x1 ... xn -> e : t1 -> t2 -> ... -> tn -> u`.

## Function Application

Here is a simplified version of function applications. This is the syntax for it:

```OCaml
e0 e1 e2 ... en
```

The first expression `e0` is the function and it is applied to arguments `e1` to `en`. This is like calling a function in languages like TCL.

### Static Semantics

If we assume that `e1 : t1`, `e2 : t2`, ... `en : tn` and `e0 : t1 -> t2 -> ... -> tn -> u`, then `e0 e1 ... en : u`.

### Dynamic Semantics

To evaluate `e0 e1 ... en`:

1. Evaluate `e0` to a function, and evaluate the rest of the expressions to a value. For `e0` you will either have an anonymous function or a named function `f`. If it is named, you will have to find the definition for the function `f`. Anyways, regardless of if the function that is defined by `e0` is a recursive, non-recursive, or anonymous function, we now have the argument names and the body expressions. The rest of the expression `e1` ... `en` are evaluated to a value `v1` ... `vn`. `f` is also viewed as `let rec f x1 ... xn = e`.
2. Substitute each values `vi` for the corresponding value `xi` in the body `e`. This substitution creates a new expression `e'`.
3. Evaluate `e'` to a new value `v`, which is the result of the evaluation of `e0 e1 ... en`.

Both these rules and the rules for `let` involves some substitution. This was done on purpose to allow for multiple methods to represent the same semantics. For example `let x = e1 in e2` is semantically identical to `(fun x e2) e1`.

## 2.4.4 Pipelines

OCaml has a built-in infix for function application called the pipeline operator. This is written like this: `|>` which looks like triangle pointing to the right. It's supposed to look like values being sent from the left to the right. Here is an example for better understanding:

```OCaml
let square = fun x -> x * x;;
let inc = fun x -> x + 1;;
```

Here are two ways to square 6:

```OCaml
square (inc 5);;
5 |> inc |> square;;
(* They will both evaluate to 36*)
```

Instead of working by nesting with confusing parenthesis, we are now working with literally an arrow pointing us in the direction that we want to value to travel. This is incredibly clear to readers what is happening.

A good example of why this is a good idea can be seen in the example below:

```OCaml
5 |> inc |> square |> inc |> inc |> square;;
square (inc (inc (square (inc 5))));;
```

So what we just learned here is a just a nicer way to scale function applications to when you have to process through a lot of functions.

## 2.4.5 Polymorphic Functions

*The identity function* is the function that just returns the input.

```OCaml
let id x = x

val id : 'a -> 'a = <fun>

let id = fun x -> x

val id : 'a -> 'a = <fun>
```

`'a` is called a type variable which represent an unknown type. It will always start with a single quote, and the common ones are `'a`, `'b`, and `'c`, which are pronounced alpha, beta, and gamma.

```OCaml
id 42;;
id true;;
id "bigred";;

- : int = 42
- : bool = true
- : string = "bigred"
```

Since you can apply this one function to multiple types, it is a polymorphic function. *poly* for many, and *morphic* for forms.

By adding some manual type annotation, we can force the function to be more restrictive. For example:

```OCaml
let int_id (x : int) = (x : int)
```

^ By doing this, other types cannot be used with this function now. Now another way to declare this `int` only function using the original `id` function is by doing the following:

```OCaml
let int_id' : int -> int = id
```

So what is happening here? I suppose we bounded the original `'a -> 'a` function to a new name with the restriction of `int -> int`. Supposedly we should be looking at this in terms of behaviour. The function `int_id` promises to take `int` as an input and also have `int` as an output. Even though the original `id` function makes many more promises, namely other types like `bool` as input and output. By binding `id` in this way, we basically throw away the other promises and leave it as only `int`. Doing this is pretty safe, so we can write some functions without types and then morph it into the type we need it to be later.

Doing the converse is not true. We cannot go from `int -> int` to `'a -> 'a`. This will cause many issues when your input is not an `int`, but luckily for us, OCaml is actually smart enough to stop the assignment from going through. This interaction can be thought in terms of function assignments.

| [Previous](ch02_03_expressions.md) | [Next]() | 
| ---------------------------------- | -------- |
