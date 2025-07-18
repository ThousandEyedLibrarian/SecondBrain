A type of [[C++ Abstract Data Type (ADT)]], and a core aspect of [[Object-Oriented Programming]], similar to [[C++ Structures]] except with private data structures by default upon initialisation, generally used for more complex tasking.

Example:
```cpp
class Student {
    int roll_no;
    std::string name;
    float marks;

public:
    void set_data(int r, std::string n, float m) {
        roll_no = r;
        name = n;
        marks = m;
    }

    void display() {
        std::cout << "Roll no: " << roll_no
                  << "\nName: " << name
                  << "\nMarks: " << marks << std::endl;
    }
};

Student s1; // create an object of the 'Student' class
```


See also:
- [[C++]]