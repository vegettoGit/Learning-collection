## [Observability Tools C++: Beyond GDB and printf - Tools to Understand the Behavior of Your Program - Ivica Bogosavljevic - CppCon 2022](https://www.youtube.com/watch?v=C9vmS5xV23A&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* On an unfamiliar codebase, we want to analyze: Hot and cold functions, timeline, memory usage, hardware efficiency, how the program interacts with the operating system. Debuggers and printf aren't enough.
* Observability tools are also useful for debugging weird / unusual behaviors.
* Flamegraphs / Speedscope.
  * It shows stacktraces and time.
  * Data is collected with perf, then we feed speedscope (the visualizer) with it.
* Heap profilers / Heaptrack.
  * Debugging memory consumption issues.
  * Peak Contributions, Largest Memory Leaks, Most Memory Allocations, Most Temporary Allocations.
* Coverage tools / Icov.
  * For each line in your source code, it shows you how many times that line was executed. You might find out lines that were never executed.
  * When running with Icov for debugging, your program will run slower as the compiler has added new lines of code behind the scenes.
* Kernel call tracing / Strace.
  * Observe how your program talks with the OS.
  * Important if the program is spending a lot of time in system mode (when the operating system is doing work for your program).
* Hardware counters and event counters / Perf.
  * Time elapsed (how much in total, in user mode and in system mode), task-clock, context-switches, cpu-migrations, page-faults, cycles, instructions per cycle, branches and  branch-misses.
* Data flow analysis - Pernosco.
* Other debugging tools.
  * Valgrind, Sanitizers, Helgrind, Reverse debugging, etc.

## [Introduction to Hardware Efficiency in Cpp - Ivica Bogosavljevic - CppCon 2022](https://www.youtube.com/watch?v=Fs_T070H9C8&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Hardware efficiency is important for peak performance. We want the best usage of hardware resources.
* 2 major bottlenecks: 
  * Computationally intensive or CPU bound (limited by CPU resources).
  * Memory intensive or memory bound (limited by the memory subsystem).
  * Others: Disk bound, network bound.
* Dedicated profiling tools to read the hardware performance counters: Intel's VTUNE, AMD uProf, pmu-tools, perf or LIKWID.
* Optimizing computationally intensive code.
  * Code which is processing simple data types, where the data is stored in an array / vector and with sequential access to values.
  * Domains: Image / audio / video processing, machine learning, telecommunications, scientific computing.
* Introduction to vectorization.
  * SIMD: Single Instruction, Multiple Data. Modern CPUs can process multiple data in a single instruction.
  * Automatic compiler vectorization is not always possible. Compilers auto-vectorize loops when certain conditions are met.
  * Prerequisites for autovectorization: Simple data types, sequential memory access pattern, independent iterations, number of iterations known, not many conditionals within the loop, no pointer aliasing.
  * A few tips: Loop fission (split loop into vectorizable and non-vectorizable parts), loop unswitching (move invariants outside of the loop) and loop sectioning (iterate in smaller sections).
* Optimizing memory intensive code.
  * Instead of using a vector that contains instances of a class, each member of the class has its own vector.
  * From Array of Structs to Struct of Arrays.
  * Processing a matrix column wise is memory bound. Make sure we are accessing the data sequentially.
  * CPUs are much faster than memory. CPUs are data starved.
  * Solution: Data cache memory. Accessing a piece of data which is already in the cache is fast.
* When do cache misses typically happen?
  * Dereferencing a pointer for the first time (pointer data members, heap allocated objects, vector of pointers, chasing pointers).
  * Accessing a member of an array in a random fashion.
  * Lookup in a hash map or a binary tree (std::set, std::unondered_set, std::map, std::unordered_map).
* When do cache hits typically happen?
  * Iterating sequentially through an array / vector.
  * Keeping the data set small.
  * Data accessed together should be close neighbors in memory.
  * What is accessed one after another (linked list, binary tree) should be laid out in contiguous memory.  
* The CPU has a component called data prefetcher. If the memory access pattern is predictable, it prefetches the data before is needed. That's why data access is so much faster for contiguous structures such as arrays and vectors.
  * Vector of values vs vector of pointers.
* Why is it faster to process small classes?
  * The data is brought to the CPU in blocks (typically 64 bytes).
  * Large classes bring in unused data to the CPU. This is wasted memory bandwidth.
  * Data members that are often accessed together should be declared together in the class definition, increasing their chances to be in the same cache block.  
* Always measure!

## [The Hidden Performance Price of C++ Virtual Functions - Ivica Bogosavljevic - CppCon 2022](https://www.youtube.com/watch?v=kRdbqjw2WIs&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Virtual functions in C++:
  * Enable flexibility.
  * Basic component of OOP.
* Virtual functions are slower than regular functions.
* The performance price of virtual functions depends on several factors.
* How do virtual functions work?
  * Virtual tables. Each object has a vptr (hidden) pointing to their `VTABLE`. There is a VTABLE for each type. The entries of the VTABLE are pointers to functions. The vptr pointer is set when the constructor runs.
  * Virtual function calls: The compiler accesses the hidden vptr and knows which entry in the VTABLE is the address of the function we want to call. At runtime, we need to dereference the vptr to be able to get the address of the function from the VTABLE entry, then dereference the address of the function. There is a runtime cost on dereferencing.
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
  * The main reason you want to use a vector of pointers is polymorphism. But there are other alternatives such as using `std::variant` with `std::visitor`.
* Compiler Optimizations:
  * The compiler knows the address of non-virtual functions at compile time, which means the compiler can inline a non-virtual function and avoid the function call. Inlining saves a few instructions on the function call.
  * After inlining, the compiler can perform many other optimizations such as: Move loop invariant code outside of the calling loop, use vectorization (instructions that can process multiple data at once).
* Jump Destination Guessing:
  * To speed up computation, modern CPUs do a bunch of guessing (speculative execution).
  * In the case of virtual functions, the CPU guesses which virtual function will be called and it starts executing the instructions belonging to it. If the guess is correct, this saves time, but otherwise the CPU needs to cancel and start over, which is costly.
  * In a vector of pointers, the CPU can predict better when it's sorted by type.
* Instruction Cache Evictions:
  * Modern CPUs rely on getting to know the instructions they are executing. Code that has already been executed is hot code, where its instructions are in the instruction cache, its branch predictors know the outcome of the branch and its jump predictors know the target of the jump.
  * The CPU is faster when executing hot code. The CPU memory is limited. Code that is currently hot will eventually become cold unless executed frequently.
  * Virtual functions (especially large ones where each object has a different implementation) imply that we are switching from one implementation to another. This is cold code.
  * Once again, the best case is when the objects in the container are sorted by type.

## [Refresher on Containers, Algorithms and Performance - Vladimir Vishnevskii - C++ on Sea 2022](https://www.youtube.com/watch?v=zxKGKwwbkU0&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [Where Have All the Cycles Gone? by Sean Parent](https://www.youtube.com/watch?v=B-aDBB34o6Y&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [High Performance Code 201: Hybrid Data Structures - Chandler Carruth - CppCon 2016](https://www.youtube.com/watch?v=vElZc6zSIXM&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA) 

## [Efficiency with Algorithms, Performance with Data Structures - Chandler Carruth - CppCon 2014](https://www.youtube.com/watch?v=fHNmRkzxHWs&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


