## [import CMake, CMake and C++20 Modules - Bill Hoffman - CppCon 2022](https://www.youtube.com/watch?v=5X803cXe02Y&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Where did CMake come from?
* How CMake Changes The Way We Build C++.
* CMake is a Community Effort. Bloomberg is helping, Minecraft is collaborating. CMake support in Visual Studio. CMake in Qt.
* CMake adapts to new technologies so developers don't have to.
* Why CMake is Popular. Commands `add_library()`, `add_executable()`, `add_test()`.
* CMake Workflow.
* Running CMake.
* Modern CMake ("Usage Requirements").
* Presets: `CMakePresets.json` (version controlled) and `CMakeUserPresets.json`.
* Precompiled Headers.
* Full cross platform install system.
* Using CPack: Creates professional platform specific installers.
* Testing with CMake. Running CTest.
* CDash.
* Enter C++ Modules.
  * Build order matters.
  * Built Module Interface (BMI).
  * Build graph multiple targets.
  * Where we are today.
  * `FILE_SET`.
  * Named Module Types.
  * Examples: `mymodule.cpp`, `mymodule_impl.cpp`, `mymodule_part.cpp`, `mymodule_part_impl.cpp`, `mymodule_part_internal.cpp`, cmake code, install and export cmake code.
  * CMake C++20 Modules: gcc, msvc. Simple Example. Module Tests.
* A few more CMake features.

## [Using Incredibuild to Accelerate Static Code Analysis and Builds - Jonathan "Beau" Peck - CppCon 2022](https://www.youtube.com/watch?v=M7zMl2WOp6g&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Setting the Table.
  * Accelerate: Compilation, Shader / Render / VFX, Tests, Static Code Analysis, CI / CD.
* Development Acceleration Platform.
  * How does it work? Process Virtualization.
  * Core Architecture: Initiator, Coordinator, Helpers (Dynamically managed resource pool). Heterogeneous compute.
  * Incredibuild Cloud. Orchestration Service.
  * CI/SpeeD with Github Actions.
  * Static Code Analysis. Klocwork.
* How Can I Use The Platform + Demos.

## [New in Visual Studio 2022 - Conformance, Performance, Important Features - Marian Luparu & Sy Brand - CppCon 2022](https://www.youtube.com/watch?v=vdblR5Ty9f8&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* Conformance.
  * The compiler now supports a few C++23 features.
  * C++20 is complete.
  * Experimental support for Modules + CMake.
  * Demo: CMakePresets.json, vcpkg, Modules + CMake, `std::expected`, `std::stacktrace`, Deducing this, Refactor-aware go-to-definition, etc.
* Performance.
  *  Loop If Unswitching.
  * MinMax. Chained calls now generate less instructions.
  * Stride Backwards Vectorization.
  * ByteSwap. MSVC now better identifies byte swap operations.
* Features of Importance.
  * Inline hints for parameters & auto.
  * Context aware autocomplete for enum types.
  * Speed improvements on Search & Navigaton scenarios: Find all references, Go to File, Find in files.
  * Unreal Engine Integration: New features.
  * Static Analysis improvements.
  * CMake integration.
  * Linux targeting.
  * MacOS targeting.
  * Execution & Static Analysis support on Compiler Explorer.
  * Simplify C++ dependency management with vcpkg.
  * Embedded.
  * Demo: Git integration (Line staging, compare branches within VS), Compiler Explorer, Diagnostics and others.


