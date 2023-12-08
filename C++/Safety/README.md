## [Safety-First: How To Develop C++ Safety-Critical Software - Andreas Weis - CppNow 2023](https://www.youtube.com/watch?v=mUFRDsgjBrE)
### Topics covered:
* Motivation.
  * The Pragmatic Programmer, The Software Craftsman.
* What is safety?
* What are the regulations around functional safety.
* A tour of an ISO safety standard for software.
* Using C++ in a safety-critical environment.

## [Keynote: Safety in C++: All the Safeties! - Sean Parent - C++ on Sea 2023](https://www.youtube.com/watch?v=BaUv9sgLCPc)
### Topics covered:
* Sean's team at Adobe: Improve software development practices.
* Why talk about Safety?
* What is Memory Safety?
* Safety in terms of Safety Properties.
  * What are Safety Properties?
  * Leslie Lamport definition.
  * Example Safety Property for Self Driving Car.
  * Example Liveness Property for Self Driving Car.
* Safety of a Programming Language.
  * Achieving Safety in a Language.
  * What is a Memory Safe Language?
  * Frame rule for Programming Languages.
* What's the Problem?
* Memory Safety in C++.
  * Sanitizers can help, at a performance cost which usually rules them out for production code.
  * If not used in production, combine sanitizers with fuzzers.
  * Not safety properties hold in the presence of UB.
* The Illusion of Safety.
  * Safety is a tool for local reasoning.
* Can C++ be Memory Safe?
* Forward.
  * A (New) Possible Future.

## [C++ and Safety - Timur Doumler - C++ on Sea 2023](https://www.youtube.com/watch?v=imtpoc9jtOE)
### Topics covered:
* Terminology.
  * Safety, security (intentional), correctness.
  * Regulation of safety-critical applications.
  * "Language safety": it exhibits no undefined behavior. Safety refers to: memory (type, bounds, lifetime, initialisation), thread, arithmetic, definition.
  * "Correctness": The state of being free from error.
* So why this talk?
* C++ vs C safety.
* Language safety == no UB.
  * Safety tradeoffs: Performance, backwards compatibility, correctness, complexity, expressivity, portability, cost.
* Memory safety:
  * Type safety: No way to express type punning.
  * Bounds safety: Mandatory bounds checking.
  * Lifetime safety: Three ways to guarantee lifetime safety.
  * Initialisation safety: Enforce explicit initialisation or have implicit initialisation to default value.
* Thread safety.
  * Threadsan.
* Arithmetic safety.
* Definition safety.
  * ODR violations.
  * IFNDR.
* Good news: Tests, code coverage, fuzzing, coding guidelines, code reviews, static analysers, sanitisers.
* There is no safe code.
* How safety-critical is our code? How many users do we have? Who are our users?
* Safety vs Performance.
* Alternatives.

## [Removing Needless Undefined Behavior for a Safer C++ - Alisdair Meredith - ACCU 2023](https://www.youtube.com/watch?v=iY7ft98nM2k)
### Addressing UB for a Safer C++.
### Topics covered:
* Discussion of what we mean by Undefined Behavior.
  * What is a program?
  * What is UB?
  * What is behavior?
  * What is compile-time behavior?
  * What is Unspecified Behavior?
  * What is Implementation-Defined Behavior?
  * Example 1: Demonstrating time travel.
  * Example 2: Is time travel inevitable?
  * What is Undefined Behavior?
  * What are the bounds of Undefined Behavior?
* Undefined Behavior in the process of translating a program.
  * UB at compile time.
  * UB in the preprocessor.
* Common sources of Undefined Behavior.
  * Indeterminate Values. Uninitialised local variables.
  * Indeterminate Values. Beyond local variables.
* Potential improvements.
  * Many ways forward.
  * Erroneous Behavior.
  * Preconditions in core language.
  * Contracts are coming! On target for C++26. Examples.

## [Undefined Behavior in C++: A Performance Viewpoint - Fedor Pikus - CppNow 2022](https://www.youtube.com/watch?v=BbMybgmQBhU)


