---
title: GooseLang - Custom Programming Language
tags:
  - To/Do
---
*Note: Made in good fun, and having your own programming language is cool~*

Over the past month, I've been working on creating my own programming language, GooseLang. It has everything to do with geese - while keeping all the things I love about Python, C, Java etc compiled into one!
  
I decided to build a sample compiler just to get a feel for how it's done. In this initial attempt, I worked on a single-pass compiler written in C for PL/0 based on [this tutorial](https://briancallahan.net/blog/20210814.html).
- [[../104 Subject-Specific Learning/104.2 Programming/compiledVsInterpreted|Compiled and Interpreted Languages]]: GooseLang is going to be an Interpreted language for an easier development time, written in C++ (also, interpreted).
- Do this without external libraries such as [[../104 Subject-Specific Learning/104.2 Programming/llvm|LLVM]]
>[!info] About [[PL⁄ 0]]
>It is an educational language similar to Pascal intended for students to learn more about creating compilers.

In this sample project, 
- I created a [[../104 Subject-Specific Learning/104.2 Programming/lexer]] which accepts PL/0 source code, outputs tokens and metadata. Additionally, it accepts valid tokens and rejects invalid tokens.

For GooseLang, there are two main approaches I could use to define it's syntax:
- [[../104 Subject-Specific Learning/104.2 Programming/backusNaurForm]] (BNF)
- [[../104 Subject-Specific Learning/104.2 Programming/parseTrees]]
where the first option is easier to start off with. 

I want to create a simple language with an extension of .gl that can:
1. Assign variables with type-checking
2. Declare structures, create instances and access fields
3. Perform "simple" mathematical operations
4. Print variables, values and more complex expressions with operators
5. Read values from console
6. Perform if-then statements

```
// Structs are called 'nests'
nest Person {
	// Define a variable of type
	String name;
	int age;
}

// Functions are introduced with the `flock` keyword
// Parameters are added after 'with' keyword, enclosed in open braces
flock main() {
	gather your_name;
	gather your_age;

	person = new Person[your_name, your_age];
	
	// Prints to console
	honk("Hey there %s", person.name);
	if (person.age < 25) {
		honk("You have %d years left", 25 - person.age);
	}
}
```
