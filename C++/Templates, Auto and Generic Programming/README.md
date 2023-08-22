## [Back to Basics: Templates in C++ - Nicolai Josuttis - CppCon 2022](https://www.youtube.com/watch?v=HqsEHG0QJXU&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Templates (C++98).
  * Generic code for arbitrary types/values.
  * Primitive recursive language.
* Function Templates.
  * Generic function code for arbitrary types.
  * Template definition.
  * Template instantiation.
* Generic Iterating.
* Templates in Header Files.
  * They are usually defined (not only declared) in header files. No inline necessary.
* `auto` Parameters for Ordinary Functions (since C++20).
  * Abbreviated function templates.
* Function Template Requirements.
* Concepts (C++20).
  * To formulate formal constraints for generic code.
* Multiple Template Parameters.
* Return Type `auto` (C++14).
* Class Templates (C++98).
  * Generic Member Functions are Only Instantiated if Used.
  * Class Template Argument Deduction (CTAD) (C++17).
* `std::array` is a Templified Aggregate (C++11).
* Non-Type Template Parameter (NTTP) Types.
* Variadic Templates.
  * Templates for a variable number of template arguments, named parameter packs.
  * `if constexpr`.
* `auto` as Function Parameters.
  * Concepts a Type Constraints. Overload resolution prefers more specialized template.
  * `requires` and Compile-Time `if`.

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

## [Mastering Generic Programming | Creative Assembly and BAFTA Games](https://www.youtube.com/watch?v=39dILKKKMqU&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


