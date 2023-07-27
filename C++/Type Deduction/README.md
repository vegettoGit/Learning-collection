## [Embracing Trailing Return Types and `auto` Return SAFELY in Modern C++ - Pablo Halpern - CppCon 2022](https://www.youtube.com/watch?v=Tnl7FnwJ2Uw&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* What we are talking about: Trailing return type and Deduced (auto) returned type.
* This talk follows the format of the book "Embracing Modern C++ Safely", where for each feature the structure is: Description, use cases, potential pitfalls and annoyances. The talk is about 2 features from the book.
* Leading return type vs Trailing return type.
* The Trailing return type can be used with regular functions, with attributes (such as "[[nodiscard]]") or exceptions specifications (such as "noexcept") and with function templates. It can be used for Member functions, in this case the "override" and "final" modifiers go after the Trailing return type, whereas cv and ref qualifiers go before the Trailing return type.
* A few things to note about decltype(expr): 
  * It yields the type of expr, including any reference or cv qualifiers. 
  * These qualifiers can be discarded by using std::remove_cvref_t (since C++20). 
  * Be extra cautious of applying decltype to an id-expression (variable name). 
  * Adding an extra parenthesis means it's not longer an id-expression, it's then a regular expression.
* The Trailing return type makes the code easier to write in various scenarios:
  * Omitting Namespace and Class Qualifiers.
  * Using a Runtime Argument by Name (example: decltype(v.begin()), where v is of the type std::vector<T>).
  * Readable Complex Return Types. Example: If the return type is a pointer-to-function or pointer-to-class-member-function. Another example: Function template return type is dependent on the result of an expression.
  * Lambda expressions: A leading return type cannot be specified for a lambda expression, but a trailing return type can.
* Use Trailing return types a often as desired to improve your code. 
  * Simplifies expression of complex return types and separates return-type logic from the function signature. 
  * Provides consistency between regular function and lambda expression syntax. 
* Trailing return type vs auto return type. 
  * Both have "auto" in the front. With auto return type, the return type is deduced from the return statement. 
  * If there is no return expression, the return type is deduced as void.
* Multiple return Statements Must Yield Exactly the Same Deduced Type, otherwise we get a compilation error.
* Template Parameter Type Deduction: 
  * A template parameter can be decorated to form a reference or pointer to a deduced type. 
  * So for example, "template <typename T> void f(T v)", "template <typename T> void g(T& v)" and "template <typename T> void h(T* v)".
  * When the function is instantiated, the argument is matched with the parameter pattern.
* auto Variable Type Deduction: 
  * Variables whose types are deduced with auto work much the same way as template parameters.
* Decorating the auto Placeholder: 
  * Just like template parameter or auto variable, the return type can be deduced as a (cv-qualified) reference, pointer or function type.
* Deduced Conversion Operators: 
  * Conversion operators can have deduced return types. 
  * Conversion operators cannot have the same prototype, even if they deduce different types.
* Syntactic Limitations: 
  * Declaration and definition must declare their return types the same way. 
  * Disallowed deduction contexts: virtual function, initializer list (it's basically like a temporary, it would be out of scope before we can use it) and template specialization (example: vector<auto> v()).
  * Function type cannot be deduced until body has been seen.
* decltype(auto) Placeholder (introduced in C++14). 
  * Initializing a variable with the auto placeholder discards the top-level cv and ref qualifiers of the expression, whereas the decltype(auto) placeholder preserves them. 
  * The same rule applies for the placeholder used to declare a function with a deduced returned type. 
  * Decorations are not permitted. 
  * Trailing placeholder syntax works and is the only way to use decltype(auto) with a lambda expression.
* Letting the Compiler Apply the Rules. Auto deduction allows us to leave the complexities of type promotion, conversions and overloading to the compiler.
* Returning a Lambda Closure: Requires the use of a deduced return type. A lambda closure cannot be named, even with decltype. Otherwise-identical lambdas have distinct, unique types.
* Perfect Function-Return Forwarding. Returning the result of calling func as a decltype(auto) deduced return type yields exactly the same type as func would yield if called directly.
* Loss of Abstraction. A function is abstract if its interface can be understood independent of its implementation. However, a deduced return type is closely tied to the function's implementation. 
* Loss of Insulation. A function provides insulation if its body can be changed without recompiling its clients (the function definition is in a separate compilation unit). As with inline functions and function templates, the body of a function with a deduced return type must be visible at the point of invocation. Unlike inline functions, the implementation cannot be moved into a separate compilation unit simply by removing the inline keyword.
* Loss of Clarity. Functions with deduced return types are simply harder to read, especially when recursion or forwarding to another function occurs.
* Mitigating the Loss of Abstraction, Insulation and Clarity:
  * Whenever reasonable, use a defined return type.
  * Keep the functions with deduced return types very short, so that the return type is obvious.
  * Document the function carefully, so that reading the implementation is unnecessary to understand its meaning. Describe the qualities of a complex return type.
* Refactoring errors:
  * A defined return type of decltype(expression) preserves expression's value category (non-reference, lvalue reference or rvalue reference).
  * A deduced return type declared as auto discards the value category of the return expression.
  * Be very clear whether you intend to preserve top-level references.
  * Use decltype(auto) to preserve the return expression's value category.
  * Use auto& or auto&& to always return a reference.
  * For defined return types that use decltype, use std::remove_reference_t or std::remove_cvref_t (C++20) to remove top-level references.
* Return-order Sensitivity for Recursion:
  * Runtime recursion: The return type is deduced from the first return statement in the function body. All other return statements must return the same type. For recursive functions, the base case must come first.
  * Compile-time (template) recursion: Requires the base-case overload or specialization to come first.
* No SFINAE on Return Type. 
  * Template programming sometimes depends on substitution failures to quietly remove a function from the overload set. An overload is ignored if the expression is not valid.
  * Substitution failures occur during overload resolution. Return-type deduction occurs after overload resolution selects a function, too late for SFINAE.

## ["Type Deduction and Why You Care" - Scott Meyers - CppCon 2014](https://www.youtube.com/watch?v=wQxj20X-tIU&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


