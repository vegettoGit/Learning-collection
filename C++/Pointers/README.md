## [A Lock-Free Atomic Shared Pointer in Modern Cpp - Timur Doumler - CppCon 2022](https://www.youtube.com/watch?v=gTpubZ8N0no&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* We are going to be talking about `atomic<shared_ptr<const T>>`. Being able to manage an object's lifetime across threads, without using locks / mutexes.
* Herb Sutter's sample using `atomic<shared_ptr<Node>>` to implement a concurrent lock-free stack. `atomic` is used for the Head node of the stack. Note the usage of the method `compare_exchange_weak`.
* Quick review of `shared_ptr<T>` based on the standard.
  * Note how the `refcount` in the `control_block` is of type `atomic<size_t>`.
  * Changes on `refcount` are thread safe.
* For loading and storing the actual owned pointer within `std::shared_ptr<T>` in a multithreaded environment, we can use `std::atomic_load` and `std::atomic_store` since C++11. 
  * The functions have been deprecated in C++20 though. The problem with those functions is that they were free standing, they were not part of the std::shared_ptr class and that had various implications.
* Since C++20, we can use `std::atomic<std::shared_ptr<T>>`.
* This is still not lock-free though, which might be something desirable in a low latency environment.
  * As of today, `std::atomic<T>::is_lock_free` and `std::atomic<T>::is_always_lock_free` return false in all compilers for `std::atomic<std::shared_ptr<T>>`.
* There are open source implementations of a lock-free `std::atomic<std::shared_ptr<T>>`
  * Anthony Williams's implementation (proof of concept), author of C++ Concurrency in Action.
  * Folly's implementation by Dave Watson (production).
  * Vladislav Tyulbashev's implementation (proof of concept).
* Lock-free implementation of `std::atomic<std::shared_ptr<T>>`:
  * The control block pointer and the refcount need to be updated as a single operation. 
  * We need a `double compare-and-swap`, for which we don't really have an operation on any modern CPU. 
  * We do have `double-width compare-and-swap` (DWCAS) though. For this to work, however, both memory locations need to be next to each other and aligned properly.
  * The `split refcount` algorithm comes to the rescue.
  * The idea is creating a local refcount and a global refcount. The local refcount is contiguous to the control block pointer (that way we can update them together). The global refcount is just what refcount was originally.
  * The local refcount and global refcount can then be put in sync, by atomically incrementing the global count and decrementing the local count.
* Each atomic<shared_ptr> access:
  * Involves at least 3 atomic operations, more under contention.
  * Is slower than mutex when there is no contention.
  * Is much better than mutex under high contention.
* In reality though, `std::shared_ptr<T>` has more components such as a `weakcount`, a deleter and a custom allocator. Additionally, a pointer to the object T exists in not just the control block, but also in the shared_ptr itself. Do we then need to modify 3 memory locations (control block pointer, local refcount and object pointer) in a single operation? In fact, due to std::shared_ptr's aliasing constructor, where the shared_ptr manages the lifetime of one object, but it's actually pointing to another object (which has the same lifetime as the first object, for example it can be a member of that first object, or a base class), we might need to handle multiple object pointers.
  * Anthony Williams's solution: Instead of storing an object pointer, store an index (alias_index) into another data structure (in the likes of a linked list and with just the push_back operation for growing and a lookup function) which contains the object pointers (base, derived, etc.). Put the local refcount and the alias index into a single integer. The linked list structure requires memory allocations though and that cannot be lock-free. Timur explores a possible solution for that.
* `double-width compare-and-swap` (DWCAS) is supported in every modern CPU:
  * x86: cmpxchg8b
  * x64: cmpxchg16b
  * armv7 / arm64: LL/SC.
* `double-width compare-and-swap` (DWCAS) performance:
  * ~ 2x slower than CAS on x64.
  * ~ 1.5x slower than CAS on arm64.  
* Does DWCAS work with std::atomic?
  * Typically not supported because of ABI.
  * Alternative: "Packet pointer", used by folly and vtyulb, it's 64 bit only.
* Summary of existing free and open-source implementations: anthonywilliams, vtyulb, folly.
* Benchmarks.

## [Back to Basics: C++ Smart Pointers - David Olsen - CppCon 2022](https://www.youtube.com/watch?v=YokY6HzLkXs&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Problems with raw pointers. They have too many uses.
  * Single object vs. array. new vs new[], delete vs delete[], don't use ++p if single.
  * Owning vs. non-owning. The owner must free the memory when done.
  * Nullable vs. non-nullable. Some pointers can never be null, it would be nice if the type system helped enforce that.
  * T* can be used for all combinations of those characteristics.
* Smart Pointer
  * Behaves like a pointer. Can be dereferenced, points to an object.
  * Limits behavior to certain of a pointer's possible roles.
  * Most common: Automatically release resources.
  * Others: Enforce restrictions (such as don't allow nullptr), extra safety checks.
* Good uses of raw pointers
  * Non-owning pointer to a single object. Use a smart pointer for all owning pointers. Use a span type in place of non-owning pointers to arrays (C++20 std::span).
* Unique_ptr
  * Owns memory.
  * Assumes it is the only owner.
  * Automatically destroys the object and deletes memory.
  * Move-only type. No copy constructor or copy assignment operator.
  * Defined in header <memory>.
  * Very useful for implementing RAII.
  * Every unique_ptr member function is noexcept, as it doesn't allocate any resources, it only takes ownership of memory which has already been allocated.
  * It unconditionally deletes the memory in its destructor.
  * Its move constructor transfers ownership.
  * release() gives up ownership without freeing the memory.
* "template<typename T, typename... Args> unique_ptr<T> make_unique(Args&&... args)" is a standard function which allocates memory, constructs a T with the given arguments and wraps it in a std::unique_ptr<T>.
  * Prefer using make_unique to creating a unique_ptr explicitly.
* Both unique_ptr and make_unique have partial specializations for arrays.
* To transfer ownership to a function, pass std::unique_ptr by value.
* To return ownership from a function, return std::unique_ptr by value.
* Shared_ptr
  * Owns memory. The ownership is shared. Many std::shared_ptr objects work together to manage one object.
  * Automatically destroys the object and deletes the memory. Cleanup happens when the last shared_ptr gives up ownership.
  * Copyable.
  * Defined in header <memory>.
  * Usage examples: U widgets, Promise/future.
  * Shared ownership is implemented with reference counting (control block on the heap for bookkeeping).
  * Not all of its functions are noexcept, as it has to allocate memory for the control block as soon as it starts managing an object.
  * The copy constructor increases the count in the control block.
  * The move constructor transfers ownership, in this case the count doesn't change.
  * Doesn't have a release function.
  * use_count() returns the value of count in the control block, but it isn't reliable in a multithreaded environment.
  * Updating the same control block from different threads is thread safe.
  * Updating the same shared_ptr object from different threads is not thread safe.
  * To share ownership, additional shared_ptr objects must be created or assigned from an existing shared_ptr, not from the raw pointer.
* It is possible to transfer unique ownership to shared ownership, but not the other way around.
* "template<typename T, typename... Args> shared_ptr<T> make_shared(Args&&... args)" does one memory allocation for both the object and the control block, constructs T with the given arguments, initializes the control block and wraps them in a std::shared_ptr<T> object.
  * Prefer using make_shared to creating a shared_ptr directly.
* shared_ptr added support for array types in C++17. maked_shared did it in C++20.
* Weak_ptr
  * A non-owning reference to a shared_ptr managed object.
  * Knows when the lifetime of the managed object ends.
  * It can be useful for caching (keep a reference to an object for faster access). It can help with the dangling references problem.
* Custom deleters can be implemented for unique_ptr and shared_ptr.
* Used shared_from_this to convert this into a shared_ptr.

## [Back to Basics: Smart Pointers - Arthur O'Dwyer - CppCon 2019](https://www.youtube.com/watch?v=xGDLkt-jBJ4&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)



