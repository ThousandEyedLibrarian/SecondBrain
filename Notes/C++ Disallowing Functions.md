In [[C++]], sometimes you want to prevent certain operations from being performed on objects of a class. This could be because the default behaviour doesn't make sense for your class, or you want to enforce certain constraints. 

Here’s how you can disallow [[Functions]] like copying, moving, or both.

TLDR: *Just assign the function to the `delete` keyword*. 

### Disallowing Copy Operations

#### Copy Constructor

```cpp
class MyClass {
public:
    // Disallow copy constructor
    MyClass(const MyClass&) = delete;
};
```

In this example, `MyClass` cannot be copied. If someone tries to make a copy of an object of type `MyClass`, it will result in a [[Compilation]] error.

#### Copy Assignment Operator

```cpp
class MyClass {
public:
    // Disallow copy assignment operator
    MyClass& operator=(const MyClass&) = delete;
};
```

Similarly, by deleting the copy assignment operator, attempts to assign one `MyClass` object to another will be flagged by the [[Compiler]].

### Disallowing Move Operations

#### Move Constructor

```cpp
class MyClass {
public:
    // Disallow move constructor
    MyClass(MyClass&&) = delete;
};
```

Disabling the move constructor prevents objects of `MyClass` from being moved from one location to another.

#### Move Assignment Operator

```cpp
class MyClass {
public:
    // Disallow move assignment operator
    MyClass& operator=(MyClass&&) = delete;
};
```

Deleting the move assignment operator ensures that objects of `MyClass` cannot be moved using the assignment syntax.

### Why Disallow?

Disallowing functions like copy and move operations can be crucial for classes that manage resources such as [[Dynamic Memory Allocation]], file handles, or database connections. By disallowing these operations, you prevent unintended side effects and enforce safer usage patterns.

## Practical Example

```cpp
class UniqueResource {
private:
    std::unique_ptr<ResourceType> ptr;

public:
    // Disallow copying and moving
    UniqueResource(const UniqueResource&) = delete;
    UniqueResource& operator=(const UniqueResource&) = delete;
    UniqueResource(UniqueResource&&) = delete;
    UniqueResource& operator=(UniqueResource&&) = delete;

    // Constructor to acquire the resource
    UniqueResource() : ptr(std::make_unique<ResourceType>()) {}

    // Other member functions to work with the resource
};
```

In this `UniqueResource` class, the resource managed by `std::unique_ptr` should not be copied or moved because it represents a unique ownership model.


See also:
- [Advanced C++: Disallow Functions](https://www.youtube.com/watch?v=EL30-a2gblQ&list=PLE28375D4AC946CC3&index=5)