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



