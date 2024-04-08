*Note: Made in good fun, and having your own programming language is cool~*

Over the past month, I've been working on creating my own programming language, GooseLang. It has nothing to do with geese - just has all the things I love about Python, C, Java etc compiled into one!
  
I decided to build a sample [[Compilers|compiler]] just to get a feel for how it's done. In this initial attempt, I worked on a single-pass compiler written in C for PL/0 based on [this tutorial](https://briancallahan.net/blog/20210814.html).

>[!info] About [[PL⁄ 0]]
>It is an educational language similar to Pascal intended for students to learn more about creating compilers.

In this sample project, 
- I created a [[Lexer]] which accepts PL/0 source code, outputs tokens and metadata. Additionally, it accepts valid tokens and rejects invalid tokens.