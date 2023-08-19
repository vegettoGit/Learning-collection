## [How Microsoft Uses C++ to Deliver Office - Huge Size, Small Components - Zachary Henkel - CppCon 2022](https://www.youtube.com/watch?v=0QtX-nMlz0Q&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Background
* Huge Size:
  * How Many Lines of Code?
  * Preprocessor.
  * Alternative Measure for C++: Unique translation units, count compilations.
  * Total Office compiler invocations: 2 Million.
  * Costs of size. Workload, Static Analysis, Migration scope, Tests, Decommissioning.
  * Value of expanding size.
  * Is it valuable to have a huge codebase? It depends.
* Small Components (termed liblets).
  * 1995: Common functionality moved to shared library. `MSO.dll`.
  * 2011: Liblets to the rescue!
  * Layers.
  * Modern C++, Distinct public API, Self Contained, Clean Dependencies, Unit Tested.
  * Liblet success.
* What's next:
  * Header Units. Binany representation of a header file. Produces the same format as named modules. Recommended alternative to PCH (precompiled headers).
  * Liblets + Header Units.



