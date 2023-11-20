## [Most Malleable Memory Management Method in C++ - Björn Fahller - C++ on Sea 2023](https://www.youtube.com/watch?v=ptMFLSAkRj0)
### Topics covered:
* The heap.
* Allocators.
* PMR (Polymorphic Memory Resource) Allocators.
  * `memory_resource`.
* `string` frequency example.
  * With and without PMR.
  * The default `memory_resource` is `new_delete_resource`.
  * Using `unsynchronized_pool_resource`.
* Choosing a memory resource.
* PMR for your types.
  * `allocator_type`.

## [C++ Algorithmic Complexity, Data Locality, Parallelism, Compiler Optimizations, & Some Concurrency - Avi Lachmish - CppCon 2022](https://www.youtube.com/watch?v=0iXRRCnurvo)
### Topics covered:
* Cache Friendly Software.
  * Traverse by columns vs Traverse by rows.
* CPU Caches.
  * Data (D-cache), Instruction (I-cache), Translation lookaside buffer (TLB, translation between virtual memory and physical memory).
* Cache Hierarchies.
  * L1, L2, L3.
* CPU Cache Characteristics:
  * Much faster than main memory.
  * 100% CPU utilization, >99% CPU idle time! When profiling, it might look like the CPU is being utilized when it's fetching memory.
* Cache model.
  * K = 2 Way Associative Cache. A cache line's set determines k possible cache locations.
  * Cache lines.
  * Cache Line Prefetching.
  * Types of Cache Misses: Cold Miss, Capacity Miss, Conflict Miss, Sharing Miss (True Sharing, False Sharing).
  * Prefetcher. It works best for predictable linear memory access. Use cache friendly containers that have contiguous memory (`vector`, `flat_set`, `flat_map`), no pointer chasing.
* Code is memory too.
  * Code is also cached, with the same caching behavior as data.
  * Rearrange branches (put cold away from hot).
* Object Oriented Design vs Data Oriented Design.

## [Recipes for Reducing Allocations by C++ Containers - Lukas Böger - C++ on Sea 2022](https://www.youtube.com/watch?v=ukUoLnCOyio)

## [What Do You Mean by "Cache Friendly"? - Björn Fahller - C++ on Sea 2022](https://www.youtube.com/watch?v=yyNWKHoDtMs)

## [Cpu Caches and Why You Care - Scott Meyers - code::dive conference 2014](https://www.youtube.com/watch?v=WDIkqP4JbkE)


