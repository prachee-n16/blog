- The first step in the process is **recognizing words**
	- words are the smallest unit above letters
- Example: `This is a sentence`
	- We start by differentiating the "sequence of bits" that represent individual words vs. separators (i.e. spaces, period)
- Lexical analyzers divide the program into words or tokens
	- `if x == y then z = 1; else z = 2;`
		- We need to ensure the tokens are legal! 
- The tokens can have the following units:
	- keywords
	- variables
	- operators
	- constants
	- punctuations
	- white spaces

See: [[Lexer]]