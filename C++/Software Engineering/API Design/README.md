## [Building C++ Interfaces That Are Hard to Use Incorrectly - Andreas Weis - ACCU 2023](https://www.youtube.com/watch?v=PIyZ9aosHQg)
### Topics covered:
* Motivation.
* Categorization of precondition violations.
  * What is incorrect use? `std::vector` example.
  * Function Preconditions.
  * Wide Contracts - Defensive Programming.
  * Precondition Violations: Invalid argument, Invalid context.
* Leveraging the type system to prevent precondition violations.
  * Type System to the rescue!
  * Opaque Types, `glTexImage2D` example, Enumerators, Scoped Enumerators, Scoped Enumerators as Opaque Typedefs, Opaque Typedefs.
  * Structuring arguments.
  * Structured Data Access.
  * Data Types with special properties.
* Techniques for restricting access to data.
  * Limited Friendship. Access Token.
  * Declarative Interface. `glBufferData`, `glVertexAttribPointer` examples.
* Techniques for restricting control flow.
  * Modeling State Through Types. 
  * Two-Phase Initialization.
  * Error Handling Paradigms. C++23 `std::expected`.
  * Execution Tokens.
  * Scoped Execution Contexts.
  * Complex State Machines.
  * The GoF State Pattern.

## [Back to Basics: C++ API Design - Jason Turner - CppCon 2022](https://www.youtube.com/watch?v=zL-vn_pGGgY)
### Topics covered:
* Based on Jason Turner's C++ Best Practices book, item #32: "Make Your API Hard to Use Wrong".
* The Common std::vector (C++98 version).
  * "bool empty() const;" method.
  * Use Better Naming. It could rather be named "is_empty".
  * Should really add [[nodiscard]]. The compiler will now generate a warning if the return value is dropped. [[nodiscard]] can be used with lambdas since C++23 and can be applied to constructors as of C++20. It can also have a message to explain the error. It can be checked / enforced with static analysis.
  * We should also add "noexcept". It notifies the user (and compiler) that a function may not throw an exception (if it does, "terminate" must be called).
* Increasing The Stakes: A Factory Function.
  * Consider using [[nodiscard]].
  * Never Return a Raw Pointer. Consider returning a std::unique_ptr.
  * Use an enum class instead of an int for a widget type (on a widget factory function).
  * Consider using stronger typing to make our factory better. For example, use the "requires" clause to enforce "std::is_base_of_v<Widget, WidgetType>" to make a WidgetType.
  * Have a Consistent Error Handling Policy. Use one consistent method of reporting errors in your library. Strongly avoid out-of-band error reporting (such a "get_last_error()" or "errno") as it destroys the ability to make your library multithreaded. Make errors impossible to ignore (not returning an error code, consider using exceptions instead). Never use std::optional<> to indicate an error condition as it does not convey a reason, and the reason becomes out of band. Consider std::expected<> (C++23) or similar (for example a std::variant of error or returned value). std::expected is constexpr friendly.
* The Humble fopen Function.
  * Consider passing your own deleter to std::unique_ptr. For example, a lambda that closes a file for a std::unique_ptr which stores a pointer to a file.
  * Avoid easily swappable parameters. Two (or more) parameters beside each other of the same type are easy to swap. clang-tidy has a check for this: "[bugprone-easily-swappable-parameters]".
  * Avoid Implicit Conversions / Use Strong Types. Conversion operators and single parameter constructors (including variadic and ones with default parameters) should be "explicit".
* `=delete` Problematic Overloads.
  * Any function can be `=delete`d.
  * if you `=delete` a template, it will become the match for any non-exact parameters, and prevent implicit conversions.
  * (Sparingly) delete problematic overloads / prevent conversions.
* Only Pass Raw Pointers for Single Optional Objects.
  * If you pass a pointer, you must check it for nullptr.
* Prefer & Parameters For Non-Small, Non-Trivial Objects.
* Fuzz Your Interfaces.
  * A Fuzzer is a tool that tests your API against a set of "random" inputs.
  * It should be run with something like address / undefined sanitizers enabled.
  * It uses your API in ways that you never would.
  * Can be used with any API with creativity.
  * Helps discover patterns of misuse internal to your API.
* Enable for constexpr Unless You Have a Really Good Reason Not To.


