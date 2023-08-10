## [A Tour of C++ Recognised User Type Categories - Nina Ranns - CppCon 2022](https://www.youtube.com/watch?v=pdoUnvTwnr4&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Types with special provisions.
* C++ Object Model.
* Types of objects.
* Objects of user defined type.
* Aggregates.
  * Library trait: `std::is_aggregate`.
* Standard layout types.
  * Distinct address (C++11).
  * Implications of Standard Layout.
  * Common Initial Sequence.
  * Reading from a Union.
  * Library trait: `std::is_standard_layout`.
* Trivial special member functions.
* Trivially copyable type.
  * Implications of Trivially Copyable.
  * Library trait: `std::is_trivially_copyable`.
* Trivial Type.
  * Library trait: `std::is_trivial`.
* What are PODs?
  * Plain Old Data.
  * POD in C++11.
  * Now called trivial standard-layout.
  * Library trait: `std::is_pod`. Introduced in C++11, deprecated in C++20.
* Literal types.
  * Constant expressions. `constexpr` (C++11), `consteval` (C++20), `constinit` (C++20).
  * Limitations of constant expressions.
  * Literal class (C++11).
  * Literal class (C++17). Support for lambdas.
  * Literal class (C++20).
  * Library trait: `std::is_literal_type`. Introduced in C++11, deprecated in C++17, removed in C++20.
* Structural types (C++20).
* Object lifetime before C++20.
* Object lifetime after C++20.
* Implicit-lifetime types.


