## [Using Modern C++ to Eliminate Virtual Functions - Jonathan Gopel - CppCon 2022](https://www.youtube.com/watch?v=gTNJXVmuRRA&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* When virtual is useful.
* Why replace virtual.
* Binding interfaces:
  * Avoid using virtual.
  * Use a concept with a "requires" clause for what would be virtual functions in the virtual case.
  * Use a static_assert to verify that a particular class conforms to a concept.
  * Rule of 0 instead of Rule of 5.
* Owning polymorphic types. Let's compare 2 functionally equivalent approaches (with and without virtual):
  * With virtual, store a unique_ptr as part of the class.
  * Without virtual, template the class with the concept as a constraint, then store a member with the template type. We won't have to specify the template later on when using objects of that class, thanks to CTAD. If we want to be able to change the owned type at runtime, we can store the member as a variant, and use a variadic template on the class. Notice that variant has runtime cost though.
* Storing multiple types:
  * With virtual, use a vector of unique_ptr objects of a class that we can inherit from.
  * Without virtual, we need a container that can hold many different types simultaneously (such as a tuple). We also need a container that can hold multiple objects of a single type (vector, list, etc.). We can use a tuple of vectors, something like "std::tuple<std::vector<TFoos>...>", with the class containing the member tuple being templated with "template<typename... TFoos>", which includes all possible types to be used.
* Downsides of not using virtual:
  * Increased translation unit size. When using virtual, in most cases we just need the base class. Now, we need all types.
  * Potential increase to binary size.
  * May increase compile time.
  * May add complexity and be more difficult to maintain.



