## [Implementing a C++ Coroutine Task from Scratch - Dietmar Kühl - ACCU 2023](https://www.youtube.com/watch?v=Npiw4cYElng)
### Topics covered:
* Coroutine Support.
  * No coroutine classes as part of the C++20 standard.
  * The C++23 standard library only provides a generator.
* What could be `co_await`'ed?
  * Async operations (I/O, waiting for another thread), external events (user interaction, other programs), unavailable resources, reordering of data, delayed access.
* Key Concepts: Awaiter (specifying how async work is executed), Promise type (specifying how a coroutine operates).
* value = `co_await` expression;
* Awaiter Type: `await_ready()`, `await_suspend()`, `await_resume()`.
* C f() { ... `co_*` ... }
* Promise Type: `initial_suspend()`, `final_suspend()`, `unhandled_exception()`, `get_return_object()`.
* Demo Time.

## [Deciphering C++ Coroutines - A Diagrammatic Coroutine Cheat Sheet - Andreas Weis - CppCon 2022](https://www.youtube.com/watch?v=J7fYddslH0Q)
### Topics covered:
* Coroutine Basics. Essential use cases for coroutines.
  * Asynchronous computation.
  * Suspend / resume.
  * The coroutine return type.
  * What turns a function into a coroutine?
  * The smallest coroutine. Implementing the return object. `ReturnType`.
  * The coroutine promise. `promise_type`. Implementing the promise. Running the code. `get_return_object`, `initial_suspend`, `final_suspend`, `return_value`, `return_void`, `yield_value`.
  * Coroutine suspension. Awaitable (A type I can call `co_await` on). Implementing the Awaitable. The simplest Awaitable. `await_ready`, `await_suspend`, `await_resume`.
  * Resuming.
  * Coroutine handle interface. Can convert to a promise and viceversa.
  * Getting data out of a coroutine. Getting data into a coroutine.
  * Yielding values.
  * Symmetric transfer.
* Drawing a map of coroutine land.
  * Cheat Sheet.

## [C++20’s Coroutines for Beginners - Andreas Fertig - CppCon 2022](https://www.youtube.com/watch?v=8sEe-4tig_A)
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




