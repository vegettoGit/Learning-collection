## [The Observer Design Pattern in Cpp - Mike Shah - CppCon 2022](https://www.youtube.com/watch?v=4GU2YNsHrwg&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Angry Birds game example.
* Design Patterns.
  * Make programs more Flexible, Maintainable, Extensible.
  * Design Patterns book, dubbed "Gang of Four" book. Patterns organized in Creational, Structural and Behavioral.
  * The Observer Pattern is Behavioral (concerned with communication between objects).
  * It's a publish/subscribe pattern.
  * It shows up a lot in Model, View, Controller (MVC) systems.
* An object (named the subject) maintains a list of its dependents (observers) and notifies them automatically of any state changes.
* First implementation.
* 2nd Try. Utilizing Interfaces.
* 3rd round. Making our `ISubject` more powerful. `MessageTypes`, Multiple Observers.
* Observer Patter Usage: Java, Godot Engine, Blender3D, Maya3D, Ogre3D.
* Revisiting Angry Birds.

## [Breaking Dependencies - The Visitor Design Pattern in Cpp - Klaus Iglberger - CppCon 2022](https://www.youtube.com/watch?v=PEcy1vYHb8A&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* A Procedural Solution.
  * Maintainability!
* Software must be adaptable to frequent changes.
* An Object-Oriented Solution.
  * Adding operations is intrusive and thus difficult.
  * Adding operations accumulates dependencies.
* Design for the Addition of Operations.
  * Changing interfaces in OOP is difficult. Is it? Design Patterns to the rescue.
  * The Visitor design pattern is the right choice if you want to add operations, but it's not if you want to add types.
* The Design Pattern Reference.
  * Book: "Design Patterns. Elements of Reusable Object-Oriented Software".
* The Classic Visitor Design Pattern.
  * The aspect that changes is extracted and isolated (Visitor). This fulfills the Single-Responsibility Principle (SRP).
  * New operations can be added without modifying any existing code. This fulfills the Open-Closed Principle (OCP).
  * Cyclic Visitor.
  * Disadvantages: Impedes the addition of new types. Restricts operations to the public interface of types. Negatively affects performance (two virtual functions).
  * Implementation-specific disadvantages: Base class required (intrusive!). Promotes heap allocation. Requires memory management.
  * Reference-semantics.
  * OOP style.
  * Scattered memory access.
* A "Modern C++" Solution: What if we use `std::variant`?
  * `std::visit`.
  * Advantages: No inheritance hierarchy (non-intrusive). No cyclic dependency (implementation flexibility). Simpler code (KISS). There are no virtual functions. There are no pointers or indirections. There is no manual dynamic memory allocation. There is no need to manage lifetime. There is no lifetime-related issues (no need for smart pointers). The performance is better (is it?).
  * Value-semantics.
  * Procedural style.
  * Contiguous memory access.
* Performance Comparison.
* Potential Disadvantages of `std::variant`.
  * Not great if alternatives aren't of approximately the same size.
  * Reveals a lot of information (dependencies!).
* The Acyclic Visitor Design Pattern.
  * Beware the performance!

## [The Singleton Pattern - Anti-Pattern or Solution? - Klaus Iglberger - C++ on Sea 2022](https://www.youtube.com/watch?v=3xFpV3cnGbw&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


