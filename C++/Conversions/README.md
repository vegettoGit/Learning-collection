## [Taking a Byte Out of C++ - Avoiding Punning by Starting Lifetimes - Robert Leahy - CppCon 2022](https://www.youtube.com/watch?v=pbkQG09grFw&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* No Type Punning.
  * An object within its lifetime may only be accessed in certain ways. Any other access modality is Undefined Behavior.
  * Bytes which constitute an object reside in storage.
* C++ Has an Object Model.
  * Duration of storage is not necessarily the same as object lifetime.
  * Accessing an object outside of its lifetime is Undefined Behavior.
  * Meaningfulness of the concept of an object is not necessarily related to storage.
* C++ Types May Have Invariants. 
  * Types with basic values and no invariants are trivial types.
  * Trivial types still have lifetimes.
* Implicit-Lifetime Types (C++20).
  * Certain types are "implicit-lifetime" types. Aggregate types. At least one trivial constructor and trivial destructor.
  * Certain operations implicitly create objects of implicit-lifetime type. `std::malloc`, `std::memcpy`, `std::memmove`. Starting lifetime of array of `char`, `unsigned char` or `std::byte`. `operator new` and `operator new[]`.
  * Implicit lifetime rules enable zero copy techniques with well-defined behavior.
* `std::bit_cast`.
  * Creates an object whose value representation is that of another object.
  * Objects must be the same size.
  * Objects must both be trivially copyable.
* `start_lifetime_as`, `start_lifetime_as_array`.
* Ending an Object's Lifetime:
  * Lifetime can end in the usual ways: Object with automatic storage duration goes out of scope. Object with dynamic storage duration is deleted.
  * Can also end in other ways: Pseudo-destructor call (`t.~T()`, `ptr->~T()`. Reuse of backing storage.
* `std::launder`.
  * Reusing storage invalidates pointers and references to the old object. Unless the old and new objects are "transparently replaceable". Pointers point to the storage but no longer to the object.
  * `std::launder` obtains a pointer to the object from a pointer to the storage.

## [Programming for Warm Days: Avoiding Dangerous Conversions - Patrice Roy - CppNorth 2022](https://www.youtube.com/watch?v=w0XwXAo1frw&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)




