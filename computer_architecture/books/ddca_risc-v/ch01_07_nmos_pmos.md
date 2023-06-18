# 4. nMOS and pMOS Transistors

## What are MOSFETs

MOSFETs are built on silicon wafers through an ever increasingly complicated process, where silicon and silicon dioxide are grown in the nm scale. The advancement in this process has made it very inexpensive to produce billions of transistors at a time.

When the process is complete, and the wafer is cut into rectangles called **chip**, or **dice** where testing happens, and then packaging. In the completed package, metal pins connect the die to the circuit.

## How MOSFETs work

The MOSFET sandwich is layered as follows. There is a conducting layer placed on top of an insulating layer, that is sitting on the silicon, which is also called the substrate. The conducting layer is called a *gate* and in modern processes, it is made of **polycrystalline silicon**, however, in the past it was made out of metal-oxide-semiconductor. A shift in material occurred because polycrystalline silicon is able to withstand higher temperature that is used later in the process. That insulating layer is usually silicon dioxide (glass)(**oxide** is the industry shorthand). 

The sandwich creates a capacitor, with the silicon dioxide acting as the dielectric.

### There are two types of MOSFETs:
1. nMOS
2. pMOS

![Cross section illustration of MOSFET](../../../assets/ddca/Pasted%20image%2020230618132032.png)

#### nMOS

There are regions of n-type dopant besides the gate, called the source and drain. The main substrate of the nMOS are p-type. 

##### Operations

The substrate of the system is usually tied to ground (GND), which is the lowest voltage of the system.
1. When the gate is also 0V, the diode between the source or the drain to the substrate are reverse biased, and since either the source or the drain has a non-negative bias. This means that current cannot flow from the source to the drain, and thus the transistor is turned off.
2. When the gate voltage is raised to $V_{DD}$, an electric field is created that will pull positive charge to the top plate, and negative charge to the bottom plate. When enough voltage, there will be so much negative charge on the bottom plate that a region of the p-type substrate will act like an n-type substrate. This region is called a *channel*, and it will give a continuous path from the n-type source to the n-type drain. Now electrons from the source can flow to the drain, and thus, the transistor is ON.

![Function of nMOS](../../../assets/ddca/Pasted%20image%2020230618135229.png)

#### pMOS

Literally just the opposite of nMOS. The substrate is tied to $V_{DD}$, so when the gate is also at $V_{DD}$, the transistor is turned OFF, and when the gate is $GND$, the channel inverts to a p-type substrate, and the transistor turns ON.

The gate voltage used to turn on the transistor is called the *threshold voltage* and is denoted with $V_t$. The threshold voltage usually range from 0.3 to 0.7 V.

## Flaws

MOSFETs are great, but they are not the perfect switches. nMOS are great at passing 0s, but 1s are not perfect. When the gate of an nMOS is at $V_{DD}$, the source will only swing between 0 and $V_{DD}-V_t$ when its drain range from 0 to $V_{DD}$.

The same is true with pMOS, as it passes 1s well, but 0s poorly. Of course, engineers have developed ways to build logic with transistors only using their good modes.

## MOSFET usage

In computing, MOSFETs are usually used as voltage controlled switches. The *gate* voltage changes the state of the MOSFET between ON or OFF, which is really the state of the connection between the *source* and the *drain*. This physics is why this type of transistor is dubbed as *field effect transistors*.

## Design

nMOS needs a p-type substrate and pMOS need an n-type substrate. To build both on the same chip, manufacturers will usually start with a p-type substrate, and implant n-type regions called wells where they need to use pMOS. The process that uses both nMOS and pMOS are called Complimentary MOS, or **CMOS**. In the modern day, **CMOS** is commonly used in mostly all transistor applications.

## Summary diagram

![Circuit icon for nMOS and pMOS](../../../assets/Pasted%20image%2020230618140443.png)

# CMOS NOT Gate

The 

## Pointers

| Previous | [Home](ddca_risc-v_abstract.md) | Next |
| -------- | ------------------------------- | ---- |
