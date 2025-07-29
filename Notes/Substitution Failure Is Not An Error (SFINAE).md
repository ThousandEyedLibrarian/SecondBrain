Enables restricting of [[C++ Templates]] [[Functions]] By Type

A.K.A [[Substitution Failure Is Not An Error (SFINAE)]].

1. Create a template function
2. Create a struct to represent your acceptable types
3. Create the template specialisation functions for those types only

Member substitution allows the program to substitute for only those types and throw otherwise.

```cpp
template<typename T>
struct FloatOrDouble {/* No member - allows for substitution of type */};

template<>
struct FloatOrDouble<float> {
	using type = void;
}

template<>
struct FloatOrDouble<double> {
	using type = void;
}

// Use it in a function declaration
template<class T, class U = typename FloatOrDouble<t>::type>
T doSomething(T x)
```