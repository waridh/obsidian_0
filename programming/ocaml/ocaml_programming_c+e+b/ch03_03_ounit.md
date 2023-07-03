# 3.3 Unit testing with OUnit

OUnit is the unit testing framework for OCaml. This is a solution for when your program gets too large for toplevel to test, and you need to design a test suite. Just like with device validation, your test suite needs to contain many unit tests that will test all the different functions and edge cases that your function might run into.

The framework in OUnit is similar to JUnit in Java or HUnit in Haskell. This is the basic workflow of OUnit:
- Write your function in a file `f.ml`. Could have multiple functions.
- Write unit tests in a separate file called `test.ml`.
- Build and run `test` to execute the unit test.

