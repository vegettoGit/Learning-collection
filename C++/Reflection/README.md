## [Reflection in C++ - Past, Present, and Hopeful Future - Andrei Alexandrescu - CppCon 2022](https://www.youtube.com/watch?v=YXIVw6QFgAI&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Design by Reflection. Topics covered:
* What is Reflection?
  * Ability of a program to observe its own code and shape its behavior accordingly.
  * On C++ we focus on compile-time reflection and generic code. It's the ability of a template to query details of its template parameters and shape its definition accordingly.
  * Insertion: Code generation driven by reflection.
* Motivation.
  * Why do we care about adding reflection to C++?
  * The MLOC challenge. We must look at increasing leverage: more correct behaviors from fewer lines of code.
  * There is a lot more to reflection than boilerplate (contiguous block of repetitive, lightly patterned code).
  * Example: `tainted_string` implementation. What does it take to implement it with private inheritance? We now have to do things like copy the iterators, since `std::string` defines its own. We can't encode the notion of copying a type. This is the very opposite of abstraction. Flexible code customization is key to true reuse.
  * Example: Container adaptors such as `std::stack`, `std::queue`, `std::priority_queue`. They rigidly code to the least common denominator, with a fixed interface and fixed assumptions (such as no random access in `std::stack`). We want to adapt the interface to the container capabilities, offering optional types and capabilities depending on host.
  * Example: Scott Meyers's Effective STL Item 2 (Beware the illusion of container-independent code). Lack of reflection forces generic code to work against rigid syntactic interfaces, least common denominator functionality, have little recourse in face of syntactic / semantic variation, fail to compile instead of flexibly offering limited interfaces and use any number of tricks (boilerplate!) to compensate for the lack of simple compile-time queries about types.
  * Example: Powerset interfaces. Witht reflection, any interface is a powerset of interfaces, may define a subset of methods in the spec.
* Brief History and Related Work.
  * A few words on historical developments and carrying good lessons forward.
  * LISP naturally has reflection. The data and code syntax is the same.
  * Aspect Oriented Programming: Doesn't focus so much on code generation.
  * There are various macro (preprocessor) systems (Lisp, Dylan, Rust), which focus on code generation less than introspection. The macros can also be used for introspection though.
  * More recent work: Circle, Julia reflection, Rust macros, D reflection, Herb Sutter's Metaclasses.
  * Static reflection is on the verge of becoming mainstream.
  * Modern C++ power makes the language ready: `consteval`, CT `new`, CT `std::allocator`, CT `std::vector` and CT `std::string` were specifically added for supporting reflection.
* Static Reflection in C++:
  * Template-based: reflection of a type is an instance of a template (use with template metaprogramming). This can be problematic for memory, as every instance of a template is alive for the whole compilation time.
  * Inheritance-based: inheritance tree mimics the grammar. Quite difficult to use in practice, inefficient during compilation.
  * Value-based: Use conste(xpr | val) to manipulate, using "mainstream" C++ code style. This is the sweet spot for C++.
* A word on Reflection in the D Language. Some of its capabilities are being proposed for C++.
* A word on Reflection in the Rust Language: Not really reflection as much as "powerful macros that can do much of what reflection does".
* `P1240:` status, suggestions and aspirations. C++ proposed basic primitives:
  * Proposal walk-through with examples.
  * Alias to value. `T` is a type/name of a namespace/identifier/expression etc. `^T` (reified) yields a `constexpr` value of type `meta::info`.
  * Convert value back to alias. `e` is a compile-time value of type `meta::info`. `[ :e: ]` yields a template name or type.
  * Reciprocity axioms. `[ :^T: ]` is `T` and `^[ :e: ]` is `e`. Allows code to control insertion.
  * A host of primitives for manipulating `meta::info` values, under the guise of regular `consteval` function to the user.
  * Example: Print the name  of an Enum. Algorithm selection during compilation.
  * Operations on reified values: Add const to reflected type, instantiate template `r` with arguments `rs`, get the type "reference to `r`", get the type "pointer to `r`", if `c` get type `r1` otherwise `r2`.
  * Example (aspirational): Define a "traced" class (parrot all method definitions of a given class, add tracing in tow), such as `traced<Widget>` or `traced<vector<int>>`.
  * Example (aspirational): Pass by Alias / Name. Only trace user-chosen methods. The methods to trace are passed as template variadic arguments.
  * Embedded DSLS: Two-way integration. Generate `SQL CREATE TABLE` statementss from C++ struct fields (proposed example), generate C++ struct/bindings from `SQL CREATE TABLE/SELECT` (aspirational), generate parser from grammar spec (mother lode).




