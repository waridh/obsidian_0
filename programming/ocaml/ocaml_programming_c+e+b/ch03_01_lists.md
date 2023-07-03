# Lists

Conceptually, we know what a list is, but how is it done is OCaml? Lists in OCaml are implemented as a singly linked list. These list enjoy first class status in the language. There are a lot of macro supports for lists in OCaml, so it is easy to use.

## 3.1.1 Building a List

There are three syntactic forms for building a list in OCaml:

```OCaml
[]
e1 :: e2
[e1; e2; ...; en]
```

`[]` is an empty list, and it is pronounced `nil`.  Given a list `lst` and an element `elt`, we can prepend the list by writing `elt :: lst`. The `::` is called a cons, and it stands for constructor. Only the first element of the list is called the head, the rest are called the tail.

Another cool thing is that the following are equivalent:

```OCaml
[e1; e2; ...; en]
e1 :: e2 :: ... :: en :: []
```

Now since the element of the list is actually arbitrary, then we could actually nest the list as deep as we like. e.g., `[[[]]; [[1; 2; 3]]]`.

### Dynamic semantics

- [] is already a value
- If `e1` evaluates to value `v1` and if `e2` evaluates to value `v2`, then `e1 :: e2` evaluates to `v1 :: v2`.

Through some mathematical derivation, we end up with the rule:

- If `ei` evaluates to `vi` for all `i`, then `[e1; ...; ei]` evaluates to `[v1; ...; vi]`.

We are now sick of saying evaluates to, we instead we are going to be using a new notation: `==>`. This is not OCaml syntax, Cornell just decided that they did not want to write boiler plate text.

- If `e1 ==> v1` and if `e2 ==> v2` then `e1 :: e2 ==> v1 :: v2`.
- If `ei ==> vi` for all `i`, then `[e1; ...; ei] ==> [v1; ...; vi]`.

### Static Semantics

All the elements in a list must have the same type. If an element type is `t`, then the type of the list is `t list`. Types in lists should be read from right to left, so a list of list of `t`'s would be `t list list`. `list` isn't a type. but instead a type constructor. It takes in a type and generate a new type. It is like a function that operates on a type instead of a value.

Type-checking rules:

- `[] : 'a list`
- If `e1 : t` and `e2 : t list` then `e1 :: e2 : t list`.

On that `nil`, the compiler will assume generic until something is passed into in, in which the type of the list will be defined.

## 3.1.2 Accessing a list

You can really only build a list with either a `nil` or a `cons`. If we want to look inside a list, we actually also have to define what happens on empty content, and if it's non-empty. This is *pattern matching* and we see it in Rust as well.

Here is an example of pattern matching used to get the sum of a list:

```OCaml
let rec sum lst =
    match lst with
    | [] -> 0
    | h :: t -> h + sum t

val sum : int list -> int = <fun>
```

As you can see here, iterating through a list was made recursive. Let `h` be the head element and `t` be the tail element. Other names could be use, but the underlaying principle of matching still applies.

Actually, just to note, we never need newlines when defining these functions, they were just added for better readability. Second point is that the first `|` is optional. A faster way to write this function would be the following:

```OCaml
let rec sum lst = match lst with [] -> 0 | h :: t -> h + sum t
```

Here is an example of writing a function that calculates the length of a list:

```OCaml
let rec length lst = match lst with [] -> 0 | h :: t -> 1 + length t
```

```OCaml
val length : 'a list -> int = <fun>
```

Actually, if we are not going to be using the value, but still show it's presence in pattern matching, you can use `_`.

```OCaml
let rec length lst = match lst with [] -> 0 | _ :: t -> 1 + length t
```

What is nice here is that OCaml has a built in library with a lot of these functions already. Finding the length of a list can be done using the function `List.length`.

Another list function example:

```OCaml
let rec append lst1 lst2 =
    match lst1 with [] -> lst2 | h :: t -> h :: append t lst2
```

```OCaml
val append : 'a list -> 'a list -> 'a list = <fun>
```

Learning how to create this function is useful, but like before, the function has already been implemented by OCaml, and it is the operator `@`. Here is an example of the usage:

```OCaml
lst1 @ lst2
```

Here is another example of examining if a list is empty:

```OCaml
let empty lst = match lst with [] -> true | h :: t -> false
```

```OCaml
val empty : 'a list -> bool = <fun>
```

It's not even a recursive function because the checking method is simple and does not need traversal.

Another thing to think about is that induction and recursion are very similar. In induction with natural numbers, we start with the base case of 0, and an inductive case of $n + 1$. In recursion, we have a base case of 0/[], and a recursive case of non-empty.

Back to the topic of lists, there are two library functions for getting the head and getting the tail of a list, `List.hd` and `List.tl`. This issue with these functions is that they will return an error when used on an empty list. Unlike Rust, the compiler will not argue with you when there are some cases that are not handled.

## 3.1.3 (Not) Mutating Lists

Something big to note is that lists are actually immutable and OCaml programmers will have to just consume and return a new list every time that they want to change it. Here is a function that will return the same list, but with the first element incremented by one.

```OCaml
let inc_first lst = match lst with [] -> [] | h :: t -> h + 1 :: t
```

So we are actually returning a 
