## [Implementing Understandable World Class Hash Tables in C++ - Eduardo Madrid, Scott Bruce - CppCon 2022](https://www.youtube.com/watch?v=IMnbytvHCjM&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* What is required for fast hash tables?
  * Locality friendly algorithm. Retrieving cache lines is expensive.
  * Parallel computation. Check keys in parallel.
  * Efficient encoding of metadata. Keys & Values.
* Hash Table Briefing.
  * Chaining (Closed addressing). Extremely bad locality. `std::unordered_map` uses chaining.
  * Probing (Open addressing).
* Robin Hood Fundamentals.  
  * Linear probed hash table.
  * Home index, Actual Index, PSL (Probe Sequence Length).
  * Insertion.
  * Search. Maximum length of the operation is log(table size), with a non-adversarial hash function.
  * Delete.
  * Locality Friendly. Max probe lengths grow slowly.
* Some other hashtable designs.
  * Skarupke's Robin Hood Hash.
  * Martinus's Robin Hood Hash.
  * Google/Abseil's SwissTable / related hash tables. Uses SIMD for broad metadata block check.
  * F14 SIMD hash map (Facebook's Folly library). It avoids overhead by chunking.
* Design and Goals.
  * Very high performance, type erased dynamic tables, generic programming, zero cost abstraction layers, and others.
* SWAR (SIMD within a register).
  * Safety.
* Generic Programming.
* Better Instruction Cost Models.
* Design for High Load Factor.
* Table Parameterization: Metadata, Data Layout.
* Type Erasure for Runtime Optimization.
* Implementation details.
  * Metadata Bit Packing, The Sharpest Needle, Hash vs Scatter and Hoist, Deterministic code, Insertion and Eviction Chains, Division is wildly expensive, Deletion by Shifting Back, Resizing.
* Results.

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


