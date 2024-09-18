This is a sentence; we know this because it follows the rules set out by the English language. There is an order we expect to see. 

This tokenizes as: 
```
This      line    is      a          long        sentence 
[article] [noun]  [verb]  [article]  [adjective] [noun]  
```
If *article + noun* is the subject, *article + adjective + noun* is the object, then
`subject + verb + object = sentence`

The compiler does a similar process to get information on what needs to be done. 

Example: `if x == y then z = 1; else z = 2;`
We can draw a [[Parse Trees]] to understand what needs to be done:
![[Parse Tree Example 1.png]]
This is a top-down approach: We start from the inputs and rules we have defined, matching them to get our conclusion. Note: this method is inefficient.
See more: https://www.cs.mcgill.ca/~cs520/2022/slides/6-bottom-up-parsing.pdf
- [[Parsing techniques]]

Related: [[Parser]]