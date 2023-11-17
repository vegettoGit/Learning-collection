## [Keynote: C++ Horizons - Bryce Adelstein Lelbach - ACCU 2023](https://www.youtube.com/watch?v=efrgipu94Oc)
### Topics covered:
* C++20 is in the field.
  * Modules, Coroutines, Concepts, Ranges.
* C++23 is coming!
  * More ranges, Formatted output, `mdspan`, `expected`, `import std`, Deducing this.
* On The Horizon For C++.
  * Reflection, Pattern Matching, Senders.
* Reflection.
  * Extract information from the program itself.
  * Program, Metaprogram.
  * Reify operator, Splice operator, Identifier splice operator, Splice pack expansion.
  * Example: Array of Structs to Struct of Arrays.
* Pattern Matching.
  * Selection in C++, `inspect`.
  * Pattern guards.
  * Compound patterns, Alternative patterns, Extractor patterns.
  * Example: Generate JSON from C++ types.
* Senders.
  * Today, C++ has no standard model for asynchrony.
  * The solution (Senders) is coming soon.
  * Schedulers are handlers to execution contexts. Schedulers produce Senders.
  * Senders represent asynchronous work. They eventually send a Signal.
  * Receivers process asynchronous Signals.
  * Senders can be composed together to form Task Graphs.
  * Pipe syntax.

## [Can C++ be 10x Simpler & Safer? - Herb Sutter - CppCon 2022](https://www.youtube.com/watch?v=ELeZAKCN4tY)
### Topics covered:
* C++ has a lot of challenges.
* The industry is doing lots of major C++ evolution experiments. This is one of those.
* Talk focus
  * Refresh C++ itself.
  * Make C++ guidance default: 90% less total guidance to teach in C++ books and courses.
  * Make C++ modules default.
  * Keep C++ ecosystem / packagers.
  * Keep C++ compatibility.
* Analogy on how Bjarne solved key C issues by creating C++, and how something similar could be done now to solve C++ problems.
  * cppfront: Cpp2 -> Cpp1.
  * Let's embrace C++, but it needs to be safer, simpler and more toolable.
* cppfront can be built using any major C++20 compiler (MSVC, gcc, Clang).
* "syntax 2" code can be built with any major C++20 compiler, with cppfront/include in the include path.
* Design principle: Be consistent, be orthogonal, be general.
* C++23 "import std;" is implicit. Modules-first, fast build.
* There are no references in Cpp2.
 * "inout" for parameter passing.
* The "_" wildcard is an implicit template.
* Order independence. No forward declarations in Cpp2, because we forward declare everything in Cpp1.
* Default [[nodiscard]]
* Normal CTAD.
* UFCS.
* Readable Cpp1, we can switch to Cpp1 anytime and keep our code.
* Self-contained support library header.
* Left-to-right unary operators.
* Readable Cpp1 in my personal formatting style.
* With Cpp2, "Don't pay for what you don't use" is being applied to backwards compatibility.
* Safety
  * Type safety (Cppcon 2021). Implement using "as".
  * Bounds safety. Example: Don't ++ a pointer, use std::span instead, with std::span internally doing a bounds check. Also refer to cpp2::assert_in_bounds (generated for us in code) and cpp2::Bounds::set_handler (call our code when the assert happens).
  * Lifetime safety (Cppcon 2015).
  * Initialization safety (Cppcon 2020). Refer to the generated code cpp2::deferred_init (initialization without assignment) and construct (called on first assignment).
* Simplicity examples.
  * Parameter passing (Cppcon 2020).
  * Parameter styles: in (the generated "cpp2::in" is automatically const), copy, inout, move, forward. "std::move" can be automatically called for a definite last use of a "copy" parameter.
* Consistency in functions: named function, unnamed function and range-for body. See how unnamed function (lambdas) captures are handled.


