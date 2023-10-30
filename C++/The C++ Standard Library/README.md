## [C++ Standard Views - Nico Josuttis - ACCU 2023](https://www.youtube.com/watch?v=qv29fo9sUjY)
### Topics covered:
* Example: Generic Print Function.
  * Using Abbreviated Function Template Syntax.
  * Using Concepts. `std::ranges::input_range`.
  * Using Views. `std::views::take`, `std::views::transform`.
  * Using Zip Views. `std::views::zip`, `std::views::iota`.
* Example: Pipeline of Range Adaptors. `std::views::filter`, `std::views::take`, `std::views::keys`.
  * Using Iota View. `std::views::filter`, `std::views::drop`, `std::views::take`, `std::views::transform`. 
* C++20: How Views Operate.
* C++20: API of Views.
  * Processing Containers and Views.
  * How expensive is `begin()`? (`vector` vs `list`).
  * Views do not provide expensive member functions.
  * The basic API of views depends on constraints.
  * C++20: Basic View Interface. `view_interface`.
  * Views that Cache `begin()`.
  * Member Functions of Views.
  * Passing Containers and Views by Universal Reference.
  * Concurrent Iterations over Views.
  * Passing Containers and Views by Value. Accepting Only Views by Value. Overloading for Containers and Views.
* C++20: Modifying View Elements.
  * Using the Filter View.
  * Modifications Considered Harmful with Caching. "Use (and reuse) views ad hoc".
  * `cbegin()`
  * Exact Type of Views to Containers. `std::ranges::ref_view` for named objects (lvalues), does not propagate `const`. `std::ranges::owning_view` for temporaries (rvalues), propagates `const`.
  * `zip_view`.
* C++ Views that Just Work.
  * Usability, Safety, Predictability, Performance.

## [What Belongs In The C++ Standard Library? - Bryce Adelstein Lelbach - CppNow 2021](https://www.youtube.com/watch?v=OgM0MYb4DqE)


