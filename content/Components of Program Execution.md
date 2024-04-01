---
tags:
  - Areas
  - OperatingSystems
  - to-complete
  - ece252
---
To execute a program, the components for a minimal set are:
- Main memory
- System Bus
- Processor
	- Within this, we have a I/O communicating data to us that requires some processing
	- Central Processing Unit (with a Control Unit and ALU) communicates with memory unit.

**Processor**
- Brain of the computer which fetches instructions, decodes them, executes them (a cycle which repeats infinitely)
- Different steps may be completed in parallel (pipeline) --> ECE 222
- The largest unit in a processor is the word: 
	- 32-bit computer -> 32-bit word, 64-bit computer -> 64-bit word

**CPU**
- CPU instructions are specific to the processor (x86, ARM, RISC, MIFS)
	- Some instructions are only available in "supervisor" mode and running it in user mode is an error.
	- When running our programs, we can't ask to "close" the computer or read input from keyboard directly. What if we do the wrong thing, crash the computer in a while loop forever?
- CPUs have storage locations called registers
	- These will store data or instructions. A great analogy is if memory is a bookshelf, these are your pockets - quick access to data
	- Management of registers is partially the role of the OS. 

**Critical Registers in CPU**
- Program Counter - address of next instruction. 
	- The reason we have this is because if statements or for loops, it's not always sequential. We might need to branch back to a previous line. 
- Status Register - Array of bits to indicate flags. For example, if we are in supervisor mode, if there's low power
- Instruction Register - Instruction most recently fetched, so in decode stage, we can refer to this
- Stack Pointer - Where the local data is kept. We really care about this because all our local variables are here in memory
- General Purpose Registers - store data, addresses etc. Basically, pockets to put in data to use later.

How do we inform the computer of something that just happened? **[[Interrupts]]**
- CPU needs data but it takes a variable amount of time to get that information, while I work on something else.
	- Interrupt: Get a notification when data has arrived
- Polling is separate: Check periodically if the data has arrived
