## Problem Statement
The generalized problem statement:
> Given a *memory pool* of size $2^n$ (bytes), design a memory allocator that can handle requests asking for an amount of size k of *contiguous* memory.
> The allocator allocates a block of (at least) size k and returns its address or declares no memory available.
> The allocator should also handle requests to free previously allocated memory.

We can consider free-space management as a sub-problem: 
> Keep track of the location and the size of the free space (some kind of list); (some kind of [[Free List|free list]])


# Mechanism

## Partition
We need to partition memory based on the requests we get from user programs:

Static partitioning is partitioning memory beforehand in fixed-size units.
- Great because it's easy to manage, allocation = first-free unit
- Bad because how to determine unit size
	- Too small? Allocations would fail!
	- Too large? Any request takes an entire unit and the rest is wasted.
Dynamic partitioning is partitioning memory based on requests in variable-sized units.
- Great because it minimizes internal fragmentation and allocates exactly size of request
- Bad because it's harder to manage as it creates hole in memory; There is enough memory but space is not contiguous 
A hybrid of static and dynamic partitioning is [[Binary Buddy System]]


> [!note] Fragmentation: Internal vs. External
> Internal Fragmentation: process is larger than the memory and fixed-sized memory blocks are designated for it
> External Fragmentation: process is removed and variable-sized memory blocks are designated for it
> 
> How can we mitigate external fragmentation?
> - Compaction: shuffle memory contents to place all free memory together in one large block
> 	- OS: Relocate processes so we have "contiguous" blocks of memory
> 	- For user level libraries e.g. malloc, this is harder! *Techniques to perform compaction without relocation exist with caveat*
> 		- See why here: [[mesh-pldi19-powers.pdf]] 
> 		- Basic explanation: In C/C++, where pointers are assigned to memory addresses, shifting memory around is dangerous since we need to update all these pointers. 
> - Swapping: Temporarily swap out memory contents to disk.
> 	- OS: rolls out inactive process to disk, releases the memory it holds. When process becomes active again, OS reloads from memory.
> 	- For user level libraries e.g. malloc, this is not practical due to huge performance overhead

Consider low-level mechanism for tracking free space: [[Free List]]

What are some basic strategies for managing memory?
1. Best-fit: Search through the free list and find units of free memory that are as big or bigger than requested size. Return the one that is **smallest** in group of candidates
	- Requires exhaustive search $O(n)$, tends to leave smaller units 
	- however, it's still trying to reduce wasted space by returning closest-size unit
2. Worst-fit: Opposite; Search for largest unit and return requested amount, keep the large chunk on free list
	- Try to leave big units free instead of small units
	- Requires exhaustive search $O(n)$, tends to empirically perform worse and "excessive" fragmentation
3. First-fit: Search for first unit that is big enough and returns requested amount, keeping remaining on free list
	- Fast since no need for exhaustive search
	- Sometimes this pollutes the beginning of free list with "small" units
4. Next-fit: Similar to First-fit, but search starts from last allocated unit
	- Spread the searches for free space through the list more uniformly
	- Performance is similar to first-fit
5. [[Binary Buddy System]]