## [Simulating Low-Level Hardware Devices in Cpp - Ben Saks - CppCon 2022](https://www.youtube.com/watch?v=zqHvN8xpuKY&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Overview:
  * Embedded applications need to work on target hardware, but working on real hardware isn't always ideal (it limits our ability to test and debug, it takes time to upload code to the hardware).
  * We can minimize the impact of these costs by running our application in a simulated environment.
  * We will use operator overloading to make the simulated registers behave similarly to the target hardware registers.
* Our Example Program.
* Classes and Memory-Mapped Hardware.
  * CPUs typically communicate with external devices via device registers.
  * A device register is circuitry that provides an interface to a device.
  * "Typical" Address Space.
  * In C++, you can access a memory-mapped register as if it was an ordinary object via an appropiately-initialized pointer.
  * Many hardware devices have multiple registers, often located at contiguous addresses.
* Setting Up for the Target Hardware.
  * Operator New Overload.
  * Operator Delete Overload.
* Challenges of Real Hardware.
* Simulating Individual Registers.
  * Our simulation should produce the side effects of accessing hardware registers, when accessing device registers.
  * Our device register objects will need to support on-read and on-write effects.
* The `device_register` Class.
  * The conversion operator defines an implicit conversion from a user-defined type to another type. It provides a place to insert the code for the on-read side effect.
  * Overload operator `=`. This is a place to trigger code for the on-write side effect.
  * Supports the bitwise operations `&=` and `|=`. They involve writing and reading, so they trigger both side effects.
* Side Effects by Location.
  * Let's base each register's side effect on its memory location.
  * Each side effect is a pointer to function that takes `std::uint32_t` (representing the value of the register): `void (*) (std::uint32_t);`. We can also use `std::function<std::uint32_t>`.
  * `device_register` will use a static `std::map` that associates each `device_register`'s location with its effect handlers object.
* Dynamic Memory and Simulations.
  * Dynamically-allocated memory might not be available on embedded systems. This makes it hard to use containers such as `std::map`. It's never used on the target hardware, it's just for the simulation.

## [C++ in Constrained Environments - Bjarne Stroustrup - CppCon 2022](https://www.youtube.com/watch?v=2BuJjaGuInI&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Fundamental ideas
  * Constrained environments: Notably embedded systems (where users don't think of the system as computers). It involves a wide variety of constraints: Limited space for code and data, limited processing power, strict limits on latency, zero or very limited downtime, limited run-time support, etc.
  * Our focus is on: Reliability, Dependability, Resources, Messy problems, Maintainability.
  * C++ pillars: Direct map to hardware and zero-overhead abstractions. What you don't use, you don't pay for. It doesn't mean "zero cost".
* Low-level manipulation
  * Adopt language features that reduce the chance of errors.
  * Layout model, user-defined types, resource management, union and variant, span.
  * Bit manipulation. std::bitset contains a rich set of operations on sets of bits.
* Raise the level of abstraction.
  * User-defined types, classes, templates, resource management.
  * Move work from run time to compile time: Inlining of function calls, Overloading (avoid run-time selection), Copy elision and move constructors, Virtual member functions (simple indirection instead of run-time name lookup), "ordinary" function calls, constant expression evaluation, constexpr functions, Type-rich programming (avoid having to write error handlers when the compiler or a static analyzer catches the error).
* Core Guidelines
  * Documented conceptual framework.
  * We can write type and resource-safe C++.
  * Provide guarantees for the absence of certain classes of errors.
  * Distinguish between what can be done and what's reasonable to do.
  * Avoid "dark corners" of the language.
  * Examples: Initialize variables. Use variant vs union. Use read only constant values when possible. Avoid dangling pointers.
* Exceptions and error codes
  * Both are needed
  * Throw exceptions when there is no suitable return path for error codes (constructors and operators).
  * Throw exceptions when an error must percolate back up the call chain to an "ultimate caller" (verbose, tedious, error prone).
  * Exceptions have a run-time cost (example: stack unwinding).
  * Use errors when an immediate caller can reasonably be expected to handle the failure.
  * Use errors on systems with very little memory.
* Foundations of C++
  * Static type system, RAII, Efficient object oriented programming, Flexible and efficient generic programming, Compile-time programming, Direct use of machine and operating system resources.
* Dreams of the future
  * ISO Standard: Executors, Pattern matching, Static reflection, Better library support for coroutines, Make the preprocessor redundant, Integrated support for static analysis.
  * Stability / compatibility.
  * Performance: No bloat in the implementation of language features and standard library components.
  * A package mechanism. A repository of packages.
  * More C++ Core Guidelines.
  * Static analysis supporting code transformation.

