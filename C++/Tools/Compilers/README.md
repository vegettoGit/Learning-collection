## [What's New in Compiler Explorer? - Matt Godbolt - C++ on Sea 2023](https://www.youtube.com/watch?v=O5sEug_iaf4)
### Topics covered:
* What? Why? When? How? Who?
* The talk goes through a series of User Journeys.
* Low latency trader user: 
  * Sum Over an Array example.
  * Diff View.
  * History feature.
  * Analysis, `llvm-mca`: Total Cycles, Iterations, Instructions, etc.
  * Inlining: Link Time Optimization.
  * IDE mode.
  * Templates.
* Online C++ Trainer user:
  * Teaching.
  * Compiler overrides: Target architecture, etc.
  * Mouse over.
  * Control Flow Graph.
  * Execution.
  * Include Libraries.
  * Linking.
  * Clang Tidy.
  * Sonar.
* User who writes code that pushes the boundaries of C++:
  * AST.
  * Compiler internals. LLVM pass viewer.
  * Will it compile? Conformance view.
* Software developer who writes emulators in his spare time (Matt Godbolt).
  * Stack view, optimization view, GPU execution, Windows execution, etc.

## [What Happens After The Compiler in C++ (How Linking Works) - Anders Schau Knatten - C++ on Sea 2023](https://www.youtube.com/watch?v=h4s891KVN80)
### Topics covered:
* A Simple Function.
  * Instruction pointer (`rip`). `jmp` changes `rip`.
  * `eax` (return register).
  * Inspecting binaries: `objdump`, `xxd`, etc.
  * Executable: header, `.text`, `.data`.
* Relocations.
  * Static: Avoid relocation.
* More Files!
* Data.
  * Calling convention. 
  * `edi`, `esi` registers.
  * `rbp` (the stack pointer).
  * Parameters, locals, globals.
  * `.data` section (global data, internal data, extern data)
  * `.bss` section (uninitialized data, zero data).
  * `.rodata` section (read only data).
* Dynamic Linking.
* Shared objects really are very shared.
  * `.text` directly mapped into memory.
  * Many processes share the same `.text`.
  * `.got` (Global offset table): A table of where all my globals are.
  * `.plt` (Procedure linkage table). Looks in `.got`, but the first time the address is not in `.got` yet and we have to go through the loader.
  * Each process has a separate `.plt` and a separate `.got`.
* Summary:
  * Locals, parameters and returns: registers and stack.
  * Static linking: Global data relocations resolved by linker, function relocations resolved by linker.
  * Dynamic linking: GOT handles global data, PLT + GOT handle functions.
  
## [KEYNOTE: What Everyone Should Know About How Amazing Compilers Are - Matt Godbolt - C++ on Sea 2019](https://www.youtube.com/watch?v=w0sz5WbS5AM)


