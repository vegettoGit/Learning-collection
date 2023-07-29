## [The Hidden Performance Price of C++ Virtual Functions - Ivica Bogosavljevic - CppCon 2022](https://www.youtube.com/watch?v=kRdbqjw2WIs&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Virtual functions in C++.
  * Enable flexibility.
  * Basic component of OOP.
* Virtual functions are slower than regular functions.
* The performance price of virtual functions depends on several factors.
* How do virtual functions work?
  * Virtual tables. Each object has a vptr (hidden) pointing to their `VTABLE`. There is a VTABLE for each type. The entries of the VTABLE are pointers to functions. The vptr pointer is set when the constructor runs.
  * Virtual function calls: The compiler accesses the hidden vptr and knows which entry in the VTABLE is the address of function we want to call. At runtime, we need to dereference the vptr to be able to get the address of the function from the VTABLE entry, then dereference the address of the function. There is a runtime cost dereferencing.
* Virtual functions are therefore more expensive than non-virtual functions. 
* Initial analysis with an experiment. 
  * Vector of 20 million objects of the same type. 
  * 20 million calls to a virtual function are a bit more expensive than 20 million calls to a non-virtual function, but the results don't look that bad (a difference of milliseconds), it's a slight overhead.
* Vector of pointers:
  * To activate the virtual function mechanism, we need to access objects through a pointer or a reference. Objects need to be allocated on the heap (using new, malloc or smart pointers). Accessing objects on the heap can be very slow.
  * Optimal layout (higher cache hit rate when all objects of the same type are next to each other) vs non-optimal layout.
  * Accessing objects on the heap can be very slow because of data cache misses. If objects are neighbors in memory, we can expect performance improvements, otherwise we can expect slowdowns. If the neighboring pointers do not point to neighboring elements on the heap, we can expect cache misses.
  * There is no guarantee that neighboring pointers will point to neighboring objects in memory.
  * Vector of objects is much better for performance than vector of pointers. A vector of objects doesn't suffer from data cache misses.
  * The memory layout is therefore very important for performance.
  * The slowdown isn't about virtual functions per se, it's more related to the memory layout. 
  * The main reason you want to use a vector of pointers is polymorphism. But there are other alternative such as using `std::variant` with `std::visitor`.
* Compiler Optimizations:
  * The compiler knows the address of non-virtual functions at compile time, which means the compiler can inline the non-virtual function and avoid the function call. Inlining saves a few instructions on the function call.
  * After inlining, the compiler can perform many other optimizations such as: Move loop invariant code outside of the calling loop, use vectorization (instructions that can process multiple data at once).
* Jump Destination Guessing:
  * To speed up computation, modern CPUs do a bunch of guessing (speculative execution).
  * In the case of virtual functions, the CPU guesses which virtual function will be called and it starts executing the instructions belonging to it. If the guess is correct, this saves time, but otherwise the CPU needs to cancel and starts over, which is costly.
  * In a vector, the CPU can predict better when types are sorted.
* Instruction Cache Evictions:
  * Modern CPUs rely on getting to know the instructions they are executing. Code that has already been executed is hot code, where its instructions are in the instruction cache, its branch predictors know the outcome of the branch and its jump predictors know then target of the jump.
  * The CPU is faster when executing hot code. The CPU memory is limited. Code that is currently hot will eventually become cold unless executed frequently.
  * Virtual functions (especially large ones where each object has a different implementation) imply that we are switching from one implementation to another. This is cold code.
  * Once again, the best case is when the objects in the container are sorted by type.

## [Refresher on Containers, Algorithms and Performance - Vladimir Vishnevskii - C++ on Sea 2022](https://www.youtube.com/watch?v=zxKGKwwbkU0&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [Where Have All the Cycles Gone? by Sean Parent](https://www.youtube.com/watch?v=B-aDBB34o6Y&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [“High Performance Code 201: Hybrid Data Structures" - Chandler Carruth - CppCon 2016](https://www.youtube.com/watch?v=vElZc6zSIXM&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA) 

## ["Efficiency with Algorithms, Performance with Data Structures" - Chandler Carruth - CppCon 2014](https://www.youtube.com/watch?v=fHNmRkzxHWs&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


