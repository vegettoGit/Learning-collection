## [How to Use C++ Dependency Injection to Write Maintainable Software - Francesco Zoffoli - CppCon 2022](https://www.youtube.com/watch?v=l6Y9PqyK1Mc&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Dependency Injection.
  * Observable behaviour, Intended interface, Usage.
  * An interface has a set of pre-conditions and post-conditions. 
  * An interface can have various implementations.
  * We want to decide at a higher level which of the implementations we inject and pass to the user.
  * Never instantiate your own dependency. Dependencies should be passed as parameters.
* Dependencies:
  * How a dependency is passed (example: reference, shared_ptr, etc.) imposes constraints on the user and the component.
* Types of dependencies: Data.
  * Data must always be read-only, we want to avoid action at a distance.
  * Use value-types.
  * Prefer making it explicit (structured types, schematized types).
  * The shape is the interface. For example, we can use a concrete type (`std::vector`), a view object (`std::span`) or a polymorphic object (`any_range`).
  * `std::span` only works with contiguous sequences, whereas `any_range` works with all sequences.
  * For constant data, use `const &`.
  * For data that we are treating as constant (read-only), but might still be changed externally by another thread, use `std::atomic_ref<const T>`.
* Types of dependencies: Behaviour.
  * Stateful effect (server request), get data on-demand (reading a file from disk), perform pure computation.
  * A behaviour can be a Single action or a Bundle of actions.
  * For single action runtime polymorphism, use `std::function` or `std::function_ref`.
  * For single action compile time polymorphism, use a concept leveraging `std::invocable` and `std::invoke_result`.
  * For a bundle with runtime polymorphism, use an Abstract Base Class.
  * For a bundle with static polymorphism, use a concept.
* Passing dependencies to components.
  * Avoid using setters. They enable cycles, confuse lifetimes, force to handle change at runtime, force to handle not being set.
  * Passing to the constructor. Decoupling, Lifetime is automatic, Easy sharing (unless using unique_ptr).
  * Passing as argument to a function.
  * Factories. `shared_ptr` aliasing constructor.
* Abstracting Components.
  * Problem: Complex wiring, knowledge required for wiring.
  * We want to expose higher level components.
  * When implementing an interface, expect a dependency.
  * Use a factory to defer decisions.
  * Use a struct. Use a function that returns the created struct (taking advantage of copy elision and RVO). The constructor does all the wiring for the dependent components. Has automatic lifetime and allows us to expose multiple interfaces (in the public section). However it doesn't support polymorphism (for that we can use the factory).

## [A Practical Guide to Loose Coupling - Kris Jusiak - C++ on Sea 2022](https://www.youtube.com/watch?v=w46l_gG4xQU&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


