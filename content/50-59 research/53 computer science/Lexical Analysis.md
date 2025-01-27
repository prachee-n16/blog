The goal of lexical analysis is to partition input string into substrings, where each substring represents a **token**.

Tokens correspond to sets of strings with specific rules:
- **Identifier:** Strings of letters or digits, starting with a letter. 
- **Integer:** A non-empty string of digits. 
- **Keyword:** Specific reserved words (e.g., `"else"`, `"if"`, `"begin"`, ...). 
- **Whitespace:** A non-empty sequence of blanks, newlines, and tabs.

To design a lexer:
- Define a finite set of tokens where choice of tokens depends on language, parser and items of interest
- Describe which strings belong to each token

To implement a lexer:
- Recognize substrings corresponding to tokens
- Return the value or lexeme of the token
