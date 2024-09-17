*Dynamic Random Access Memory*

When a bit needs to be stored in memory, the transistor is used to charge or discharge the capacitor. The wordline or bitline is used to do the charging. 
- Charged capacitor --> 1, Discharged capacitor --> 0

When reading/writing, the wordline goes high and transistor connects capacitor to bitline. The value on the bitline is stored in the capacitor.

Since charge in capacitor is too small to read, a sense amplifier is used. 
- It detects small differences in charge; thus, outputs the digital logic repr. it stores

**Note: Reading destroys the charge on capacitor.** Solution: Pre-charge to put the value read from bitline back to capacitor.

![](https://www.allaboutcircuits.com/uploads/articles/intro_to_DRAM1.png)

