## [C++20’s [[likely]] Attribute - Optimizations, Pessimizations, and [[unlikely]] Consequences - Amir Kirsh & Tomer Vromen - CppCon 2022](https://www.youtube.com/watch?v=RjPK3HKcouA&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Two new attributes in C++20.
* Back to History ("It was there before").
* Code layout
  * Likely ("hot") code paths should be close.
  * Unlikely ("cold") code paths should be far.
  * Reduce I-Cache stress, meaning leave room for hot stuff.
  * Example: A simple switch statement.
* A tale of two branch predictions.
  * The CPU's branch predictor.
  * The compiler's branch predictor.
  * Example: CPU's branch predictor.
  * Example: Compiler's branch predictor. Another example, this time with C++ exceptions.
  * Cold branch: When a branch is encountered for the first time. The CPU remembers the branch by its memory address. Indirect branches (switch/case jump table, call by pointer) are more complicated.
  * Compiler's branch predictor: GCC vs Clang.
* What can the compiler (optimizer) do with this information?
  * It can improve the compiler branch predictor.
  * It can improve the code layout.
  * It may improve the Instructions Cache.
  * The compiler can't really improve the CPU branch predictor. The CPU knows better than us, let it do it's thing.
  * If you really care, use PGO, running it on representative inputs.
* Is it worth the hassle?
  * In the most simple cases, the compiler branch predictor sees the same, with no effect at all.
  * In some caes it is just ignored (it competes with other optimizations).
  * It is easy to have bad `[[likely]]` and `[[unlikely]]` as the code changes (attributes may remain in the wrong place).
  * Consider using `[[likely]]` and `[[unlikely]]` only in cases where the call ratio between the branches would be significantly different than what the compiler would assume, and only in case where it should matter for performance (critical paths). Take a look at the assembly and do your own benchmarks.


