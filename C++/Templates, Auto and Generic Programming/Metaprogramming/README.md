## [Adapting C++20 Ranges Algorithms for Most Metaprogramming Needs in Fewer Than 1,000 Lines of Code - Daisy Hollman & Kris Jusiak - CppNow 2023](https://www.youtube.com/watch?v=69PuizjrgBM)
### Topics covered:
* But why?
* Sorting a `type_list` with `std::sort`.
* Type lists in C++.
  * Parameter packs.
  * Implementation.
  * "Value domain" vs "Type domain".
* Implementing metafunctions using `std::type_identity` (C++20).
* Using a lambda for the Key function.
* Getting the parameter pack out of the type list.
* Implementation strategy.
  * Get the indices for our type list.
  * Enumerating a parameter pack.
  * Problem: `std::sort` doesn't return sorted indices.
  * Sort the indices with `std::sort`. We can shorten this with `std::ranges::sort`.
  * Accessing the Nth element of a pack.
  * Applying `at` for each sorted list.
  * How do two pack expansions interact with each other?
  * The Compare function for the `sort`.
  * Applying Key with `std::variant`.
  * Applying Key another way: Build a jump table from a parameter pack.
  * What if we don't want to assume a common return type?
* Template Meta-Programming with `std::ranges` (C++20). 
  * Why? Use case.
  * `to_tuple`.
  * Motivation example (run-time).
  * Let's do it at compile-time...
  * C++20's `typeid` operator `==` is `constexpr`.
  * How?
  * Don't Repeat Yourself (DRY).
  * Compile-time benchmarks. 

## [Nth Pack Element in C++ - A Case Study - Kris Jusiak - CppCon 2022](https://www.youtube.com/watch?v=MLmDm1XFhEM&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Motivation / Goal.
  * Performance of compilation times, Reflection, Serialization.
  * `std::get<int>(std::tuple{1, 2, 3});` is ambiguous as there are 3 ints we can get from the tuple, not just one.
  * `std::get<1>(std::tuple{1, 2, 3});` is ok, 1 is a valid index in the tuple.
  * Getting the first element is easy. `constexpr auto first_pack_element = [] (auto first, auto... args) { return first; } (args...);`.
  * Last element is quite simple as well: `constexpr auto last_pack_element = (..., (args = args));`.
  * Get both first and last at once: `constexpr auto [first, last] = [] (auto first, auto... ts) { return std::tuple{first, (ts, ...)}; } (1, 2, 3);`.
  * So how can we do `constexpr auto nth = nth_pack_element<N>(1, 2, 3);`?
  * `template<auto N> [[nodiscard]] constexpr auto get(auto t) { return nth_pack_element<N>(...); }`.
* Various solutions to grabbing the Nth pack element since we got Variadic Packs in C++11.
  * std::array (for same types only).
  * Recursion.
  * Arg expansion. Apply Immediately-Invoked Function Expression (IIFE).
  * Concept expansion.
  * Language extension: __type_pack_element (clang), Circle.
* Apply to std::get<N>(tuple).
* Tuples and ranges.
* Benchmarks in different solutions and languages.


