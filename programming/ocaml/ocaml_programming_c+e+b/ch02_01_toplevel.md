# The OCaml Toplevel

The Toplevel is like a calculator or a command-line interface to OCaml. It's similar to JShell for Java, or the interactive Python interpreter. The toplevel is useful for trying out small piece of code without going to the trouble of launching the OCaml compiler, but its not very good for working with larger programs.

The toplevel is more like a read-eval-print-loop. It can read the programmer input, evaluate, print the result, and repeat.

To start the toplevel, just run `utop` in the terminal. `ctrl-D` is how you exit the toplevel, but you can also type in `#quit;;`. In the toplevel, you need to put the `#` before a command.

## 2.1.1 Types and Values

You can type in expressions in the OCaml toplevel. End an expression with a double semi-colon `;;` and then press the return key. OCaml will evaluate the expression and tell you the resulting value, and the value's type.

```OCaml
# 42;;
- : int = 42
```

