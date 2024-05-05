---
title: Digital Logic Gate
---
**Digital Logic Gates**
The Buffer (simplest digital logic gate) serves two purposes
- Create an output signal B that is same as signal A without placing a "load" on signal A
	- Implies that this strengthens signal A, connected to power supply/ground to maintain the signal
- Used as a delay element
![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSMk_f5P5r7DMewiZ-raKm9ne0N0AP71VAN7iJt7y95Rg&s)

The symbol here lacks a bubble, which typically stands for inversion
- Note: A signal named `CLK_n` indicates it's in active low (inversion!)

The inverter is another simple logic gate that inverts the value of signal A.
![](https://www.gsnetwork.com/wp-content/uploads/2023/01/inverter-truth-table.jpg)
Notation: The over-bar is another way to show it's inverted. Apostrophe or exclamation mark exists because it's difficult to type this into textbooks. HDL's have the same issue!

The AND gate is a two-input digital logic gate, where output signal C is 1 when both input signals A and B are 1.
![](https://cdn.shopify.com/s/files/1/0611/1644/9018/files/AND_Logic_Gate_symbol_with_truth_table_600x600.png?v=1681242963)
A triple-AND gate is a cascading gate system with two AND gates one after another. In latex,
$$C = A \cdot B$$

The OR gate, another two-input logic gate, outputs signal C as 1 when either A or B is 1.
![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT2KZzOUrMGVBqoawL6GWssWNIkkATSd66-HlZonzFs6w&s)

The XOR gate, another two-input logic gate, outputs signal C as 1 when exactly one input is value 1.
![](https://cdn.shopify.com/s/files/1/0611/1644/9018/files/XOR_Logic_Gate_symbol_with_truth_table_480x480.jpg?v=1681931209)

Why is this important? In latex,
$$C = A \oplus B$$
==Parity is a technique that checks whether data has been lost or written over when it is moved from one place in storage to another or when it is transmitted between computers.==
- Even parity bit generator by producing an output that will ensure input bits has an even number of values of 1.
- Can be used as controlled inversion (need to understand how again)

**Totem Pole Output Drivers**
- Always output a digital value (either 0 or 1) and can never be turned off
- They are not suitable for "shared" bus signals, as we want to avoid signal conflicts as shown below:
See: [Magic Smoke](https://en.wikipedia.org/wiki/Magic_smoke)

Open Drain Digital Logic Gate and Open Source Digital Logic, where output 1 and 0 is replaced with Z respectively.

Review of Tri-state buffers, in the eyes of Tri-state output drivers.
![](https://i.ytimg.com/vi/X2HPjppH7Rs/maxresdefault.jpg)
Here, B is a control input and when it's 0, output signal is Z state. Otherwise, when B is enabled, this is the equivalent of the buffer shown above. 
- In the second and third table, we show a simplified truth table.

Registers are edge-triggered devices, Latches are level-triggered devices. 
- In a register, on the rising edge of the CLK signal, output Q is updated to input D
- In a latch, when enable is 1, output Q is updated to input D.
- Any other time, output Q reflects the stored value
![](https://image1.slideserve.com/2400301/latch-versus-register-l.jpg)

D-registers are preferred because it prevents additional noise from being added in, it's better synchronization and eliminates race conditions.