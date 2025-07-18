## Namespaces

Namespaces are one of the tools in [[C++]] to organise code by providing a named scope for different identifiers, like [[Functions]], [[C++ Classes]], and variables. 

```cpp
namespace MyNamespace {
    int aFunction() {
        // function implementation
    }
}
// to use the function
MyNamespace::aFunction();
```

## Include Guards

Include guards are a tool for preventing multiple inclusions of a header file in your project. They consist of preprocessor directives that conditionally include the header file only once, even if it’s included in multiple places.

```cpp
#ifndef MY_HEADER_FILE_H
#define MY_HEADER_FILE_H

// Code here

#endif // MY_HEADER_FILE_H
```

## Header and Source Files

Separating your implementation and declarations into header (_.h) and source (_.cpp) files is a key aspect of structuring your codebase in C++. Header files usually contain class and function declarations, while source files contain their definitions.

- MyClass.h

```cpp
#ifndef MY_CLASS_H
#define MY_CLASS_H

class MyClass
{
public:
    MyClass();
    int myMethod();
};
 
#endif // MY_CLASS_H
```

- MyClass.cpp

```cpp
#include "MyClass.h"

MyClass::MyClass() {
    // constructor implementation
}

int MyClass::myMethod() {
    // method implementation
}
```

### Separate [[Compilation]]

C++ allows for separate compilation, which means that each source file can be compiled independently into [[Object Files]] file. These object files can then be linked together to form the final executable. This provides faster build times when making changes to a single source file since only that file needs to be recompiled, and the other object files can be reused.

```
# Compile each source file into an object file
g++ -c main.cpp -o main.o
g++ -c example.cpp -o example.o

# Link object files together to create the executable
g++ main.o example.o -o my_program
```

See also:
- [[C++]]
- [[Namespaces]]
- [[C++ Compilation]]