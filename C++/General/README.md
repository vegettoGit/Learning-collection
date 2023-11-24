## [`*(char*)0 = 0;` What Does the C++ Programmer Intend With This Code? - JF Bastien - C++ on Sea 2023](https://www.youtube.com/watch?v=dFIqNZ8VbRY)
### Topics covered:
* Single main function, main entry point (global ctors happen before), normal program termination (calls `std::exit(0)`), global dtors called.
* `reinterpret_cast`.
* `std::bit_cast`.
* SIGSEGV (Address boundary error).
* `volatile char*` (going outside of the C++ abstract machine, do what I mean, avoid speculation, untrusted shared memory, signal handling, external modification).
* There could be something at 0!
  * memory mapped register, interrupt vector table, webassembly, memory protection (virtual vs physical memory address, page table entry).
* ABI.
  * Page table walk.
* Kinds of instructions: arithmetic (+, -, *), control (jump), memory (load, store).
  * Some instructions are multiple memory accesses.
* Registers, Shadow registers.
* Instruction pointer.
* Caches (d$, i$).
  * L1, L2, L3.
  * L1 and L2 are addressed virtually.
  * L3 and Memory are addressed physically.
  * iTLB vs dTLB. We can hit or miss. If we miss, we then do a pagetable lookup, then SEGFAULT might happen.
  * Tools: cachegrind.
* Memory.


## [The Best Parts of C++ - Jason Turner - CppNorth 2022](https://www.youtube.com/watch?v=SRBBfgWm0P8)

## [Keynote: The Tragedy of C++, Acts One & Two - Sean Parent - CppNorth 2022](https://www.youtube.com/watch?v=kZCPURMH744)

## [A Medley of C++ - Walter E Brown - C++ on Sea 2022](https://www.youtube.com/watch?v=dRClYjASTvA)


