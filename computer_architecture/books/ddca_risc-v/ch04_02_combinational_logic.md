# 4.2 Combinational Logic

This chapter goes through some information about designing combinational logic using HDLs. The output of these circuits will only depend on the current input and have no memory. It's really about learning how to write behavioural models of combinational logic with HDLs.

## 4.2.1 Bitwise Operators

*Bitwise* operators act one a single-bit signal or multibit buses. For example, the `inv` module can be written in SystemVerilog as such:

```SystemVerilog
module inv(input logic [3:0] a,
          output logic [3:0] y);
    assign y=~a; // This makes the y output just the inversion of a
endmodule
```

SystemVerilog lets you choose either little-endian or big-endian. This is done via the order of the index that is put to choose the bus. `[3:0]` is little-endian, while `[0:3]` would be big-endian.

Choosing the endian of the bus has always been arbitrary, and it does not matter in the example circuit that was illustrated here. The book that I am reading is choosing to work with little-endian for the HDL designs that are going to be taught.

Here are some more examples with SystemVerilog:

```SystemVerilog
module gates(input logic [3:0] a, b,
            output logic [3:0] y1, y2, y3, y4, y5);
    /* five different two-input logic gates acting on 4-bit busses*/

    assign y1 = a & b; // AND
    assign y2 = a | b; // OR
    assign y3 = a ^ b; // XOR
    assign y4 = ~(a & b); //NAND
    assign y5 = ~(a | b); //NOR
endmodule
```

SystemVerilog has some operators built in to represent Boolean logic, but not for all gates, as some of them, we have to construct ourselves `&, |, ^` . When operators are combined with operands, it is called an expression: `a & b`. A statement includes the assignment to an output: `assign y1 = a & b`.

Something interesting in SystemVerilog are *continuous assignment statements*. Here is an inline example: `assign out = in1 op in2`. Basically, this syntax changes the state of out based on the inputs. This is the foundation to combinational logic.

## 4.2.2 Comments and White Spaces

This subsection teaches electrical engineers to comment code. I don't have that background, and so, know how to comment well.

## 4.2.3 Reduction Operators

Reduction operators imply a multi-input gate acting on a single bus.

## 4.2.4 Conditional Assignment

*Conditional assignment* select the output from among alternatives based on an input called *condition*. It's literally a conditional from programming.

Here is how you can write a 2:1 multiplexer using conditional assignment.

```SystemVerilog
module mux2(
    input logic [3:0] d0, d1,
    input logic s,
    output logic [3:0] y
);
assign y = s ? d1 : d0;  // Holy crap, this is just like Rust
endmodule
```

So the `?` operator chooses based on the first expression. When `s == 1`, then it will pick the second expression `d1`, else it will pick `d0`. At a higher level of abstraction, a multiplexer is just a bunch of conditionals.

Slightly unrelated, the `?` operator is called a ternary operator because it takes three inputs.

You can increase the amount of options by using nested conditional operators. So this is like working around a bad syntax on a programming language.

```SystemVerilog
module mux4(
    input logic [3:0] d0, d1, d2, d3,
    input logic [1:0] s,
    output logic [3:0] y
); // You can see that now selecting a signal in a bus is like indexing an array. I think that it's very intuitive and can be applied to actual programming languages.
    assign y = s[1] ? (s[0] ? d3 : d2) :
    (s[0] ? d1 : d0);
endmodule
```

## 4.2.5 Internal Variables

Sometimes, you need to break a complex design into smaller chunks. To do this, we make internal variables. For example, the full-adder is a circuit with three inputs and two outputs. Here is the logical equation:

$$
S = A \oplus B \oplus C_{in}
$$
$$
C_{out} = AB + AC_{in} + BC_{in}
$$

We could actually define an intermediate variable and simplify the equation further by doing this:

$$
P = A \oplus B
$$

$$
G = AB
$$

And this would change the original full adder module into this:

$$
S = P \oplus C_{in}
$$

$$
C_{out} = G + C_{in}\left(A + B \right)
$$

$$
C_{out} = G + C_{in}P
$$

### Implementing this in SystemVerilog

```SystemVerilog
module fulladder(
    input logic a, b, cin,
    output logic s, cout
); // The things in the module declaration are basically the IO, but if it's not declared there, then it is an internal variable
    logic p, g;

    assign p = a ^ b;
    assign g = a & b;
    assign s = p ^ cin;
    assign cout = g | (cin & p);
endmodule
```

So the little weird thing that is a little specific to HDLs is that the order of declaration does not matter unlike a programming language where it does. This is because of the way the language is designed -> Not compiled for fast performance.