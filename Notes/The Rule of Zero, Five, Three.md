AKA the law of three, the big three

A rule of thumb mainly to keep your code handy-dandy and safe from errors.

## The Rule of Three

The Rule of Three states that a class or structure that manages resources should define the following three special member functions:

- Destructor
- Copy constructor
- Copy assignment operator

These functions are necessary for proper resource management, such as releasing memory or correctly handling deep copies.

_Example:_

```cpp
class MyResource {
public:
    // Constructor and destructor
    MyResource() : data(new int[100]) {} 
    ~MyResource() { delete[] data; } 

    // Copy constructor
    MyResource(const MyResource& other) : data(new int[100]) {
        std::copy(other.data, other.data + 100, data);
    }

    // Copy assignment operator
    MyResource& operator=(const MyResource& other) {
        if (&other == this) { return *this; }
        std::copy(other.data, other.data + 100, data);
        return *this;
    }

private:
    int* data;
};
```

### But why?

Basically, the rule claims that if one of these had to be defined by you then the others likely don't fit the needs of the class in one case and therefore won't in others either so should be redefined for your specific cases.

### The Rule of Five

Sometimes broadened to the rule of five, this is simply the rule above but including the move constructor and move assignment operator.

Modern [[C++]] introduces [[C++ Move Semantics]], which allows for more efficient handling of resources by transferring ownership without necessarily copying all the data.

_Example:_

```cpp
class MyResource {
public:
    // Constructors and destructor
    MyResource() : data(new int[100]) {}
    ~MyResource() { delete[] data; }

    // Copy constructor
    MyResource(const MyResource& other) : data(new int[100]) {
        std::copy(other.data, other.data + 100, data);
    }

    // Copy assignment operator
    MyResource& operator=(const MyResource& other) {
        if (&other == this) { return *this; }
        std::copy(other.data, other.data + 100, data);
        return *this;
    }

    // Move constructor
    MyResource(MyResource&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }

    // Move assignment operator
    MyResource& operator=(MyResource&& other) noexcept {
        if (&other == this) { return *this; }
        delete[] data;
        data = other.data;
        other.data = nullptr;
        return *this;
    }

private:
    int* data;
};
```

See also:
- [[C++]]