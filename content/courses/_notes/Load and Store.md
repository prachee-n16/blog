Atomic operations i.e. cannot be interleaved with or split by other operations
- So, if I am loading or storing from or to a word, no context switches are allowed during this time.
In x86 architecture, 
- A variable is naturally aligned if it's memory address is a multiple of it's size.
	- e.g. 2-byte variable should be aligned to addresses that are multiples of 2, 0x1002, 0x1004 etc.
- Naturally aligned variables benefit from load and store operations
	- Reading and writing from 0x1002 is atomic by nature. This guarantee allows data consistency and integrity

How does mutual exclusion with atomic load/store work?
Assume there are two threads currently executing,
```cpp
// Thread A
valueA = BUSY;
turn = 1;

while(valueB == BUSY && turn == 1);

// critical section
valueA = FREE;
```

```cpp
// Thread B
valueB = BUSY;
turn = 0;

while(valueA == BUSY && turn == 0);

// critical section 
valueB = FREE;
```
