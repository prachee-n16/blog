There are 2 types of parsing techniques:
- Top-down parsing
	- Looks at the highest level of the parse tree and works down using rules of grammar
	- uses Left Most Derivation
		- We derive the string by deriving value of the leftmost non-terminal symbol, and moving left to right
	- Example: recursive descent parser
- Bottom-up parsing
	- Looks at the lowest level of parse tree and works up using rules of grammar; We start with tokens and construct parse tree by working from the leaves upwards (i.e. reducing the string to a start symbol)
	- uses Right Most Derivation
		- Since we are reducing the string, the rightmost non-terminal character is reduced first 
	- Example: ItsShift Reduce parser

