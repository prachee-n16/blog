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
		void produce(const T& item);
		T consume();
}

void produce(const T& item) {
	if (count == maxSize) {
		throw std::runtime_error("Buffer is full");
	}
	buffer[head] = item;
	head = (head + 1) % maxSize;
	count++;
}

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