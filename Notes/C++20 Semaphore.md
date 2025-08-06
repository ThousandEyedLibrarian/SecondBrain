Semaphores are synchronisation [[Primitive]]s that help control access to shared resources in [[Multiprogramming (Multithreading)]] programs ([[C++ Multithreading]]).

Builds upon the concept of [[Mutex]]es.

The *semaphore* header provides the standard [[C++]] way to work with semaphores.

```cpp
#include <semaphore>
std::counting_semaphore<size_t> sem(1); // Initialise a semaphore with an initial count of 1
```

There are 3 methods to acquire and release a semaphore object:

**Method 1: Aquire and Release**

To acquire (lock) the semaphore, you can use the acquire method:

```cpp
sem.acquire();
// Critical section code
sem.release();
```

The **acquire** method decreases the semaphore count by one, effectively locking it. The **release** method increases the count, releasing the semaphore.

**Method 2: Try-Aquire**

You can also use the try_acquire method to try to acquire the semaphore without blocking:

```cpp
if (sem.try_acquire()) {
    // Successfully acquired the semaphore
    // Critical section code
    sem.release();
} else {
    // Semaphore was not acquired
}
```

**Method 3: Waiting with Timeout**

C++20 also introduced the `try_acquire_for` and `try_acquire_until` methods to try acquiring the semaphore with a timeout.

```cpp
if (sem.try_acquire_for(std::chrono::seconds(1))) {
    // Successfully acquired the semaphore within 1 second
    // Critical section code
    sem.release();
} else {
   // Semaphore was not acquired within 1 second
}
```

## Semaphore Types

1. `std::counting_semaphore<10> semaphore(3)`
	1. Initialises a semaphore with max 3 simultaneous threads accessing a shared resource
	2. [[Threads]] can acquire and release counts, and the semaphore's count is incremented or decremented accordingly
	3. If a thread tries to acquire more counts than are available, it will block until counts become available
2. `std::binary_semaphore semaphore(1)`
	1. Initialises a semaphore with max 1 simultaneous thread accessing the resource
	2. Basically a lighterweight interface for a [[Mutex]]

## Why Use Semaphores Over Mutex?

1. **Fine-Grained Control:** To access a resource concurrently, semaphores can be configured to allow a specific number of threads.
2. **Generalisation:** Semaphores are more versatile and can be used to implement other synchronisation primitives.
3. **Multiple Resources:** Counting semaphores can be used to manage multiple instances of a resource. This makes them suitable for scenarios where you need to control access to a pool of resources (e.g., a thread pool or a connection pool).
4. **Blocking and Waiting:** Blocking and waiting mechanisms in semaphores allow threads to wait until a resource becomes available again.
5. **Timeouts:** A timeout could be specified when acquiring a semaphore, which makes it more useful.