The structure (phases) of a compiler
```mermaid
graph TD
A[input program] --> B[lexical analyzer]
B -- tokens --> C[parser]
C -- AST --> D[semantic analysis i.e. type checking]
D -- IR i.e. intermediate representation --> E[code optimizations]
E -- address format --> F[code generation]
F --> G[output program]
```

- [[Lexical Analyzer]]
- [[Parsing]]
- [[Semantic Analysis]]
- [[Code Optimizations in Compilers|Code Optimizations in Compilers]]
- [[Code Generation in Compilers|Code Generation]]