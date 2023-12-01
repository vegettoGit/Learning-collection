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
  * Locals, parameters and returns: regisers and stack.
  * Static linking: Global data relocations resolved by linker, function relocations resolved by linker.
  * Dynamic linking: GOT handles global data, PLT + GOT handle functions.
  
## [KEYNOTE: What Everyone Should Know About How Amazing Compilers Are - Matt Godbolt - C++ on Sea 2019](https://www.youtube.com/watch?v=w0sz5WbS5AM)


