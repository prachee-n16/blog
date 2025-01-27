Systems whose correctness depends on both temporal aspects and functional aspects
- temporal aspects are specified through deadline
	- results need to be produced before deadline, otherwise it's too late and considered a failure

**Types of real-time systems**
- Soft
	- try to meet all deadlines
		- system does not fail if a few deadlines are missed
- Firm
	- result has no use outside deadline window
		- tasks that fail are discarded
- Hard
	- must always meet all deadlines window
		- system fails if deadline window is missed
