---
tags: serdes, communication
---

# Overview

A pair of function blocks:
- Used in high speed communication as a solution for limited input/output.
- Converts between serial data and parallel data interface in each direction.
- Primary use is to transmit data over a single line/lane in order to minimize the number of I/O pins and interconnects. <!-- Similar to Multiplexers-->

## Generic function

There are two functional blocks in the basics of SerDes

1. Parallel in Serial Out (PISO)
	1. Usually has a parallel clock input, a set of data input lines, and input data latches
	2. It may use internal or external phase-locked loop to multiply the incoming parallel clock up to serial frequency.
	3. The simplest form has a single shift register that receives the parallel data once per parallel cycle and shifts it out at a higher serial clock rate. Implementation may also make use a double-buffered register to avoid metastability when transferring data between clock domain.
2. Serial in Parallel out (SIPO)
	1. Usually has a receive port output, a set of data output line and output data latches
	2. The receive clock may have been recovered from the data by serial clock recovery technique,  but SerDes that do not transmit a clock use reference clock to lock the PLL to the correct Tx frequency, avoiding low harmonic frequencies present in the data stream.
	3. The SIPO block divides the incoming clock down to the parallel rate.
	4. There is usually two registers connected as a double buffer. One register to clock the serial stream, and the other for slower, parallel side.

There are four different SerDes architecture:
1. Parallel clock SerDes
2. Embedded clock SerDes
3. 8b/10b SerDes
4. Bit interleaved SerDes

Some SerDes  will have encoding/decoding blocks. Usually 8b10 and used for easier clock rate recovery in the receiver, to provide framing, and to provide DC balance.

### Source Synchronous Clocking

Parallel clock SerDes is usually used to serialize a parallel bus input along with data address and control signals. It is sent with a reference clock.

### Embedded Clocking

The clock and data is sent in a single stream.
- One cycle of the clock signal is sent first, followed by the data bit stream.
	- This causes a periodic rising edge at the start of the bitstream.
	- This makes it very easy to recover the clock from the bitstream.

### Data Encoding

- 8b10b SerDes maps each data byte to a 10-bit code (character) before serializing the data.
- The deserializer uses the reference clock to monitor the recovered clock rom the bit stream.
- The clock data is synthesized into the data bitstream, the serializer (transmitter) clock jitter tolerance is lower than the other methods.
- The control code allow framing, usually on the start of the packet.
- This is defined by Gigabit Ethernet specification

### Bit interleaved SerDes

Bit interleaved SerDes multiplexes several slower serial data streams into a faster serial stream, and then the receiver demultiplex the faster bit stream back to slower streams.

# Summary

Acts a lot like a multiplexer, but more automated, and without a select signal.

# Pointers

- [Home](communication_abstract.md)

# Citation

- [Wiki page](https://en.wikipedia.org/wiki/SerDes)