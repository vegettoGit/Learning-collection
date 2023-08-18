## [Observability Tools C++: Beyond GDB and printf - Tools to Understand the Behavior of Your Program - Ivica Bogosavljevic - CppCon 2022](https://www.youtube.com/watch?v=C9vmS5xV23A&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* On an unfamiliar codebase, we want to analyze: Hot and cold functions, timeline, memory usage, hardware efficiency, how the program interacts with the operating system. Debuggers and printf aren't enough.
* Observability tools are also useful for debugging weird / unusual behaviors.
* Flamegraphs / Speedscope.
  * It shows stacktraces and time.
  * Data is collected with perf, then we feed speedscope (the visualizer) with it.
* Heap profilers / Heaptrack.
  * Debugging memory consumption issues.
  * Peak Contributions, Largest Memory Leaks, Most Memory Allocations, Most Temporary Allocations.
* Coverage tools / Icov.
  * For each line in your source code, it shows you how many times that line was executed. You might find out that some lines of code were never executed.
  * When running with Icov for debugging, your program will run slower as the compiler has added new lines of code behind the scenes.
* Kernel call tracing / Strace.
  * Observe how your program talks with the OS.
  * Important if the program is spending a lot of time in system mode (when the operating system is doing work for your program).
* Hardware counters and event counters / Perf.
  * Time elapsed (how much in total, in user mode and in system mode), task-clock, context-switches, cpu-migrations, page-faults, cycles, instructions per cycle, branches and  branch-misses.
* Data flow analysis - Pernosco.
* Other debugging tools.
  * Valgrind, Sanitizers, Helgrind, Reverse debugging, etc.


