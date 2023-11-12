## [C++23 - What's In It For You? - Marc Gregoire - CppCon 2022](https://www.youtube.com/watch?v=b0NkuoUkv0M&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* C++23 Core Language:
  * Deducing this.
  * `if consteval`.
  * Multidimensional Subscript Operator.
  * Attributes on Lambda-Expressions.
  * Literal Suffix for `size_t`.
  * auto(x): decay-copy in The Language.
  * `#elifdef`, `#elifndef`, `#warning`.
  * Marking Unreachable Code.
  * Assumptions. `[[assume(expr)]]`.
  * Named Universal Character Escapes.
  * Trim Whitespace Before Line Splicing.
* C++23 Standard Library:
  * String Formatting Improvements.
  * Standard Library Modules.
  * `std::flat_map`, `std::flat_multimap`.
  * `std::mdspan`.
  * `std::generator`.
  * `basic_string(_view)::contains()`.
  * Construct `string(_view)` From `nullptr`.
  * `basic_string::resize_and_overwrite()`.
  * Monadic Operations for `std::optional`.
  * Stacktrace Library.
  * Changes to Ranges Library.
  * Changes to Views Library.
  * `std::expected`.
  * `std::move_only_function`.
  * `std::spanstream`.
  * `std::byteswap()`.
  * `std::to_underlying()`.
  * Associative Containers Heterogeneous Erasure.
* Removed Features.
  * Garbage Collection Support.

## [What’s New in C++23 - Sy Brand - CppCon 2022](https://www.youtube.com/watch?v=vbHWDvY59SQ&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* std::views::chunk(size): Groups the elements in chunks of the given size.
  * There is also std::views::chunk_by, which takes a function instead of a size and groups the elements which return the same value on the function into the same chunk.
* std::print
  * It's like std::format from C++20, but instead of formatting into a string, it formats into a stream.
  * Formatting ranges wasn't a thing in C++20, now you can do it with std::print.
* Compose range adapters together within a lambda, when there isn't an actual range in the lambda.
* [[always_inline]] attribute.
  * Attributes can now be added to lambdas.
* std::views::zip
  * It takes any number of ranges (it's variadic).
  * You get back tuples with elements of each of the ranges (tuple i is made of the elements at position i on each range).
* std::views::zip::transform
  * It takes a function as an input and it yields the result of calling that function on the tuples.
* std::ranges::to<std::unordered_map> (No need to specify the underlying types).
  * Example: Output the result of std::views::zip into an unordered map.
  * Note: An unordered map is pretty much a vector of linked lists under the hood, it's not great in terms of performance, for instance it might cause multiple cache misses.
* std::ranges::to<std::flat_map> (No need to specify the underlying types either).
  * std::flat_map is a new container which splits up our keys and values into 2 contiguous containers. It doesn't use hashing. This is much more cache efficient.
* std::views::cartesian_product
  * Very useful for cases where we want to do a nested loop on a bunch of containers, and then use that result for further operations (such a putting the results into a container, or giving them to a filter).
* Monadic interface for std::optional
  * std::optional::and_then
  * std::optional::transform: Change the value inside an optional, only if there is one.
  * std::optional::or_else
* std::expected: Instead of getting either something or nothing (as it happens with std::optional), we get either something or an error.
* Deduce this:
  * template <class Self> constexpr auto&& value(this Self&& self);
  * We can then use std::forward in our memmber function.
  * We don't have to duplicate code and create a member function for all cases (rvalue, lvalue, const and no const, etc.) any longer.
  * CRTP becomes much easier to write.
* std::generator
  * The first standard library coroutine.
  * On the function with std::generator as return type, co_yield suspends the coroutine and returns the value we want.
  * When calling that function again, the coroutine resumes.
  * Simpler code. With coroutines, the state is carried over every time the coroutine is resumed. We don't have to take care of that state in our code.
* The operator () (call operator) can now be static.
* std::out_ptr. It can be used when we want to manage into a shared pointer a given returned pointer which has been allocated for us.
* std::to_underlying. It converts an enumeration to its underlying type (for example an int).
* std::inout_ptr
* std::is_scoped_enum (a type trait)
* constexpr std::unique_ptr
* std::move_only_function
* std::unreachable. Very useful on switch statements.
* std::mdspan. Multidimensional index.
* std::byteswap. Useful for network APIs.
* consteval for running specific code at compile time.
* constexpr for <cmath>
* std::ospanstream. Create an output stream from an existing buffer
* std::stacktrace::current() outputs onto a std::ospanstream
* std::views::join_with. A new range adapter.
* std::string::contains
* std::ranges::iota
* std::ranges::shift_left, std::ranges::shift_right
* Modules
  * import std; Modules for the standard library

## [How C++23 changes the way we write code - Timur Doumler - NDC TechTown 2022](https://www.youtube.com/watch?v=HdZTw5qLg6A&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [A Preview of C++ 23 - Daniela Engert - NDC TechTown 2022](https://www.youtube.com/watch?v=r8c6ws9Tow0&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [Contemporary C++ in Action - Daniela Engert - C++ on Sea 2022](https://www.youtube.com/watch?v=J_1-Au2MX6Y&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [Keynote: Lightning Updates - Hana Dusíková - C++ on Sea 2022](https://www.youtube.com/watch?v=f5o42_bMidg&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)



