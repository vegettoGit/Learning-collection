## [The C++ Rvalue Lifetime Disaster - Arno Schoedl - C++ on Sea 2023](https://www.youtube.com/watch?v=9V195P3Tv_8)
### Topics covered:
* Rvalue References.
* Rvalue References for Moving - Pitfalls.
* Temporary Lifetime Extension.
  * Temporary Lifetime Extension vs `decltype(auto)`.
* `auto_cref`.
  * `auto_cref_return` for NRVO/move optimization.
* C++ Rvalue Amnesia.
  * Conditional operator afraid of Rvalue Amnesia.
  * C++20 `common_reference` Not Afraid.
* Promises of References.
* Any chance to fix C++?
  * Reference Declarations.
  * How to opt in to new behavior?
  * Impact on Standard Library.
  * Until then... Mitigations.

## [Back to Basics: C++ Move Semantics - Andreas Fertig - CppCon 2022](https://www.youtube.com/watch?v=knEaMpytRMA)
### Topics covered:
* Move semantics: Move or duplicate.
* Overloads.
* Triggering the rvalue-overload. `std::move` is a cast.
* The value categories.
* The place of a potential performance win.
* A "moved from" object is nothing special.
* The Standard Template Library (STL), move and custom object.
* `std::move` is not always the right thing.
* `move` or `forward`.
* Perfect forwarding.
* Use `move` only rarely.
* Compiler-generated special members.
* Utilizing move semantics even more: ref-qualifiers.




