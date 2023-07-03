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


