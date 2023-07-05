# 3.5.4 Metastability

In asynchronous inputs, you cannot guarantee that the input will come in at a time that isn't overlapping with the aperture. What happens when the input changes between $t_{setup}$ and $t_{hold}$? This input would violate the dynamic discipline, and the output would be undefined.

## Metastable State

When a flip-

# 3.5.5 Synchronizers

In the real world, not all inputs are going to be synchronous, for example, human inputs are guaranteed to be asynchronous. If the system is not build to handle those types of input, failures and lock ups can happen. Although not completely preventable, there are ways of minimizing the chances of creating erratic behaviour in a systems like this. One of those ways are *synchronizers*.

Functionally, synchronizers will take an asynchronous input D, and a clock CLK. It makes an output Q within a bounded amount of time<!--Specified by the clock??-->. The output will have a valid logic level with an extremely high probability. If D is stable during the aperture, Q should take on the same value as D. If D changes during the aperture, Q may either take on a HIGH or LOW value, but must not be metastable.