- mathematical logic constructs that enable one to program a computer
	- syntax: language constructs
	- semantics: what does the syntax mean?
		- assumes/enables a model of computation such as Turing machines or mathematical functions
		- denotational, operational and axiomatic
- Programming language design is not easy as it must
	- enable programs to produce efficient code
	- enable secure and correct construction
	- discourage bad programming practices
	- make it easy to program the computer
	- increase productivity for programmers
	- help automate routine tasks
##### Types of Programming language
- Declarative: specify the what of the computation; runtime and compiler will figure out the how e.g. SQL, Matlab
	- Pure functional and logic-based languages are declarative e.g. Haskell (functional), Prolog (logic-based)
- Imperative: specify the what and how of the computation e.g. C/C++/Java/Python
##### Implementation
- Major strategies
	- Interpreter
		- reads it line-by-line and executes according to semantic without additional compilation step
		- Ultimately, little or no preprocessing where interpreter is a virtual machine
	- Compiler
		- extensive preprocessing and offline optimizations
	- Mixed: JIT Compilation
##### Brief History of High Level Languages
- FORTRAN I
	- John Backus had the idea to make programming easier by writing in a higher-level which later converts to assembly
	- FORTRAN gets it's name from FORmula TRANslation
	- By 1958, >50% of all software is in FORTRAN with development time halved

