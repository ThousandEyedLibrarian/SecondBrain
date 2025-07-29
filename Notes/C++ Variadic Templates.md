Variadic templates allow you to define functions or class templates that can take an arbitrary number of arguments (zero or more) of any type. They are primarily used to:

- Write generic code that handles multiple arguments flexibly.
- Avoid repetitive code for functions or classes with varying numbers of parameters.
- Enable compile-time recursion for processing argument lists.

The key syntax involves the `...` (ellipsis) operator, which indicates a parameter pack, and `typename...` or `class...` to declare a pack of types.

### Syntax and Core Concepts

#### Parameter Packs

A parameter pack is a template parameter or function parameter that represents a variable number of arguments. There are two types:

- **Template Parameter Pack**: Declared in a template definition, e.g., `typename... Args`.
- **Function Parameter Pack**: Declared in a function parameter list, e.g., `Args... args`.

Example:

```c
template<typename... Args> // Template parameter pack
void print(Args... args); // Function parameter pack
```

#### Pack Expansion

The `...` operator is used to expand a parameter pack into individual elements. For example, in a function call, `args...` expands to a comma-separated list of arguments.

#### Basic Example

```c
#include <iostream>

template<typename... Args>
void print(Args... args) {
    // Expands to print each argument
    ((std::cout << args << " "), ...); // Fold expression (C++17)
}

int main() {
    print(1, "hello", 3.14); // Outputs: 1 hello 3.14
    return 0;
}
```

Here, `Args` is a template parameter pack, and `args` is a function parameter pack. The fold expression `((std::cout << args << " "), ...)` expands to print each argument with a space.

#### Recursion for Processing Parameter Packs

Before [[C++17]], variadic templates often used [[Recursion]] to process arguments, as there was no direct way to iterate over a pack. A base case (non-variadic overload) is typically defined to terminate recursion.

Example:

```c
#include <iostream>

// Base case to terminate recursion
void print() {}

// Recursive case
template<typename T, typename... Args>
void print(T first, Args... rest) {
    std::cout << first << " ";
    print(rest...); // Recursively process the rest
}

int main() {
    print(1, "hello", 3.14); // Outputs: 1 hello 3.14
    return 0;
}
```

#### Fold Expressions (C++17)

C++17 introduced fold expressions, which simplify processing parameter packs by eliminating the need for explicit recursion. Fold expressions apply an operator (e.g., `+`, `<<`, `,`) to all elements in a pack.

There are two types of fold expressions:

- **Unary Fold**: Applies an operator to all elements in a pack.
- **Binary Fold**: Combines a pack with an initial value using an operator.

Syntax:

- Unary right fold: `(pack op ...)` or `(... op pack)`
- Binary fold: `(pack op ... op init)` or `(init op ... op pack)`

Example:

```c
template<typename... Args>
auto sum(Args... args) {
    return (args + ...); // Unary right fold
}

int main() {
    std::cout << sum(1, 2, 3, 4) << std::endl; // Outputs: 10
    return 0;
}
```

#### sizeof... Operator

The `sizeof...` operator returns the number of elements in a parameter pack at compile time.

Example:

```c
template<typename... Args>
void count_args(Args... args) {
    std::cout << "Number of arguments: " << sizeof...(args) << std::endl;
}

int main() {
    count_args(1, "hello", 3.14); // Outputs: Number of arguments: 3
    return 0;
}
```

### Constraining Variadic Args

You can constrain parameter packs using concepts ([[C++20]]) or [[Substitution Failure Is Not An Error (SFINAE)]] (pre-C++20) to restrict the types accepted.

Example with Concepts:

```c
#include <concepts>
#include <iostream>

template<typename... Args>
    requires (std::integral<Args> && ...)
void print_integers(Args... args) {
    ((std::cout << args << " "), ...);
}

int main() {
    print_integers(1, 2, 3); // Works
    // print_integers(1, "hello", 3); // Fails: "hello" is not integral
    return 0;
}
```