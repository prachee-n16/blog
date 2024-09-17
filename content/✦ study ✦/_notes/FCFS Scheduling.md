First come, first served; Also called FIFO i.e. first in, first out
- Simplest to implement as it can be easily managed with a FIFO queue
	- Similar to how it works in Lab 1 with `ready_queue`
Consider the utility of this:
- Pro
	- simple
	- fair
- Cons
	- short tasks get stuck behind last ones i.e. convoy effect

Example:
- Wait time for P1 is 0, P2 is 24, P3 is 27
- Average wait time is (0 + 24 + 27)/3 = 17
- Average response time is (24 + 27 + 30)/3 = 27

However, if we consider tasks in a different order, the metrics improve:
- Wait time for P2 is 0, P3 is 3, P1 is 6
- Average wait time is (0+ 3 + 6)/3 = 3
- Average response time is (3 + 6 + 30)/3 = 13
