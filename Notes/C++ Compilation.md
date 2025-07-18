Edit -> Compile -> Execute cycle

### Let's run through the behind the scenes of this

1. First off your **pre-processor** comes along and runs through all the # statements at the top of your file, eg include, define, ifndef, endif, etc.
2. Then your **compiler** translates all the raw code and turns it into assembly instructions.
3. Your **assembler** comes in and partially compiles an individual cpp file into an object file, which is a machine code file (1s and 0s) that is missing its links to vars, funcs, methods that the code requires to actually run, in their place it contains a *'symbol table'* for all the missing links.
4. Finally, your **linker** connects all the missing links between the object files by matching the symbols in each of the symbol tables of the object files, after which it becomes a full executable.

### Why is this handy to know?

Well bud, you can do a partial compilation to only spend time compiling the part of a file or project that you've changed, to do this you use the -c flag in gcc, look it up online idgaf. 

You don't need to spend the time and resources recompiling the entire project, you can simply compile the change.

You can also make libraries using this method, a library is typically an object file that is then linked into an individual project using a linker per above.  Uses the linker flag -l, look it up.

## Going Deeper on C++ Compilation

### Stages of Compilation in C++

Remember, the process of [[Compilation]] in C++ can be divided into four primary stages: 
1. Preprocessing
2. Compilation
3. Assembly
4. Linking 

#### 1. Preprocessing

The first stage is the preprocessing of the source code. Preprocessors modify the source code before the actual compilation process. They handle directives that start with a `#` (hash) symbol, like `#include`, `#define`, and `#if`. In this stage, included header files are expanded, macros are replaced, and conditional compilation statements are processed.

**Code Example:**

```cpp
#include <iostream>
#define PI 3.14

int main() {
    std::cout << "The value of PI is: " << PI << std::endl;
    return 0;
}
```

#### 2. Compilation

The second stage is the actual compilation of the preprocessed source code. The compiler translates the modified source code into an intermediate representation, usually specific to the target processor architecture. This step also involves performing syntax checking, semantic analysis, and producing error messages for any issues encountered in the source code.

**Code Example:**

```cpp
int main() {
    int a = 10;
    int b = 20;
    int sum = a + b;
    return 0;
}
```

#### 3. Assembly

The third stage is converting the compiler’s intermediate representation into assembly language. This stage generates assembly code using mnemonics and syntax that is specific to the target processor architecture. Assemblers then convert this assembly code into object code (machine code).

**Code Example ([[x86 Architecture]] [[Assembly]]):**

```assembly
mov eax, 10
mov ebx, 20
add eax, ebx
```

#### 4. Linking

The final stage is the linking of the object code with the necessary libraries and other object files. In this stage, the [[Linkers]] merges multiple [[Object Files]] and [[Object Code Libraries]], resolves external references from other modules or libraries, allocates [[Memory]] addresses for functions and variables, and generates an executable file that can be run on the target platform.

**Code Example (linking objects and libraries):**

```
$ g++ main.o -o main -lm
```


See also:
- [[Makefiles]]
- [[Compiler Drivers]]


