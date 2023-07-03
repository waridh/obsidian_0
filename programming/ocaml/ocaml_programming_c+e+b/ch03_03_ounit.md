# 3.3 Unit testing with OUnit

OUnit is the unit testing framework for OCaml. This is a solution for when your program gets too large for toplevel to test, and you need to design a test suite. Just like with device validation, your test suite needs to contain many unit tests that will test all the different functions and edge cases that your function might run into.

The framework in OUnit is similar to JUnit in Java or HUnit in Haskell. This is the basic workflow of OUnit:
- Write your function in a file `f.ml`. Could have multiple functions.
- Write unit tests in a separate file called `test.ml`.
- Build and run `test` to execute the unit test.

## 3.3.1 Example of OUnit

Example function file `sum.ml`:

```OCaml
let rec sum = function [] -> 0 | h :: t -> h + sum t
```

`test.ml`:

```OCaml
open OUnit2
open Sum

let tests = "Test suite for sum" >::: [
    "empty" >:: (fun _ -> assert_equal 0 (sum []));
    "singleton" >:: (fun _ -> assert_equal 1 (sum (1 :: [])));
    "two_elements" >:: (fun _ -> assert_equal 3 (sum (1 :: 2 :: [])));

]

let _ = run_test_tt_main tests
```

To run these tests properly, you will actually also have to set up dune so that it would include the `ounit2` module.

```Dune
(executable
(name test)
(libraries ounit2))
```

In the `dune-project` file, just keep things the same:

```OCaml
(lang dune 3.4)
```

Now we will get an indicator if a function breaks.

For example, if `sum.ml` `sum` is written like the following:

```OCaml
let rec sum = function
| [] -> 1 (*bug*)
| h :: t -> h + (sum t)

```

You will see an error that looks like this instead:

```OCaml
FFF
==============================================================================
Error: test suite for sum:2:two_elements.

File ".../_build/oUnit-test suite for sum-...#01.log", line 9, characters 1-1:
Error: test suite for sum:2:two_elements (in the log).

Raised at OUnitAssert.assert_failure in file "src/lib/ounit2/advanced/oUnitAssert.ml", line 45, characters 2-27
Called from OUnitRunner.run_one_test.(fun) in file "src/lib/ounit2/advanced/oUnitRunner.ml", line 83, characters 13-26

not equal
------------------------------------------------------------------------------
```

The first line that say `FFF` tells us that three test cases failed.

## 3.3.2 Explanation of OUnit example

open OUnit2 brings the definitions made in the OUnit2 module into scope. The same thing is done with `Sum`. It's capitalized like that to represent the `sum.ml` file.

We also need to make a list of test cases:

```OCaml
[
    "empty" >:: (fun _ -> assert_equal 0 (sum []));
    "singleton" >:: (fun _ -> assert_equal 1 (sum (1 :: [])));
    "two_elements" >:: (fun _ -> assert_equal 3 (sum (1 :: 2 :: [])));
]
```

Each test case has a string that gives it a descriptive name, and a function that probably does an assertion to check if the function output is equal to what we expect. `assert_equal` is a function that is given by `ounit2`, but it is actually not included with the language.

`>:::` and `>::` are separators provided by `ounit2` to setup your test cases. Use this page as reference when trying to build unit tests.

## 3.3.3 Improving OUnit Output

The default error output for OUnit might not be so helpful. In the previous example, we only see that it says `not equal`, but we could make it better. `assert_equal` has an optional argument that lets you 
