This is a hybrid approach of static and dynamic partitioning.

It's more flexible than static partitioning since it doesn't have to be fixed-size or require partitioning. It's less flexible than dynamic since blocks are allocated at granularities of $2^k$ bytes.

Free memory is first conceptually thought as a big space of size $2^n$. For a given request of size $S$, search for free space *recursively*. 
- We divide the free space by two until a block that is just big enough to accomodate the request is found. 
- Return that block, with the other half being called buddy of this block
- Buddies of size $2^k$ that become unallocated are coalesced back in a block of size $2^{k+1}$

Pros: Speed
- no exhaustive search for allocation
- coalescing becomes easy
Cons: Suffers both internal and external fragmentation

**Implementation**
- Binary-tree representation of Buddy System: Represent each $2^k$ byte block with a binary tree node
	- The entire memory pool is initially represented as a single $2^n$ byte block i.e. root
	- Assume a minimum block size of $2^i$ bytes
		- This limit allows us to calculate the max height of the tree as $h = n - i + 1$
	- Level $k$ has most $2^k$ nodes of size $2^{n-k}$ bytes; 
	- The max number of nodes in the entire tree: $2^h - 1$
- Naive implementation: Linked data structure with points (but pointer chasing is slow)
- Better implementation: Implement the full tree through bit array
	- allocate a bit array of size  $2^h - 1$ i.e. maximum number of nodes in the tree
	- Let 1 represent (partially) allocated or 0 represent free or not allocated
- Use bit array indexing to find the node in the tree!

Allocation: Given the size of the program, 
- Figure out proper block size, i.e. size = 100K will go into size = 128K
- Figure out which level that block will be at
- If there is a free block, use or otherwise, go above a level and look again
- Split the block in 2 and return 1.
- High-level algorithm:
	- for each level, implement a doubly linked list of free blocks with a head pointer
	- to allocate a block of size S, find k such that $2^{m-k-1} < S \leq 2^{m-k}$ 
	- if the level k list is not empty, use the head of the list
- otherwise, decrease the level until a non-empty list at level k' is found and split the head till we reach k
	- If none are found, this operation fails.
- Time complexity: O(h)

Deallocation: To find the size of the block without a header, 
- Start from the corresponding node at the bottom level and recursively check whether it is allocated i.e. Bit == 1
	- The first one that is allocated is the block to free. 
- High-level algorithm:
	- Start at level $k = h - 1$ i.e. level of leaf node
	- Compute $x = (addr - base_addr)/2^i$
	- If the bit for the $x_{th}$ node at level $k == 1$, stop
	- Otherwise, set $k = k -1$ and $x = x/2$ and repeat the last step
- Once x, k have been found, set the bit to be 0. If the bit for it's buddy is also 0, move to parent at level $k - 1$ and repeat (coalescing)
- Time complexity: O(h)
