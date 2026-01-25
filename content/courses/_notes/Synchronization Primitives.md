The focus is on: Synchronization Primitives

| Shared Objects      | Synch Primitives              | Atomic Instructions                                          |
| ------------------- | ----------------------------- | ------------------------------------------------------------ |
| [[Bounded Buffers]] | Mutex, Semaphore, CV, Monitor | [[Load and Store\|Load/Store]], Disable interrupts, Test&Set |

**Bounded Buffer**
Let's begin by defining what this class would look like.
```cpp
template<typename T>
class BoundedBuffer {
	private:
		std::vector<T> buffer;
		size_t head;
		size_t tail;
		size_t count;
		size_t maxSize;

	public:
		void produce(const T& item)
		T consume()
}
```

```c
void product(const T& item) {
	if (count == maxSize) {
		throw std::runtime_error("Buffer is full");
	}
	buffer[head] = item;
	head = (head + 1) % maxSize;
	count++;
}
```

```c
T consume() {
	if (count == 0) {
		throw std::runtime_error("Buffer is empty");
	}
	T item = buffer[tail];
	tail = (tail + 1) % maxSize;
	count--;
	return item;
}
```

**Atomic Mem. Op.**
Assume load and store operations are atomic
- no context switches in middle of load or store from or to a word
```c
/**THREAD 1*/
valueA = BUSY;
turn = 1;

while (valueB == BUSY && turn = 1);
// critical section

valueA = FREE;

/**THREAD 2*/
valueB = BUSY;
turn = 0;

while (valueA == BUSY && turn = 0);
// critical section

valueB = FREE;
```
- note: this is bad!
	- not the same code for both threads so hard to generalize for n threads
	- way too complex for such a simple example
	- this protects "one critical section"
- Instructions need to be executed in program order; compilers might rearrange however so we need memory barriers

Example:
```
// THREAD 1
// no dependency so can be reordered
p = someComputation();
pInitialized = true;

// THREAD 2
while (!pInitialized);
q = someFunc(p);
if (q != someFunc(p))
	panic();
```

This also ties into memory consistency in memory processors. In some "consistency models", this is not required. Memory consistency model defines the behavior of memory operations in multi-threaded operations.
```
// CPU 1
data = NEW;
flag = SET;

// CPU 2
r1 = flag;
if (r1 != SET) goto L1;
r2 = data;
```
The strongest model guarantees that all memory operations appear to execute in the same order as programmed, from the perspective of all processors. 

**Mutex**
There are two possible operations:
- mutex.lock(): wait until lock is free, then grab it
- mutex.unlock(): unlock and wake up anyone waiting

Rules of using mutex:
- always lock before accessing shared data
	- best place for locking is beginning of procedure
- always unlock after finishing with shared data
	- best place for unlocking is end of procedure
	- only the thread that locked mutex should unlock it
	- do not throw locked mutex to someone else to unlock

```
getP() {
	mutex.lock();
	if (P == NULL) {
		// some code
		p = temp;
	}
	mutex.unlock();
	return p;
}
```
This is expensive because every thread will lock/unlock, better to move it inside the if check.

```
getP() {
	if (P == NULL) {
		mutex.lock();
		// some code
		p = temp; // double-checked locking
	}
	mutex.unlock();
	return p;
}
```
Possible issues: 
> A pitfall in concurrent code where a data structure is lazily initialized by first, checking without a lock if it has been set, and if not, acquiring a lock and checking again, before calling the initialization function. With instruction re-ordering, double-checked locking can fail unexpectedly

How to implement this mutexes?
- on a uniprocessor, any sequence of instructions by one thread appears atomic to other threads if no context switch occurs in the middle.
- we can avoid context switching by 
	- avoiding voluntary context switches
	- preventing involuntary context switches by disabling interrupts
- the naive implementation is disable/enable interrupts when locking/unlocking
	- does not work well in multiprocessors
	- Real-time OS should guarantee timing (critical sections could be really long)
- Instead, introduce a lock variable which imposes mutual exclusion only during operations on that one variable