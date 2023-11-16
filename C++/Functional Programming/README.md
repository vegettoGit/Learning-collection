## [And Then() Some(T): C++ Combinators - Higher-Order Functions in Cpp - Victor Ciura - ACCU 2023](https://www.youtube.com/watch?v=bRFLKEfPvgk)
### Topics covered:
* Modern C++ is functional.
* Type Constructors.
* Functor | Applicative | Monad.
* Lifting any function.
* Composition of lifted functions.
* Monadic `std::optional`.
* Heritage.
  * Rust, Haskell (Maybe, Either).
* `std::expected<T, E>`.

## [The Imperatives Must Go! [Functional Programming in Modern C++] - Victor Ciura - CppCon 2022](https://www.youtube.com/watch?v=M5HuOZ4sgJE)
### Topics covered:
* Functional Programming. What is it all about?
  * A style of programming in which the basic method of computation is the application of functions to arguments.
  * A functional language is one that supports and encourages the functional style.
  * Functional: What. Non-Functional: How.
* Paradox of Programming: Machine/Human impedance mismatch.
* Semantics.
* Let's address the elephant in the room...
  * Haskell.
* Historical Background.
* Why (not) Haskell?
  * Functional programming ideas that have been around for 40 years are rediscovered to solve our current software complexity problems.
  * Contemporary C++ has become more functional: lambdas & closures, `std::function`, value types and constants, lazy ranges, folding, mapping, partial application (bind), higher-order functions, monads such as optional, future...
  * A Taste of Haskell.
  * Quick Sort.
* True Story: Word frequencies problem. Donald Knuth, "Programming Pearls" column in the Communications of the ACM journal. Doug Mcllroy.
  * It's all about | pipelines.
* Books
  * Category Theory for Programmers. Bartosz Milewski.
  * Functional Programming in C++. Ivan Cukic.
* Lift Open Source C++ 17 library. Bjorn Fahller.
* Functor | Applicative | Monad.
  * No need to break encapsulation.
  * Better composition (chaining, continuation).
* Type Constructors.
  * There are various ways to hide a value and access the value within.
  * Encapsulate the values of another type into a context.
* Function lifting.
  * Create a higher-order function.
  * `std::optional` can simplify APIs.
  * Lifting any function.
  * Composition of lifted functions.
  * Composition example.
  * Lifting a function to a vector.
* Values.
  * Expressions yield values, Statements do not.
  * Vaue-oriented design reconciles functional and procedural programming by focusing on value semantics. Like functional programming, it promotes local reasoning and composition.
* Immutable.
  * Top 4 places to never use const.
* C++ 20 Ranges.
  * New algorithms, many adaptors, views, actions, pipelines, lazy evaluation, projections, very efficient generated code.
  * A taste of ranges.


