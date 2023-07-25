## [C++20’s Coroutines for Beginners - Andreas Fertig - CppCon 2022](https://www.youtube.com/watch?v=8sEe-4tig_A&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Function vs Coroutine comparison
  * (call & return) vs (call, suspend, co_yield, resume, suspend, co_yield, resume..., co_return)
  * The coroutine decides when it suspends. This makes them a good fit for cooperative multitasking, meaning we don't need locks as we have control on the data.
  * co_yield (output action) and co_await (input action) pause a coroutine.
  * co_return ends a coroutine.
* 2 types of coroutines
  * Stackfull: The data is on the stack.
  * Stackless: The data (coroutine frame) is stored on the heap. This is what we have in C++.
* Simplify code with coroutines
  * Replace callbacks with coroutines.
  * Parsers become much more readable.
  * A lot of the state maintenance code is no longer required.
* Elements of a coroutine
  * Wrapper type (return type of the coroutine function's prototype).
  * promise_type. A coroutine is a finite state machine (FSM) controlled and customized by the promise_type.
  * An awaitable type (optional).
  * An iterator (optional).
* Examples:
  * Coroutine chat: It shows how co_yield, co_await and co_return call functions on the promise_type (yield_value, await_transform and return_value). The Chat struct contains the coroutine handle.
  * Interleave two std::vector objects. It uses a Generator.
  * Scheduling multiple tasks. Tasks call co_await to suspend their execution. Our awaiter struct inherits from std::suspend_always and await_suspend pushes the task back into the scheduler.
* A few definitions
  * Task: A coroutine that does a job without returning a value.
  * Generator: A coroutine that does a job and returns a value (either by co_yield or co_return).
* Helper types for coroutines
  * std::suspend_always
  * std::suspend_never

## [An Introduction to Multithreading in C++20 - Anthony Williams - ACCU 2022](https://www.youtube.com/watch?v=3uH-2CkBlPQ&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### [CppCon 2022 version](https://www.youtube.com/watch?v=A7sVFJLJM-A&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Choosing your Concurrency Model.
  * 2 fundamental reasons we want to use multithreading in our applications: Scalability (Amdahl' law applies) & Separation of Concerns.
  * These reasons inform our choice of model.
* Scalability: Parallel Algorithms.
  * Many standard library algorithms have parallel versions.
  * Example: std::sort, using std::execution par.
  * If this works for you, it's the easiest thing you can do.
  * We can combine consecutive calls: "std::transform(std::execution::par, ...)" and "std::reduce(std::execution::par, ...)". Reduce has to first gather the results from the Transform. In terms of scalability and applying Amdahl' law, it's more efficient to combine them together into "std::transform_reduce(std::execution::par, ...)". 
* Scalability: Independent Tasks.
  * Split your work into many independent tasks and use a (non-standard for now) thread pool.
  * "execute(tp, [] { do_work(); });" where "tp" is of the type "thread_pool".
* Separation of Concerns.
  * Raw performance not a priority.
  * Large sequential tasks that can run concurrently "in the background".
  * Dedicated threads: Run each long-running task on its own thread. Example: "std::jthread gui([]{ run_gui(); })".
* Starting and Managing Threads.
  * Cooperative cancellation. We need a way to interrupt background tasks. Forcibly stopping a thread is undesirable. Instead, C++20 provides std::stop_source and std::stop_token to handle cooperative cancellation. If the target task doesn't check "token.stop_requested()", nothing happens. You can also use std::stop_callback to provide your own cancellation mechanism.
  * Use std::jthread in 99% of cases. std::async can be used where you want a result. std::thread should only be used if you have no choice.
  * Stop tokens are tightly integrated into std::jthread. std::jthread's destructor calls "request_stop()" on std::stop_source (created on std::jthread's constructor) and waits for the owned thread to finish.
  * std::jthread is a value type, it's a handle and it's movable. Ownership can be transferred. It can be stored in containers (example: std::vector<std::jthread>). There is no need to use new (programmers coming from Java).
  * Threads:: Callables and Arguments. The callable and arguments are copied into storage local to the new thread. This helps avoiding dangling references and race conditions. Use std::ref when you really want a reference. Or use a lambda with the reference capture.
* Synchronizing Data.
  * Synchronization facilities: Most multithreaded programs need to share state between threads. We need to watch out for data races (a data race is UB).
  * Use the below in the order listed. If you cannot use one for your case, then see if you can use the next one.
  * Latches. std::latch is a single-use counter that allows threads to wait for the count to reach zero. When it reaches zero, it stays zero, it latches. It's not reusable.
  * Barriers. std::barrier<> is reusable. When the count reaches zero, the barrier is signalled, the completion function is called (on one of the participating threads) and the count is reset. Since it's reusable, we can run this in a loop. Barriers are great for loop synchronization between parallel tasks.
  * Futures. Provide a mechanism for a one-shot transfer of data between threads. std::async launches a task that returns a value. std::promise explicitly sets that value (or an exception). std::packaged_task wraps a task that returns a value, it can be passed into a thread pool. All of these give us a std::future<T> for the result. std::future<T>::get can be called just once, if we call "get" again, it will throw, it's a one-shot. std::shared_future<T> allows multiple threads to receive the same result, we can then call "get" on each thread.
  * Mutexes. Mutual Exclusion. It's a means of preventing concurrent execution. We should use them as sparingly as possible, it can affect the scalability of the application if we start putting mutexes everywhere. C++ provides 6 mutex types, always use std::mutex unless you have a very specific reason to use std::timed_mutex, std::recursive_mutex, std::recursive_timed_mutex, std::shared_mutex or std::shared_timed_mutex. Locking and unlocking is done via RAII types. Use std::scoped_lock (allows us to lock multiple mutexes), unless you have a very good reason to use std::unique_lock (if you are using condition variables), std::lock_guard (if you only want to lock one mutex and you need backwards compatiibility with C++17 or earlier) or std::shared_lock.
  * std::condition_variable. Waiting for data from other threads to be ready. Busy waiting is bad as it consumes CPU time, wastes electricity and delays the notification. std::condition_variable provides notifications to avoid busy waiting. We use its method "wait" and give it a std::unique_lock and a predicate. We can cancel condition variable waits with stop tokens.
  * Semaphores. Represents a number of available "slots". If we acquire a slot on the semaphore then the count is decreased until we release the slot. Attempting to acquire a slot when the count is zero will either block or fail. A thread may release a slot without acquiring one and viceversa. Semaphores can be used to build just about any synchronization mechanism, including latches, barriers and mutexes. A binary semaphore has 2 states (1 slot free or no slots free) and it can be used as a mutex. In C++20, refer to std::counting_semaphore<max_count>. std::binary_semaphore is an alias for std::counting_semaphore<1>.
  * Atomics. They are the lowest level synchronization primitive. They are written std::atomic<T>, where T must be Trivially copyable and Bitwise comparable. Except T can also be std::shared_ptr<U> or std::weak_ptr<U>. std::atomic<T> may not be lock free, it may use an internal mutex (if so, probably a spin lock). std::atomic_flag, std::atomic_signed_lock_free and std::atomic_unsigned_lock_free are the only guaranteed lock-free types. On most platforms, std::atomic<integral-type> and std::atomic<T*> are lock-free. We can query std::atomic<T>::is_always_lock_free.

## [Concurrency in C++: A Programmer’s Overview (part 1 of 2) - Fedor Pikus - CppNow 2022](https://www.youtube.com/watch?v=ywJ4cq67-uc&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [Concurrency in C++: A Programmer’s Overview (part 2 of 2) - Fedor Pikus - CppNow 2022](https://www.youtube.com/watch?v=R0V4xJ9HZpA&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [Lightning Talk: A Spinlock Implementation - Fedor Pikus - CppNow 2022](https://www.youtube.com/watch?v=rmGJc9PXpuE&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

