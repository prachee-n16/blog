Regular Expression (Regex) is a sequence of characters that specifies a pattern in any given text (string). 
###### BASIC REGEX CHARACTERS

```
regex ::= letter          # match the exact letter
          ( regex )       # group pattern and match
          regex?          # match zero or one of the pattern
          regex+          # match one or more of the pattern
          regex*          # match zero or more of the pattern
          regex regex     # match sequence of patterns
          regex | regex   # match either pattern (choice)
          
letter ::= char           # match the exact character
          .               # match any character
          [ char+ ]       # match any character in the group
          [^ letter+ ]    # match any character not in the group

char ::= (a single character)
```
