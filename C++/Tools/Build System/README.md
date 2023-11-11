## [Improving C++ Compilation Times: Tools & Techniques - Vittorio Romeo - ACCU 2023](https://www.youtube.com/watch?v=PfHD3BsVsAM)
### Topics covered:
* Why should we care about compilation times?
* Improving compilation times: a flowchart-based approach.
  * Low-hanging fruits: Build System (ninja vs make), Linker (ld vs lld vs mold), compilation cache (ccache, sccache, FASTBuild, Incredibuild), build machine configuration, build machine hardware, PCH (using precompiled headers with CMake, etc.), Unity Builds (coalesce multiple source files into fewer larger ones)...
  * Profiling compilation and dealing with bottlenecks: ClangBuildAnalyzer, CompileScore...
  * Improving physical design: Forward declarations, PImpl, header hygiene, etc.
* A few remarks on C++20 modules.
* Benchmarks and examples from SFML 3.x.
### Goals.
  * Understand what can negatively impact build times.
  * Provide actionable points to improve your compilation times.
  * Call to action: Improve your favorite open-source project's build.
  * Spark some interesting discussion!

## [import CMake, CMake and C++20 Modules - Bill Hoffman - CppCon 2022](https://www.youtube.com/watch?v=5X803cXe02Y)
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





