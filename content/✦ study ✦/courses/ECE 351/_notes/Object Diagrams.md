They visualize the state of an executing program; depicts objects, stack frames, heap and pointers to a specific time point during program execution.

![[Object Diagram - Key.png]]

An example to construct object diagram - Consider this code structure, written in Java:
```java
class BigFoo {
	static Foo x;
	static Foo y;

	public static void main(String[] args) {
		init();
	}

	static void init() {
		x = new Foo();
		Foo bar1 = new Foo();
		Foo bar2 = new Foo();
		x.a = bar1;
		x.b = bar2;
		bar1.c = bar2;
		bar2.c = bar1;
		// object diagram 1
		
		y = new Foo();
		y.attack(x);
		// object diagram 2
	}
	
}

class Foo {
	SmallFoo a;
	SmallFoo b;
	SmallFoo c;

	void clear(Foo f) {
		f.a = null;
		f.b = null;
	}
}
```

