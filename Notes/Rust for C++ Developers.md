G'day! If you're coming from [[C++]], you'll find [[Rust]] both familiar and a bit strange. Hopefully this helps a tad.

## Memory Management: Say G'day to the Borrow Checker

### Ownership vs Raw [[Pointers]]
In C++, you might write:
```cpp
std::string* str = new std::string("G'day!");
// Remember to delete str later...
```

In Rust, ownership is built into the type system:
```rust
let s = String::from("G'day!"); // Automatically cleaned up
```

### References vs References
[[C++ L-value References]] and [[C++ R-value References]] are pretty loose compared to Rust's strict borrowing rules:

```cpp
// C++: Multiple mutable references? No worries!
string& ref1 = str;
string& ref2 = str; // Sure, why not?
```

```rust
// Rust: Choose one!
let mut s = String::from("G'day!");
let r1 = &mut s;
// let r2 = &mut s; // Nope! Can't have two mutable references
```

### [[Smart Pointers]]: Old Mates, New Rules
If you're used to `std::unique_ptr` and `std::shared_ptr`, Rust has similar concepts:

```rust
use std::rc::Rc;      // Like std::shared_ptr
use std::cell::RefCell; // For interior mutability
use std::box::Box;    // Like std::unique_ptr

// When you need shared ownership
let shared = Rc::new(String::from("Share me!"));
let clone = Rc::clone(&shared); // Reference count increases

// When you need heap allocation
let boxed = Box::new(String::from("Heap time!"));
```

## [[C++ Templates]] vs Generics

### Basic Generic [[Functions]]
C++:
```cpp
template<typename T>
T max(T a, T b) {
    return a > b ? a : b;
}
```

Rust:
```rust
fn max<T: std::cmp::PartialOrd>(a: T, b: T) -> T {
    if a > b { a } else { b }
}
```

### Trait Bounds vs Concepts
C++20 concepts are similar to Rust traits:

```cpp
// C++20
template<typename T>
concept Printable = requires(T x) {
    { std::cout << x } -> std::same_as<std::ostream&>;
};
```

```rust
// Rust
trait Printable {
    fn print(&self);
}

fn print_it<T: Printable>(x: T) {
    x.print();
}
```

## Error Handling: No More Exceptions!

### Result Type
Instead of try/catch, Rust uses Result:

```rust
fn might_fail() -> Result<String, MyError> {
    if everything_ok {
        Ok(String::from("All good!"))
    } else {
        Err(MyError::new("Whoops!"))
    }
}

// Using the ? operator (like try but better)
fn do_stuff() -> Result<(), MyError> {
    let s = might_fail()?; // Returns error if might_fail returns Err
    Ok(())
}
```

### Option Type
Instead of null pointers, Rust has Option:

```rust
fn find_thing(things: &[Thing]) -> Option<&Thing> {
    if let Some(thing) = things.first() {
        Some(thing)
    } else {
        None
    }
}

// Pattern matching is your friend
match find_thing(&things) {
    Some(thing) => println!("Found it: {:?}", thing),
    None => println!("Nothing here mate!"),
}
```

## [[C++ Classes]] vs Structs and Impls

### Basic Structure
C++:
```cpp
class MyClass {
public:
    MyClass(int x) : x_(x) {}
    void do_thing();
private:
    int x_;
};
```

Rust:
```rust
struct MyStruct {
    x: i32,
}

impl MyStruct {
    // Constructor (called an "associated function" in Rust)
    fn new(x: i32) -> Self {
        MyStruct { x }
    }
    
    // Method
    fn do_thing(&self) {
        println!("x is {}", self.x);
    }
}
```

### [[Inheritance]] vs [[Composition]]
Rust doesn't have inheritance. Instead, use traits and composition:

```rust
trait Animal {
    fn make_sound(&self);
}

struct Dog {
    name: String,
}

impl Animal for Dog {
    fn make_sound(&self) {
        println!("{} says woof!", self.name);
    }
}
```

## Modern Features You'll Love

### Pattern Matching
```rust
match value {
    0 => println!("Zero!"),
    1..=9 => println!("Single digit!"),
    n @ 10..=99 => println!("Two digits: {}", n),
    _ => println!("Lots of digits!"),
}
```

### Closures
```rust
// Like C++ lambdas, but more ergonomic
let add = |a, b| a + b;
let result = add(5, 3);

// With type annotations
let multiply: fn(i32, i32) -> i32 = |a, b| a * b;
```

### Async/Await
```rust
async fn fetch_data() -> Result<String, Error> {
    let response = client.get("https://api.example.com").await?;
    Ok(response.text().await?)
}
```

## [[Memory]] Safety Features

### Lifetimes
When Rust can't figure out lifetimes automatically:

```rust
struct Container<'a> {
    data: &'a str, // Reference with explicit lifetime
}

impl<'a> Container<'a> {
    fn get_data(&self) -> &'a str {
        self.data
    }
}
```

### Thread Safety
Rust's type system enforces [[Threads]] safety:

```rust
use std::sync::{Arc, Mutex};

// Thread-safe shared ownership
let data = Arc::new(Mutex::new(vec![1, 2, 3]));

let data_clone = Arc::clone(&data);
std::thread::spawn(move || {
    let mut data = data_clone.lock().unwrap();
    data.push(4);
});
```

## Performance Considerations

### Zero-Cost Abstractions
Just like C++, Rust aims for zero-cost abstractions:

```rust
// This iterator chain compiles to efficient machine code
let sum: i32 = (0..1000)
    .filter(|x| x % 2 == 0)
    .map(|x| x * x)
    .sum();
```

### [[Resource Acquisition Is Initialization (RAII)]] and Drop
Like C++ [[Destructor]]s, but with guaranteed ordering:

```rust
struct ResourceHandler {
    data: String,
}

impl Drop for ResourceHandler {
    fn drop(&mut self) {
        println!("Cleaning up!");
    }
}
```

## Common Gotchas for C++ Developers

1. **Mutability**
   - Everything is immutable by default
   - Use `mut` keyword explicitly
   ```rust
   let mut x = 5;
   x = 6; // Only works because x is mut
   ```

2. **[[C++ Move Semantics]] vs Rust Semantics**
   ```rust
   let s1 = String::from("hello");
   let s2 = s1; // s1 is moved, can't use it anymore
   // println!("{}", s1); // This won't compile!
   ```

3. **No Implicit Type Conversion**
   ```rust
   let x: i32 = 5;
   let y: i64 = x as i64; // Must be explicit
   ```

4. **String vs str**
   ```rust
   let s: String = String::from("Owned string");
   let str_slice: &str = "String literal";
   let slice: &str = &s; // Borrow as slice
   ```

## Best Practices

1. **Use Option Instead of Null**
   ```rust
   // Instead of nullable pointers:
   fn find_item(items: &[Item]) -> Option<&Item> {
       items.iter().find(|item| item.id == 5)
   }
   ```

2. **Prefer [[Stack]] Over [[Heap]]**
   ```rust
   // Usually better
   let array = [1, 2, 3, 4, 5];
   
   // Only when needed
   let vec = Box::new(vec![1, 2, 3, 4, 5]);
   ```

3. **Use Type Inference**
   ```rust
   // Let the compiler figure it out
   let mut map = HashMap::new();
   map.insert("key", "value");
   ```

## Advanced Concepts

### Interior Mutability
Like `mutable` in C++, but with more control:

```rust
use std::cell::Cell;
use std::cell::RefCell;

struct Widget {
    // Like C++'s mutable keyword
    count: Cell<u32>,
    // For when you need runtime borrow checking
    data: RefCell<Vec<String>>,
}

impl Widget {
    fn increment(&self) { // Note: self is NOT mut
        self.count.set(self.count.get() + 1);
        
        // Runtime borrow checking
        self.data.borrow_mut().push(String::from("new"));
    }
}
```

### Type State Programming
Encode states in the type system:

```rust
// Compile-time state machines
struct Uninitialized;
struct Initialized;
struct Running;

struct Server<State> {
    data: Vec<u32>,
    _state: std::marker::PhantomData<State>,
}

impl Server<Uninitialized> {
    fn new() -> Self {
        Server {
            data: Vec::new(),
            _state: std::marker::PhantomData,
        }
    }
    
    fn initialize(self) -> Server<Initialized> {
        Server {
            data: self.data,
            _state: std::marker::PhantomData,
        }
    }
}

impl Server<Initialized> {
    fn start(self) -> Server<Running> {
        Server {
            data: self.data,
            _state: std::marker::PhantomData,
        }
    }
}
```

### Advanced Trait Usage

#### Associated Types vs Generic Parameters
```rust
// Generic parameter approach
trait Container<T> {
    fn get(&self) -> &T;
}

// Associated type approach
trait Container {
    type Item;
    fn get(&self) -> &Self::Item;
}

// Implementation with associated type
impl Container for Vec<String> {
    type Item = String;
    fn get(&self) -> &Self::Item {
        &self[0]
    }
}
```

#### Trait Objects and Dynamic Dispatch
```rust
// C++ equivalent of virtual functions
trait Drawable {
    fn draw(&self);
}

struct Canvas {
    // Vec of trait objects - like C++'s vector of base class pointers
    shapes: Vec<Box<dyn Drawable>>,
}

impl Canvas {
    fn add_shape<T: Drawable + 'static>(&mut self, shape: T) {
        self.shapes.push(Box::new(shape));
    }
    
    fn draw_all(&self) {
        for shape in &self.shapes {
            shape.draw();
        }
    }
}
```

### Advanced [[Concurrency]]

#### Channels
```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (tx, rx) = mpsc::channel();
    
    // Multiple producers
    let tx1 = tx.clone();
    thread::spawn(move || {
        tx1.send("hello from thread 1").unwrap();
    });
    
    thread::spawn(move || {
        tx.send("hello from thread 2").unwrap();
    });
    
    // Single consumer
    for received in rx {
        println!("Got: {}", received);
    }
}
```

#### Async/Await with Tokio
```rust
use tokio;

#[tokio::main]
async fn main() {
    let mut handles = vec![];
    
    for i in 0..10 {
        // Spawn async tasks
        let handle = tokio::spawn(async move {
            process_data(i).await
        });
        handles.push(handle);
    }
    
    // Wait for all tasks
    for handle in handles {
        handle.await.unwrap();
    }
}

async fn process_data(i: u32) -> Result<(), Box<dyn std::error::Error>> {
    tokio::time::sleep(tokio::time::Duration::from_secs(1)).await;
    println!("Processed {}", i);
    Ok(())
}
```

### Advanced [[Memory]] Management

#### Custom Allocators
```rust
use std::alloc::{GlobalAlloc, Layout, System};

struct CountingAllocator;

unsafe impl GlobalAlloc for CountingAllocator {
    unsafe fn alloc(&self, layout: Layout) -> *mut u8 {
        println!("Allocating {} bytes", layout.size());
        System.alloc(layout)
    }
    
    unsafe fn dealloc(&self, ptr: *mut u8, layout: Layout) {
        println!("Deallocating {} bytes", layout.size());
        System.dealloc(ptr, layout)
    }
}

#[global_allocator]
static ALLOCATOR: CountingAllocator = CountingAllocator;
```

#### Arena Allocation
```rust
use typed_arena::Arena;

struct Node<'a> {
    next: Option<&'a Node<'a>>,
    data: i32,
}

fn build_linked_list() {
    let arena = Arena::new();
    
    let node1 = arena.alloc(Node {
        next: None,
        data: 1,
    });
    
    let node2 = arena.alloc(Node {
        next: Some(node1),
        data: 2,
    });
    
    // No manual cleanup needed!
}
```

### Advanced Error Handling 

#### Custom Error Types
```rust
#[derive(Debug)]
enum MyError {
    IoError(std::io::Error),
    ParseError(std::num::ParseIntError),
    Custom(String),
}

impl std::error::Error for MyError {}

impl From<std::io::Error> for MyError {
    fn from(err: std::io::Error) -> MyError {
        MyError::IoError(err)
    }
}

impl From<std::num::ParseIntError> for MyError {
    fn from(err: std::num::ParseIntError) -> MyError {
        MyError::ParseError(err)
    }
}

// Usage
fn do_stuff() -> Result<(), MyError> {
    let file = std::fs::File::open("data.txt")?; // IoError automatically converted
    let num: i32 = "not a number".parse()?;      // ParseError automatically converted
    Ok(())
}
```

### Macros and [[Metaprogramming]]

#### Declarative Macros
```rust
// Similar to C++ preprocessor but much more powerful
macro_rules! vec_of_strings {
    ($($x:expr),*) => {
        vec![$($x.to_string()),*]
    }
}

let v = vec_of_strings!["hello", "world"];
```

#### Procedural Macros
```rust
use proc_macro::TokenStream;

#[proc_macro_derive(MyTrait)]
pub fn my_trait_derive(input: TokenStream) -> TokenStream {
    // Transform input code
    "fn hello() { println!(\"Hello, world!\"); }".parse().unwrap()
}
```

### FFI and C++ Interop

#### Calling C++ from Rust
```rust
#[link(name = "my_cpp_lib")]
extern "C" {
    fn cpp_function(x: i32) -> i32;
}

fn main() {
    unsafe {
        let result = cpp_function(42);
        println!("Result from C++: {}", result);
    }
}
```

#### Exposing Rust to C++
```rust
#[no_mangle]
pub extern "C" fn rust_function(x: i32) -> i32 {
    x * 2
}
```

### Advanced Testing Features

#### Property-Based Testing
```rust
use proptest::prelude::*;

proptest! {
    #[test]
    fn doesnt_crash(s in "\\PC*") {
        let _ = my_function(&s);
    }
    
    #[test]
    fn addition_works(x in 0..100i32, y in 0..100i32) {
        let sum = x + y;
        assert!(sum >= x);
        assert!(sum >= y);
    }
}
```

#### Benchmark Tests
```rust
#![feature(test)]
extern crate test;

#[cfg(test)]
mod tests {
    use test::Bencher;
    
    #[bench]
    fn bench_add(b: &mut Bencher) {
        b.iter(|| {
            // Code to benchmark
            1 + 2
        });
    }
}
```

### Real-World [[Design Patterns]]

#### Builder Pattern
```rust
#[derive(Default)]
struct ServerBuilder {
    port: Option<u16>,
    host: Option<String>,
    workers: Option<u32>,
}

impl ServerBuilder {
    fn new() -> Self {
        ServerBuilder::default()
    }
    
    fn port(mut self, port: u16) -> Self {
        self.port = Some(port);
        self
    }
    
    fn host(mut self, host: String) -> Self {
        self.host = Some(host);
        self
    }
    
    fn workers(mut self, workers: u32) -> Self {
        self.workers = Some(workers);
        self
    }
    
    fn build(self) -> Result<Server, &'static str> {
        let port = self.port.ok_or("Port not set")?;
        let host = self.host.ok_or("Host not set")?;
        let workers = self.workers.unwrap_or(4);
        
        Ok(Server::new(host, port, workers))
    }
}
```

