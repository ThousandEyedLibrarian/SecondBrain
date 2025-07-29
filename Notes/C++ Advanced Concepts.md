I don't care whether some esoteric jackass thinks these constitute advanced or not, in the regular course of learning [[C++]] you won't come across these in beginner material but they can make life much easier in many situations.

### Restricting [[C++ Templates]] [[Functions]] By Type

A.K.A [[Substitution Failure Is Not An Error (SFINAE)]].

1. Create a template function
2. Create a struct to represent your acceptable types
3. Create the template specialisation functions for those types only

Member substitution allows the program to substitute for only those types and throw otherwise.

*When a substitution in a template fails, it does not cause a compilation error. Instead, the compiler tries other overloads or template specialisations.*

This allows **selective template instantiation** based on **type traits, function availability, or expressions**.

```cpp
#include <iostream>
#include <type_traits>

// Overload for integer types
template <typename T>
typename std::enable_if<std::is_integral<T>::value>::type foo(T) {
    std::cout << "Integral type\n";
}

// Overload for floating-point types
template <typename T>
typename std::enable_if<std::is_floating_point<T>::value>::type foo(T) {
    std::cout << "Floating-point type\n";
}

int main() {
    foo(42);   // Calls integer version
    foo(3.14); // Calls floating-point version
}
```

Note: `std::enable_if` removes the function from overload resolution when the condition is false.

#### [[C++17]] `if constexpr`

C++17 introduced **`if constexpr`**, which **removes the need for SFINAE in many cases**.

##### Example: `if constexpr` for Type Checking

```c
#include <iostream>
#include <type_traits>

template <typename T>
void foo(T x) {
    if constexpr (std::is_integral<T>::value) {
        std::cout << "Integral type\n";
    } else if constexpr (std::is_floating_point<T>::value) {
        std::cout << "Floating-point type\n";
    } else {
        std::cout << "Unknown type\n";
    }
}

int main() {
    foo(42);    // Integral type
    foo(3.14);  // Floating-point type
    foo("hi");  // Unknown type (no compilation error)
}
```

- No SFINAE required
- Compiler eliminates unused branches at compile-time.

### [[C++ Variadic Templates]]

Define functions or class templates that can take an arbitrary number of arguments (zero or more) of any type.

```cpp
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

### [[Curiously Recurring Template Pattern (CRTP)]]


See also:
- [[Metaprogramming]]
- 