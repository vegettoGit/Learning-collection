## [Back to Basics: Master C++ Value Categories With Standard Tools - Inbal Levi - CppCon 2022](https://www.youtube.com/watch?v=tH0Z2OvHAd8&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Motivation.
* Intro to value categories.
  * Originally, in the C language, an lvalue was on the left of an assignment and an rvalue (non-lvalue) on the right of the assignment.
  * Value Category of an entity defines its lifetime (can it be moved from, is it a temporary, is it observable after change) and its identity (if its address can be taken and used safely).
  * Affect two very important aspects: Performance and overload resolution.
  * A brief reminder of References.
* What are Value Categories:
  * It's a quality of an expression.
  * What (misleadingly) looks like the value category, can in fact be the type. For example, for "Data&& a", its type is "rvalue reference to Data" and it's Value Category is lvalue.
  * An entity can have a different Value Category in different contexts (example: it might be an rvalue as a parameter on a function call and an lvalue within the body of the function since it now has a name).
  * Each expression has two properties: A type (including CV qualifiers) and a value category.
* Value Categories have changed throughout the history of C++. 
  * C++98 added references, with lvalue being objects, functions and references; and rvalue being a non-lvalue (can be bound by const lvalue reference). 
  * C++11 added rvalue references and move semantics. We now have lvalues (can't be moved from), rvalues (can be moved from), xvalues (can be moved from and have identity) and prvalues (can be moved from and don't have identity).
  * C++17 added guaranteed copy elision. We now talk about "prvalue's materialization" instead of "prvalue".
  * C++20 added Implicitly move from rvalue references in return statements.
  * C++23 added "Deduced this" and "like_t".
* `glvalue` means it has identity. `lvalue` has identity (glvalue) and cannot be moved from. `xvalue` has identity (glvalue) and can be moved from (rvalue).
* `rvalue` means it can be moved from. `prvalue` can be moved from (rvalue) and doesn't have identity.
* Value categories in practice.
  * The Details of Binding. Expressions with different Value Categories "bind" to different types of References. Binding rules are important in initialization / assignment, function call and return statements.
  * Copy Elision Optimizations. Starting from C++17, the behavior of VCs is affected by Guaranteed copy elision.
* Value categories in generic code.
  * Reference collision.
  * Forwarding reference.
* Tools for handling value categories.
  * std::move.
  * std::forward.
  * std::decay.
  * decltype specifier.
  * std::declval.
  * Deducing this (C++23).

