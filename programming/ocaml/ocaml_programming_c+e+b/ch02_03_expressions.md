# Expressions

If imperative languages are primarily built on commands, then functional languages are primarily built on expressions. Some examples are `2 + 2` or `increment 21`.

The primary purpose of functional languages is to *evaluate* an expression to a *value*. A value is an expression in which there are no more computations left to perform, meaning that in function programming, values are expressions, but not all expressions are values. For example `2`, `true`, and `"two!"` are values.

There are some cases in which expressions do not evaluate to a value. There are two reasons that this would happen:
1. The evaluation raised an exception
2. The evaluation never terminates.

## Primitive Types and Values

Primitives are built on the most basic types: integers, floating point numbers, characters, strings and booleans. They act like other primitive types from other languages.

### Integers

Integer operators act just like those of Rust, so it will not be put in the notes.

OCaml integers are signed twos complement and range from $-2^{62}$ to $2^{62}-1$. This is because OCaml uses 64-bit machine words, but one of the bit has been stolen by the OCaml implementation, and thus it's actually a 63 bit integer. That last bit is used to distinguish the value between a float and an integer. There is a library that gets you access to a true 64 bit integer in the **Int64** module. If you want arbitrary precision, then you can use the **Zarith** library. Normally though, the built in **int** type is good enough with the best performance.

### Floats

```OCaml
# 3.;;
- : float = 3.

# 3;;
- : int = 3

```

basically, you will need to put that period in order to specify a float as opposed to an integer. Also, OCaml deliberately does not support operator overloading. Because of this, to do floating point multiplication, you actually need to use `*.` and not `*`.

```OCaml
# 3.14 *. 2;;
- : float = 6.28
```

OCaml will also not automatically convert between floats and int, so you will have to explicitly declare that. This can be seen here:

```OCaml
# 3.14 *. (float_of_int 2);;
- : float = 6.28
```

Because floating point is an estimate, there might be rounding errors that you will have to account for.

### Boolean

Written as `true` or `false`. You can do intersects and unions using `&&` and `||` respectively.

### Character

Written in single quotations like in C, `a`, `b`, `c`. This time it is encoded in Latin-1 which is still the size of a byte per character. You can convert between char in int by using either `char_of_int` or `int_of_char`.

### String

String are written as double quotes: `"abc"` and there is a dedicated string concatenation operator, `^`.

```OCaml

# "abc" ^ "def";;
- : string = "abcdef"
```

There are actually plenty of functions that converts things into strings. Here are a big example list:

```OCaml
# string_of_int 42;;
- : string = "42"
# String.make 1 'z';;
- : string = "z"
# int_of_string "123";;
- : int = 123
```

```OCaml
# "abc".[0];;
- : char = 'a'
```

So you can access chars from string indexing.
