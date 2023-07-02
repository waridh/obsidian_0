# Documentation

## 2.5.1 How to Document

Here is an example of how to create documentation:

```OCaml
(** [sum lst] is the sum of the elements of [lst]. *)
let rec sum lst = ...
```

The double `**` lets the compiler know that this is OCamldoc comment. The `[]` lets the markup know to render it as a monospace.

OCamldoc also supports documentation tags, like `@author`, `@deprecated`, `@param`, `@return`, etc. For some example, Cornell wants you to put these for their assignments:

```OCaml
(** @author Your Name (your netid) *)
```

There are more documentation tricks in the OCaml manual, but these notes are being created for initial ramp up.

## 2.5.2 What to Document

There is no point in doing basic documentation where you declare the parameters and the return values. Instead, follow this example:

```OCaml
(** [sum lst] is the sum of the elements of the [lst].
    The sum of an empty list is 0.*)
let rec sum lst = ...
```

## 2.5.3 Precondition and Postcondition


