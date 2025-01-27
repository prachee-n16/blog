---
title: Preprocessor Directive
---
These are lines in the programs that start with #, which the preprocessor will resolve before any other regular statements. Some common examples of this are:

**macro definitions, `#define`**
The syntax is `#define identifier replacement` and it replaces the identifier with the established replacement. It can be undefined with `#undef`.

**conditional inclusions `#ifdef` etc.**
These will run code only if a parameter has been defined, useful for debugging purposes
```cpp
#ifdef DEBUG
cout << "test" << endl;
#endif
```

Include directives such as `#include <header>` or `#include "file"` includes the file. However, 
if `#include` a header more than once, it will result in problems such as compiler errors or redefinitions.

Include guards are put around the entirety of the header file to prevent this issue. Alternatively,  `#pragma once`can be used to tell the preprocessor to skip the current header if it has already been included. 