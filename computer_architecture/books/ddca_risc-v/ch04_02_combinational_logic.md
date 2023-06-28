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