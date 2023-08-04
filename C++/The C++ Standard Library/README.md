## [Back to Basics: Standard Library Containers in Cpp - Rainer Grimm - CppCon 2022](https://www.youtube.com/watch?v=ZMUKa2kWtTk&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* General:
  * Overview. STL (Containers, Iterators, Algorithms).
  * Common Interface. `template<typename T, typename Allocator = std::allocator<T>> class vector;`. Containers provide value semantics. Some functions in the interface are: Constructor, destructor, size, erase, erase_if, comparisons, assignment, swap and so on.
  * Range-based for loop. Be aware that auto is not const by default and non-intended copies could be being made.
* Sequence containers:
  * std::array (C++11). Cannot change its size during run time. It has a fixed size, which is set at compile time. Provides random access.
  * std::vector. It' a dynamic array. Provides random access. Strength: 95% solution. Weakness: Insertion and deletion at arbitrary positions, O(n). Optimized for access to the end with O(1). Iterator invalidation.
  * std::deque (Double ended queue). It's a sequence of arrays. Provides random access. Strength: Insert and delete at begin and end. Weakness: Insertion and deletion at arbitrary positions, O(n). Optimized for begin O(1) and end O(1). Iterator invalidation.
  * std::list. It's a doubly linked list. Provides forward and backward access. Strength: Insert and delete at each position. Weakness: No random access. Optimized for begin O(1) and end O(1). No iterator invalidation.
  * std::forward_list (C++11). It's a single linked list. Does not know its length. Provides forward access only. Strength: Fast insertion and deletion, minimal memory requirements. Weakness: No random access. Optimized for begin O(1). No iterator invalidation.
* Ordered Associative Containers: std::map, std::set, std::multimap, std::multiset. They are sorted.
  * Structure. They are binary balanced search trees. Sorted in ascending order on the key (by default). Have a type(s), comparison function and an allocator.
  * Implementation. std::maps's index operator [] creates a new key/value pair if the key is not available, invoking the default constructor of the value. This happens even when reading. To avoid this, we can use "at" instead of "[]".
* Unordered Associative Containers (C++11): std::unondered_map, std::unordered_set, std::unordered_multimap, std::unordered_multiset. Also known as dictionary, associative arrays or hash tables. They extend the interface of the ordered associative containers.
  * Structure. They are a sequence of (key, value) pairs. Have a data type(s), hash function, equal function and an allocator.
  * Implementation. Apply the hash function on the key. This gives us a unique id. Apply unique id % number of buckets, this gives us a bucket to access to so we can get the value. The hash operation is constant O(1) but searching on the bucket is linear O(n), which is why we want to keep the buckets as small a possible. The Load Factor is the average number of elements of each bucket. Rehashing means that new buckets are created by default if the load factor is bigger than 1.
* Best Friends:
  * Sequence Containers. Prefer std::array and std::vector to a C-array. Use std::array if the container size is known at compile time and small (the stack is 1 to 2 Mb). Use std::vector if the container size is not known at compile time or big. std::vector and std::array manage their memory (RAII) and have an ideal memory layout (contiguous).
  * Associative Containers. std::unordered_map is your best friend.

## [The Dark Corner of STL in Cpp: MinMax Algorithms - Simon Toth - CppCon 2022](https://www.youtube.com/watch?v=jBeTvNgW25M&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* How hard is it to call `std::min`? (or others such as `std::max`, `std::clamp`, `std::minmax`)
  * We can end up with a dangling reference on `std::min`'s returned reference, when either argument on `std::min` is a prvalue.
  * With `std::min`, when we return with auto though, we end up with a copy. 
  * This doesn't happen however with `std::minmax`, as it returns a pair, so in this case with auto we are copying the pair, which still contains the dangling references.
  * What if we return structure bindings? Such as `auto [x, y] = std::minmax(1, 2);`. The types of x and y will still match the types of the pair, which are references.
  * We can be try use a `std::pair<int, int>` type: `std::pair<int, int> a = std::minmax(1, 2)`, this looks fine at compile time. An address sanitizer can detect a `stack use after scope` error here at runtime though. There is no way to detect this at compile time.
  * C++20 range versions have identical behavior: `range_value_t<R> min(R&& r, Comp comp, Proj proj);`.
  * C++14 initializer_list variants return by value. `auto x = std::min({1, 2});` and `auto y = std::minmax({1, 2});` are fine. `const int& z = std::min({1, 2});` is also fine because of lifetime extension (temporary bound to a reference, the lifetime of the temporary is extended to be the lifetime of the variable).
  * The problem is that this doesn't work with MoveOnly types. The following doesn't compile: `auto x = std::min({MoveOnly, MoveOnly})`. This can also be a problem when called with large types which are expensive to copy.
  * const correctness. We can do something like `std::min(a, b).do_something();`, but then `do_something()` needs to be const, and that's because `std::min` returns `const&`. If we want it to not be const (we might want to invoke std::min with mutable lvalue arguments), we can use `const_cast` on what `std::min` returns, but that has other implications.
* Can we fix it?
  * Remove the need for `const_cast`. Return (pair of) lvalue reference.
  * Remove the potential dangling reference. Return by value.
  * Avoid excessive copies. Only copy when returning by value and only the arguments that are returned.

## [Multidimensional C++ - Bryce Adelstein Lelbach - CppNorth 2022](https://www.youtube.com/watch?v=aFCLmQEkPUw&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [What Belongs In The C++ Standard Library? - Bryce Adelstein Lelbach - CppNow 2021](https://www.youtube.com/watch?v=OgM0MYb4DqE&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)


