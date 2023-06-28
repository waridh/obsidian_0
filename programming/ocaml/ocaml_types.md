# Built-in Compound types

## Lists

```OCaml
- : `a list = []
- : int list = [1; 2; 3]
- : int list list = [[1; 2]; [3; 4]; [5; 6]]
- : bool list = [false; true; false]
```

## Tuples

```OCaml
- : float * float = (5., 6.5)
- : bool * float * float * float * string = (true, 0., 0.45, 0.73, "french blue")
```

## Record

This is just a hashmap.

```OCaml
type point = {x: float; y:float; }

val a : point = {x = 5.; y = 6.5}

type colour = {
    websafe : bool;
    r : float;
    g : float;
    b : float;
    name : string;
}

val b : colour = {websafe = true; r = 0.; g = 0.45; b = 0.73; name = "french blue"}
```

The finicky thing with records is that on declaration, it must contain all fields. Secondly, a record may be mutable.