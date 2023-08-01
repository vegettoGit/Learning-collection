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
  * `template<auto N> [[nodiscard]] constexpr auto get(auto t) { return nth_pack_element<N>(...);`.
* Various solutions to grabbing the <N>th pack element since we got Variadic Packs in C++11.
  * std::array (for same types only).
  * Recursion.
  * Arg expansion. Apply Immediately-Invoked Function Expression (IIFE).
  * Concept expansion.
  * Language extension: __type_pack_element (clang), Circle.
* Apply to std::get<N>(tuple).
* Tuples and ranges.
* Benchmarks in different solutions and languages.

## [Mastering Generic Programming | Creative Assembly and BAFTA Games](https://www.youtube.com/watch?v=39dILKKKMqU&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


