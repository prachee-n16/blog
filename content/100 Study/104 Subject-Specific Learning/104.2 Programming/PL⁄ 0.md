It is an educational language similar to Pascal intended for students to learn more about creating compilers.

Here's the entire syntax of PL/0.
```
program		= block "." .
block		= [ "const" ident "=" number { "," ident "=" number } ";" ]
			  [ "var" ident { "," ident } ";" ]
			  { "procedure" ident ";" block ";" } statement .
statement	= [ ident ":=" expression
			  | "call" ident
			  | "begin" statement { ";" statement } "end"
			  | "if" condition "then" statement
			  | "while" condition "do" statement ] .
condition	= "odd" expression
			  | expression ( "=" | "#" | "<" | ">" ) expression .
expression	= [ "+" | "-" ] term { ( "+" | "-" ) term } .
term		= factor { ( "*" | "/" ) factor } .
factor		= ident
			  | number
			  | "(" expression ")" .
ident		= "A-Za-z_" { "A-Za-z0-9_" } .
number		= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" .
```