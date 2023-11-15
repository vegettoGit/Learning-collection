## [C++ Electronic Trading for Cpp Programmers - Mathias Gaunard - ACCU 2023](https://www.youtube.com/watch?v=ltT2fDqBCEo)
### Topics covered:
* C++ jobs in Trading.
  * Back-Office, Mid-office, Front-office.
* Trading in a nutshell.
  * Exchange assets for profit.
  * Matching. Continuous matching. Active vs Passive.
  * Order book: Data structures.
  * Strategy: Capture the spread, Aim for no risk. Asset Management.
* Connectivity.
  * Feeds.
  * Protocol considerations. Unicast vs Multicast. Recovery and reliability.
  * Serialization formats. Decimal numbers.
* Modeling and pricing.
  * Generalities.
  * Microstructure.
  * Infer price from the order book. Simple BBO models. Correlations.
  * Derivatives. Futures. Options.
* Low-Latency Execution.
  * Why speed matters. Asynchronous change requests. Fairness. Determinism. Pick-offs. Achieve good priority. Time on the wire. Ethernet, IP, TCP.
  * System architecture. Soft real-time constraints. Hybrid trading systems. Low-latency networking. Threading model.
* Data analysis and research.
  * Data pipeline. Recording time series. Recording metrics. Ingesting and working with data.
  * Research platform. Quality metrics. Simulation. Network simulation. Optimization.

## [How Microsoft Uses C++ to Deliver Office - Huge Size, Small Components - Zachary Henkel - CppCon 2022](https://www.youtube.com/watch?v=0QtX-nMlz0Q)
### Topics covered:
* Background
* Huge Size:
  * How Many Lines of Code?
  * Preprocessor.
  * Alternative Measure for C++: Unique translation units, count compilations.
  * Total Office compiler invocations: 2 Million.
  * Costs of size. Workload, Static Analysis, Migration scope, Tests, Decommissioning.
  * Value of expanding size.
  * Is it valuable to have a huge codebase? It depends.
* Small Components (termed liblets).
  * 1995: Common functionality moved to shared library. `MSO.dll`.
  * 2011: Liblets to the rescue!
  * Layers.
  * Modern C++, Distinct public API, Self Contained, Clean Dependencies, Unit Tested.
  * Liblet success.
* What's next:
  * Header Units. Binany representation of a header file. Produces the same format as named modules. Recommended alternative to PCH (precompiled headers).
  * Liblets + Header Units.



