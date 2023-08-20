## [Back to Basics: Cpp Value Semantics - Klaus Iglberger - CppCon 2022](https://www.youtube.com/watch?v=G9MxNwUoSt0&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* The Source of Classic OO Design Patterns.
  * Design Patterns: Elements of Reusable Object-Oriented Software.
* A Classic Visitor Implementation. 
  * A lot of pointers floating around (indirections affect performance).
  * Manual allocations (involves memory fragmentation).
  * Explicitly managing lifetimes.
* A Value Semantics Solution: `std::variant`. A Modern Visitor Style.
  * It's a value.
  * No base class required (non-intrusive). No inheritance hierarchy. There are no virtual functions.
  * For the code the user writes, there are no pointers or indirections, no manual dynamic memory allocations.
  * No need to manage lifetime. No need for smart pointers.
  * The code is so much simpler (KISS).
  * Better performance.
* Value Semantics:
  * Will make your code easier to write and easier to understand (less code).
  * Will make your code more correct and potentially faster.
  * Is preferable in comparison to reference semantics.
* Reference Semantics: `std::span`.
  * It's dangerous to keep a `std::span` around for longer. For example, if it points to a vector that is then reallocated.
  * It is reasonable to have `std::span` as a function argument.
* Reference Semantics: Reference Parameter. `std::erase`.
* Examples from the Standard Library.
  * The Design of the STL was in terms of Value Semantics. Containers are values (copy implies a deep copy, we don't do a shallow copy). Algorithms take arguments by value.
  * `std::optional` (C++17) is a value type. It's efficient (RVO and move semantics).
  * `std::expected` (C++23) is a value type.
  * `std::function` (C++11) is a value type. Comparison with the Command Design Pattern.
  * `std::any` (C++17) is a value type.

## [Value Semantics: Safety, Independence, Projection, & Future of Programming - Dave Abrahams - CppCon 22](https://www.youtube.com/watch?v=QthAU-t3PQ4&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Global variables cause problems.
  * The same issues apply to Pointers and References.
* Reference semantics.
  * Technical debt.
  * Spooky action: a Lovecraftian tale.
  * Incidental Algorithms.
  * Visibly broken invariants.
  * Race conditions.
  * Surprise mutation.
  * Unspecifiable mutation.
  * Safety. A safe operation cannot cause undefined behavior. A safe language has only safe operations.
  * Safety solutions: Lifetime safety (dynamic allocation + GC/RC, borrow checker/named lifetimes, add static analysis?) and Thread safety (define it and ignore the real problem, borrow checker/named lifetimes, detect and trap). It is possible but not trivial and requires making trade-offs.
  * What about immutability?
  * Tradeoffs. Pick any two: Correctness, Safety, Efficiency, Simplicity.
* Bertrand Meyer ¦ Design by contract.
  * Every operation has a contract: preconditions (what it requires), postconditions (what it delivers), invariants (what it preserves).
  * Every type has a class invariant.
* Local reasoning.
  * The tower of abstraction.
* Value semantics.
  * Definition: Regularity, Independence.
  * Every single mutating operation of any kind has independence as a requirement.
  * The whole-part relationship. Whole-part operational compositions: Copying, Equality, Hashing, Comparison, Assignment, Serialization, Differentiation. Deep and shallow are now red flags.
  * Solution checklist: Technical debt, Spooky action, Visibly broken invariants, Race conditions, Surprise mutation, Unspecifiable mutation.
  * Mutation with independence.
  * Pass-by-value for non-mutation purposes.
* C++ has value semantics.
  * Pass-by-value gives callee an independent value.
  * A returned value is independent in the caller (every rvalue is independent).
  * Default operations uphold regularity and independence: default ctor, copy, assign, destroy, move and comparison.
  * UML has first class notation for whole-part relationships.
* C++ wish list:
  * inout. 
  * in. Pass-by-value without forced copy. You can also think about it as: Pass-by-const&, with a guarantee of independence.
  * Law of exclusivity.
* Achieving value semantics today:
  * Decoupling an object graph.
  * Defining a new type.




