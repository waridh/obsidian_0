# Latches and Flip-Flops

Bistable elements are needed when trying to build components from the fundamental level. Flip-flips and latches hold these places. Let's do a little review on them.

Quick definition: When an output of an element goes into the input of another and vice versa, they are defined as *cross-coupled*.

*Bistable* is when a circuit has two stable states. Once you start building up more complex systems, there are going to be N stable states, which can convey $\log_2N$ bits of information.

## 3.2.1 SR Latch

Very simple sequential circuit, an SR latch is two cross-coupled NOR gates.

![](../../../assets/Pasted%20image%2020230705172547.png)

Functionally, it uses the set and reset signal to control the outputs of both $Q$ and $\bar{Q}$. Here is a little truth table for it:

| S   | R   | Q   | $\bar{Q}$ |
| --- | --- | --- | --------- |
| 0   | 0   | X   | X         |
| 0   | 1   | 0   | 1         |
| 1   | 0   | 1   | 0         |
| 1   | 1   | 0   | 0         | 

I have done a circuit design course before doing this, so I have an idea of how it is done.

## 3.2.2 D Latch

To improve upon the SR latch, and simplify the interface, we now have the D flip flop, which controls what it should change to, and how it should change. This is done by binding the S and R input with a new input D with an intermediate of $\bar{D}$. The clk signal was also added to control when the state should change.
