When multiple threads access shared resources, there is a possibility of a data race. To avoid this, use mutex and locks to synchronise shared resource access.

Mutex stands for Mutual Exclusion. 

In C++, std::mutex class is a synchronisation [[Primitive]] that is used to protect the shared data from being accessed by multiple [[Threads]] simultaneously. The shared data can be in the form of variables, data structures, etc.

**std::mutex** class implements mutex in [[C++]]. It is defined inside the *mutex* header file.

## Usage

The use of mutex can be divided into three steps:

### 1. Create a std::mutex Object

`std::mutex mutex_object_name;`

### 2. Lock the Thread

The **lock()** function of the std::mutex class locks the thread and allows only the current thread to run until it is unlocked. It prevents the shared resource from being accessed by multiple threads simultaneously.

`mutex_object_name.lock()`

### 3. Unlock the thread

The **unlock()** of the std::mutex function is used to release the lock after execution of the code piece containing the possibility of race condition occurrence. It resumes all the waiting threads.

`mutex_object_name.unlock()`

## Code-based Example

Example courtesy of GeeksForGeeks:
```cpp
// C++ program to illustrate the thread synchronization using mutex
#include <iostream>
#include <thread>

using namespace std;

// import mutex from C++ standard library
#include <mutex>

// Create object for mutex
mutex mtx;

// Shared resource
int number = 0;

// function to increment the number
void increment(){
    
    // Lock the thread using lock
    mtx.lock();
    
    // increment number by 1 for 1000000 times
    for(int i=0; i<1000000; i++){
        number++;
    }
    
    // Release the lock using unlock()
    mtx.unlock();
}

int main()
{
    // Create thread t1 to perform increment()
    thread t1(increment);
    
    // Create thread t2 to perform increment()
    thread t2(increment);
    
    // Start both threads simultaneously
    t1.join();
    t2.join();
    
    // Print the number after the execution of both threads
    std::cout<<"Number after execution of t1 and t2 is "<<number;
    
    return 0;
}
```

These have effectively been improved on in [[C++20]] with the invention of [[C++20 Semaphore]]s.


See also:
- [[Concurrency]]
- [[C++20 Semaphore]]