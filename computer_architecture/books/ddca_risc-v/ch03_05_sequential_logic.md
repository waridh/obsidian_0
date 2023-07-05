# 3.5.4 Metastability

In asynchronous inputs, you cannot guarantee that the input will come in at a time that isn't overlapping with the aperture. What happens when the input changes between $t_{setup}$ and $t_{hold}$? This input would violate the dynamic discipline, and the output would be undefined.

## Metastable State

When a flip-flop takes an input reading and the input is changing during the aperture, then the output will be between $0$ and $V_{DD}$ and potentially be in the forbidden zone. When it is in this zone, then it is what is called *metastable*. The reason it is called metastable is that the output could be balanced on this state until something comes to push it to the stable state, and the duration in this state is unbounded, meaning it could be indefinite.

![](../../../assets/Pasted%20image%2020230705140909.png)

## Resolution Time: $t_{res}$

This is the time it takes the output to change from a metastable state to a stable state. If the input changes outside the aperture, then the $t_{res}$ will be the same as $t_{pcq}$. If the input happens in the aperture time, then $t_{res}$ could be much longer. Here is the probability density function for the random variable:

$$
P\left( t_{res} > t \right) = \frac{T_0}{T_c}e^{- \frac{t}{\tau}}
$$

Where $T_c$ is the clock period, $T_0$ and $\tau$ are characteristic of the flip-flop. The equation is valid only for when $t$ is substantially longer than $t_{pcq}$.

The $\frac{T_0}{T_c}$ represents the probability that a conflicting asynchronous input will happen, and the probability decreased with the increase in $T_c$. $\tau$ is the time constant indicating how fast the flip-flop can move away from the metastable state. It has the do with the delay through the cross-coupled gates in the flip-flop.

# 3.5.5 Synchronizers

In the real world, not all inputs are going to be synchronous, for example, human inputs are guaranteed to be asynchronous. If the system is not build to handle those types of input, failures and lock ups can happen. Although not completely preventable, there are ways of minimizing the chances of creating erratic behaviour in a systems like this. One of those ways are *synchronizers*.

Functionally, synchronizers will take an asynchronous input D, and a clock CLK. It makes an output Q within a bounded amount of time<!--Specified by the clock??-->. The output will have a valid logic level with an extremely high probability. If D is stable during the aperture, Q should take on the same value as D. If D changes during the aperture, Q may either take on a HIGH or LOW value, but must not be metastable.