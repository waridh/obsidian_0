# 4.4 Sequential Logic

HDL synthesizers recognize certain idioms and turn them into specific sequential circuits. We are here to use the proper idioms to describe the registers and latches.

## 4.4.1 Registers

Commercial systems all use registers now. They are usually built with a positive edge-triggered D flip-flop. Here is an example implementation of a d-ff in SystemVerilog:

```SystemVerilog
module flop(input logic clk,
           input logic [3:0] d,
           output logic [3:0] q);

    always_ff @(posedge clk)
    q <= d;
endmodule
```

So in general, a SystemVerilog `always` statement is written in the form:

```SystemVerilog
always @(sensitivity list)
    statement;
```

This statement will only occur when the event specified in the sensitivity list occurs. This is like a while loop that will only continue on a positive edge on the clock.

In our example `q <= d`, `q` copies the state of `d` on a positive edge of the `clk`, and otherwise will remember the old state of `q`. A sensitivity list is also called a stimulus list.

`<=` is called a nonblocking assignment. It's like a regular `=` but there are some nuance that makes it usable on sequential logic.

The `always` statement can be used to imply `flip-flops`, `latches`, or combinational logic, depending on the sensitivity list and statement. Sometimes, all this flexibility makes it easy to produce wrong hardware. This is why SystemVerilog introduced `always_ff`, `always_latch`, `always_comb` to basically increase the type checking. `always_ff` acts like a regular `always` but it will always implicitly imply a `flip-flop`. It will produce a warning if anything else is implied.

## 4.4.2 Resettable Registers

