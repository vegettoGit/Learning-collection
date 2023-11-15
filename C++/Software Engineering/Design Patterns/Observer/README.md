## [Revisiting C++ Observers: Spooky Action at a Distance - Victor Ciura - ACCU 2023](https://www.youtube.com/watch?v=6S3DLHCAGFs)
### Topics covered:
* Design Patterns.
  * GoF.
  * Game Programming Patterns.
  * Facts and Misconceptions.
* Observer Pattern.
  * Examples: MVC, MVVM, Qt signal-slot mechanism.
  * Actors, Actions. Notify Observers when Actions occur. Low Coupling.
* Subscription Model.
  * Subscription Order. Subscribing, Over-subscribing, Unsubscribing.
* Remote Objects.
* Priority.
* Broadcast.
* Small Objects.
* Threads.
  * Don't hold a lock while calling unknown code.
* Observer Proxies.
* Global State.

## [The Observer Design Pattern in Cpp - Mike Shah - CppCon 2022](https://www.youtube.com/watch?v=4GU2YNsHrwg)
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
* Observer Pattern Usage: Java, Godot Engine, Blender3D, Maya3D, Ogre3D.
* Revisiting Angry Birds.



