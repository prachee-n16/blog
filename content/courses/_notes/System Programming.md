**Systems Programming** which deals with creating software that interact directly with the [[Operating System]], e.g. programs include
- [[File Manipulation]]
- Communication
- Processes and Thread Management
OS will sometimes not allow programs to do things, and instead, we need to ask the OS to do it.

**Concurrency** - A program is said to be concurrent if it can support two or more actions in progress at the same time.
**Parallelism** - A program is said to run in parallel if it can have two or more actions execute simultaneously

Note, a program with concurrency problem will see the following errors:
1. Consistently the wrong answer every single time  
2. Different on consecutive runs with the same input, or  
3. Correct some of the time but incorrect some of the time