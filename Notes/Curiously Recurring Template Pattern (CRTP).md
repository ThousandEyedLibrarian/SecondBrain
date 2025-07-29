This entire excerpt was taken from a very good GitHub gist by miceks, linked [here](https://gist.github.com/miceks/b75715044ecfeb5fd4ca2d7c7f975e36).

---

This post describes a form of [[C++]] runtime polymorphism using [[Inheritance]] over a closed set of types to achieve high performance [[Run-Time Type Identification (RTTI)]]-like functionality without [[C++ Virtual Function]]s. The core concept can be made to work in [[C++11,]] but some [[C++14]] creature comforts are used in the [demo code](https://godbolt.org/z/xexWz71nW).

# Background


>"*I was recently working on a personal C++ container library requiring linked list-like functionality for different node types, and some form of runtime polymorphism was required. Bog-standard virtual functions seemed the obvious solution, but the longer I tried the more awkward this approach appeared in this particular case. What I really wanted was something like `next<Y>(Node* x) -> Y*`, which, given a general node `x` in the list, returns the next node of type `Y`, but the closest I could get was encapsulating each thing you might want to do to each type of node in a virtual function which forwards the call to the correct node. This resulted in a bloated and intrusive interface which for most nodes would be trivial (is this call relevant to me? No? Forward to next node), which didn't seem great. Going back to the drawing board, the next alternative that sprung to mind was rtti and `dynamic_cast` which on paper is a good fit, but since the driving motivations were performance (this would be a very hot code path) and portability (rtti isn't always acceptable), this was ruled out also.*
>
>*Lastly, as a modern alternative to virtual function polymorphism we have `std::variant`, providing very attractive performance characteristics in the case that we know the set of possible types it can hold at compile time, which happened to be true in this case. Unfortunately, since the container I was working on was generic, some of the nodes had to accommodate a type of potentially large size. This would make the other nodes just as large, which was unacceptable. Further, there would be much code duplication if some of the nodes could not share a base class. The following weird amalgam of the above characteristics is what I ended up using, and I thought it might be interesting to other fans of C++ template over-engineering :).*"

# Design

The idea is to use CRTP beyond [[Static Polymorphism]] by storing some form of state in the base class to determine which of its derived types (template parameters) it actually is. This could of course be accomplished using [[C++ Virtual Function]]s, but if all we want to do is return some type of flag then why not store that flag directly instead of going through a [[C++ Virtual Tables]] indirection?

```c
template <typename... Ds>
class Base
{
    using Bits = unsigned;

    static_assert(sizeof...(Ds) <= std::numeric_limits<Bits>::digits, "Not enough bits");

    template <typename... Bs>
    static constexpr auto to_bits(Bs... bits) -> Bits
    {
        Bits ret = 0;
        int idx = 0;
        for(bool bit : {bits...})
            ret |= (bit << idx++);

        return ret;
    }

    template <typename T>
    static constexpr Bits bitsof = to_bits(std::is_base_of<T, Ds>::value...);


  public:
    template <typename T>
    friend auto down_cast(Base* ptr) -> T*
    {
        return (ptr->m_type & bitsof<T>) ? static_cast<T*>(ptr) : nullptr;
    }


  protected:
    template <typename T>
    Base(T*) : m_type{bitsof<T>} {}


  private:
    Bits const m_type;
};

// Declaration outside class needed unless we have C++20
template <typename T, typename... Ds> auto down_cast(Base<Ds...>*) -> T;
```

The class `Base` contains a bitflag `m_type` with exactly one bit set corresponding to the active derived type in its template parameter list[1](https://gist.github.com/miceks/b75715044ecfeb5fd4ca2d7c7f975e36#user-content-fn-1-ea9a840f629c4e553e8275fc9dfce1e2), _not_ an index like in `std::variant`. This allows us to neatly represent is-a relationships in the sub-hierarchy of `Base` through a bitmask (the `bitsof` variable template); a shared base have all the bits of its derived types set. Any such shared base class is _not_ included in the template parameter list -- only the most derived or "leaf" classes are.

The correct bit in `m_type` is deduced in the template constructor from the `this` pointer passed by the derived type on construction (se below). This saves us from having to manually set the correct bit in each derived type, which is nice. The final component is the `down_cast` function which acts like `dynamic_cast`. This is where the design really shines, as we only need a single bitwise comparison to determine if a `Base` [[Pointer]] can be bound to any part of its sub-hierarchy.

# Example

To see the method in action, consider the following not-so creative scenario:

Only `Student`, `Teacher` and `Avocado` are ever instantiated, but we have an intermediate base `Human` which allows us to reuse code, do partial downcasts, all that good stuff. Accordingly, we use a base `Base<Student, Teacher, Avocado>` instantiated on the actual instances to model the hierarchy:

```c
// Forward declare the most derived "leaf" classes and define handy alias

struct Student;
struct Teacher;
struct Avocado;

using Organism = Base<Student, Teacher, Avocado>;


// Intermediate base (need to expose Base constructor to sub-classes)

struct Human : public Organism
{
  protected:
    using Organism::Organism;
};


// Most derived definitions (passing 'this' pointer lets Base deduce correct bit)

struct Student : public Human 
{ 
    Student() : Human(this) {}
};

struct Teacher : public Human 
{ 
    Teacher() : Human(this) {}
};

struct Avocado : public Organism 
{ 
    Avocado() : Organism(this) {}
};


int main()
{
    Student s{};
    Organism* mystery = &s;

    // Prints "Human"
    if(Human* ptr = down_cast<Human>(mystery))
        std::cout << "Human\n";     

    // Prints "Student"
    if(Student* ptr = down_cast<Student>(mystery))
        std::cout << "Student\n";   

    // Prints nothing
    if(Teacher* ptr = down_cast<Teacher>(mystery))
        std::cout << "Teacher\n";

    // Prints nothing
    if(Avocado* ptr = down_cast<Avocado>(mystery))
        std::cout << "Avocado\n";
}
```

This is admittedly not the best example since the above would never be considered a reasonable alternative to virtual functions, but hopefully I convinced you in the previous section that there exist at least some scenarios where a more constrained version of rtti could be interesting. Even if this is not the case, the design could easily provide something similar to `std::visit` (delegate to correct function / code based on tag), though that would kind of discard some of its unique strengths.

# Conclusion

Putting this method in comparison with the other two dominant forms of runtime [[Polymorphism]], we have:

|Inheritance & virtual functions|Runtime CRTP|std::variant|
|---|---|---|
|Open set of types|Closed set of types|Closed set of types|
|Reference semantics|Reference semantics|Value semantics|
|Heterogeneous size|Heterogeneous size|Homogeneous size|
|Code reuse, is-a modelling|Code reuse, is-a modelling||
|dynamic_cast (potentially slow)|down_cast (fast)|get_if (fast, but no is-a semantics)|
