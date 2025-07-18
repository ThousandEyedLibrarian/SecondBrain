A type of [[C++ Abstract Data Type (ADT)]], and a core aspect of [[Object-Oriented Programming]], similar to [[C++ Classes]] except with public data structures by default upon initialisation.

Example:
```cpp
struct Employee {
    int id;
    std::string name;
    float salary;
};

Employee e1; // create an object of the 'Employee' structure
```

You can access the members of a structure using the dot operator `.`:

```cpp
e1.id = 1;
e1.name = "John Doe";
e1.salary = 40000;
```

## Why Use a Struct Instead of [[C++ Classes]]?

Generally speaking, structs are used for basic stuff, they should be data containers that carry public data and have very few basic member [[Functions]].

Classes are generally used for more complex tasking and carry private data which can be interfaced with through their public member functions.


See also:
- [[Data Structures]]
- [[C++]]