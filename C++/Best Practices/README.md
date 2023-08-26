## [Pragmatic Simplicity - Actionable Guidelines To Tame Cpp Complexity - Vittorio Romeo - CppCon 2022](https://www.youtube.com/watch?v=3eH7JRgLnG8)
### Topics covered:
* Focus on low-level complexity: abstraction design, coding style, use of language features, etc.
* Objective: Derive pragmatic and actionable guidelines.
* Defining "simplicity" and "complexity".
* 1st precept: Use the most limited tool for the job.
   * Casting, emplacing, locking.
   * `std::array` vs `T[]`. `std::variant` vs regular virtual polymorphism. `std::byte` vs `char`. `enum class` vs `enum`. `auto&&` vs `const auto&`.
   * `absl::hash_map` vs `std::unordered_map` vs `std::map`.
   * Aggregate types vs non-aggregates.
   * Uniform initialization.
   * `T` -> `std::unique_ptr<T>` -> `std::shared_ptr<T>`.
   * Using `irange` is less powerful than the traditional loop.
* 2nd precept: Value is a function of rarity.
   * Attributes, `auto`, `noexcept`. Sparingly using a feature increases its value and reduces noise.
   * A note on final (on classes). Inheritance in C++ is not always about polymorphism. "strong typedef".
   * `constexpr` functions.
   * Trailing return types. Consistent with 1st precept.
   * `const` variables.
   * `override` contextual keyword.
* A note on consistency.
   * Consistency for the sake of it is harmful.
   * Value correctness and simplicity over consistency. Go for consistency afterwards.

## [Back to Basics: The C++ Core Guidelines - Rainer Grimm - CppCon 2022](https://www.youtube.com/watch?v=UONLB7wBVSc)
### Topics covered:
* Best Practices for the Usage of C++.
* Most Prominent Guidelines.
  * MISRA C++ (2008, C++03): Motor Industry Software Reliability Association.
  * AUTOSAR C++14 (C++14): More and more used in automotive domain.
  * C++ Core Guidelines: Community driven.
* Philosophy:
  * Express intent and ideas directly in code. 
  * Don't waste resources such as space or time. 
  * Encapsulate messy contructs behind a stable interface.
* Interfaces: 
  * Should be explicit, strongly typed, have a low number of arguments, separate similar arguments.
* Functions: 
  * Distinguish between in, in/out and out parameter. 
  * Ownership semantics of function parameters.
* Classes: 
  * Class hierarchies organize related classes into hierarchical structures. 
  * Class vs Struct: Use a class if it has an invariant, establish the invariant in a constructor. 
  * A concrete type (value type) is not part of a type hierarchy, it can be created on the stack and should be regular. 
  * Regular types have the `Big Six` defined (default constructor, copy constructor, copy assignment, move constructor, move assignment, destructor) and additionally swap operator and equality operator. 
  * Make single-element constructors (conversion constructor) and conversion operators `explicit`.
* Enumerations: 
  * Use enumerations to represent sets of related named constants.
  * Prefer enum classes over "plain" enums.
* Resource Management:
  * RAII (Resource Acquisition Is Initialization). 
* Expressions and Statements: 
  * Good names are the most important rule for good software, they should be self-explanatory.
  * Don't mix signed and unsigned arithmetic.
* Performance: 
  * "Premature optimization is the root of all evil" (Donald Knuth). 
  * Measure with real-world data
  * Versionize your performance test. 
  * Enable Optimization: Use move semantics if possible, use `constexpr` if possible.
* Concurrency and Parallelism:
  * Prefer `std::jthread` to `std::thread`. 
  * Don't detach a thread. 
  * If you pass data by value between threads, it should be small, the data should be preferably local, be as local as possible.
  * To share ownership between unrelated threads, use `std::shared_ptr`.
  * Use tools to validate your concurrent code (ThreadSanitizer, CppMem).
* Error Handling:
  * Detect the error, transmit information to handler code.
  * Preserve the valid state of the program.
  * Avoid resource leaks.
* Constants: 
  * Make objects immutable by default, so that they cannot be a victim of a data race and so that we can guarantee they are initialized in a thread-safe way.
  * Casting away const from an original const object is undefined behavior if you modify it.
* Templates and Generic Programming:
  * Use templates to express algorithms that apply to many argument types.
  * Use function objects (lambdas) to pass operations to algorithms.
  * Template arguments should be at least SemiRegular (Regular without equality) or Regular (Big Six).
* The Standard Library:
  * Prefer std::array and std::vector to a C-array. They should be your first choice for a sequence container.
* Guidelines Support Library.

## [Typical C++, But Why? - Björn Fahller - NDC TechTown 2022](https://www.youtube.com/watch?v=PmVmaT1JNbw)

## [Better Code: Data Structures - Sean Parent - CppCon 2015](https://www.youtube.com/watch?v=sWgDk-o-6ZE)



