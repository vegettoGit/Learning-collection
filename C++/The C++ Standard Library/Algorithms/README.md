## [New Algorithms in C++23 - Conor Hoekstra - C++ on Sea 2023](https://www.youtube.com/watch?v=uYFRnsMD9ks)
### Topics covered:
* C++ Algorithm Land Overview.
  * C++98 Iterator Algorithms.
  * C++20 Range Algorithms.
  * C++20/23 Range Adaptors and Factories.
* C++23 Ranges Status.
  * `iota`, `chunk`, `chunk_by`, `slide`, `stride`, `repeat`, `take`, `zip_transform`, `zip`, `adjacent`, `pairwise`, `adjacent_transform`, `pairwise_transform`, `join_with`, `cartesian_product`, `enumerate`. 
* Collection Oriented Programming.
* Warm Up: Num Negatives.
* Sushi for Two.
* Max Gap.
* `filter_out_html_tags`.

## [The Dark Corner of STL in Cpp: MinMax Algorithms - Simon Toth - CppCon 2022](https://www.youtube.com/watch?v=jBeTvNgW25M)
### Topics covered:
* How hard is it to call `std::min`? (or others such as `std::max`, `std::clamp`, `std::minmax`)
  * We can end up with a dangling reference on `std::min`'s returned reference, when either argument on `std::min` is a prvalue.
  * With `std::min`, when we return with auto though, we end up with a copy. 
  * This doesn't happen however with `std::minmax`, as it returns a pair, so in this case with auto we are copying the pair, which still contains the dangling references.
  * What if we return structure bindings? Such as `auto [x, y] = std::minmax(1, 2);`. The types of x and y will still match the types of the pair, which are references.
  * We can be try use a `std::pair<int, int>` type: `std::pair<int, int> a = std::minmax(1, 2)`, this looks fine at compile time. An address sanitizer can detect a `stack use after scope` error here at runtime though. There is no way to detect this at compile time.
  * C++20 range versions have identical behavior: `range_value_t<R> min(R&& r, Comp comp, Proj proj);`.
  * C++14 initializer_list variants return by value. `auto x = std::min({1, 2});` and `auto y = std::minmax({1, 2});` are fine. `const int& z = std::min({1, 2});` is also fine because of lifetime extension (temporary bound to a reference, the lifetime of the temporary is extended to be the lifetime of the variable).
  * The problem is that this doesn't work with MoveOnly types. The following doesn't compile: `auto x = std::min({MoveOnly, MoveOnly})`. This can also be a problem when called with large types which are expensive to copy.
  * const correctness. We can do something like `std::min(a, b).do_something();`, but then `do_something()` needs to be const, and that's because `std::min` returns `const&`. If we want it to not be const (we might want to invoke std::min with mutable lvalue arguments), we can use `const_cast` on what `std::min` returns, but that has other implications.
* Can we fix it?
  * Remove the need for `const_cast`. Return (pair of) lvalue reference.
  * Remove the potential dangling reference. Return by value.
  * Avoid excessive copies. Only copy when returning by value and only the arguments that are returned.

## [Beginners Guide to C++'s Best Kept Secret -- std::algorithm - Mike Shah - C++ on Sea 2022](https://www.youtube.com/watch?v=muOR1d8ULQo)

## [The Twin Algorithms - Conor Hoekstra - CppNorth 2022](https://www.youtube.com/watch?v=w37XnvIf6qE)

## [Better Algorithm Intuition - Conor Hoekstra - Meeting C++ 2019](https://www.youtube.com/watch?v=TSZzvo4htTQ)

## [Algorithm Intuition - Conor Hoekstra - C++Now 2019](https://www.youtube.com/watch?v=48gV1SNm3WA)

## [105 STL Algorithms in Less Than an Hour - Jonathan Boccara - CppCon 2018](https://www.youtube.com/watch?v=2olsGf6JIkU)

## [Fantastic Algorithms and Where To Find Them - Nicholas Ormrod - CppCon 2017](https://www.youtube.com/watch?v=YA-nB2wjVcI)



