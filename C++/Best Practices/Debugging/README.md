## [A Guide to Debugging C++ Code: Practical and Interactive Examples - Sebastian Theophil - C++ on Sea 2023](https://www.youtube.com/watch?v=Rc2hFf1HVow)
### Nobody Can Program Correctly. A Practical and Interactive Guide to Debugging C++ Code.
### Topics covered:
* What is a bug?
* First, you have to notice the bug.
  * Crash, core dump, error message, line written to a log file, an observable misbehavior.
  * At Compile Time.
  * At Build Time & QA.
  * At Run time.
* Learning from a single occurrence?
* Quiz.
* "Only sometimes reproducible".
  * Use tools that detect hard-to-reproduce issues: AddressSanitizer, ThreadSanitizer, UndefinedBehaviorSanitizer.
  * Stress tests, log files, write code to diagnose the system when the problem occurs, etc.
  * Only reproducible on some machines.
* Quiz.
* Identify the problem.
  * Gain understanding of larger system by tracing.
  * Careful: Tracing may make timing-dependent bugs dissappear.
  * Gain understanding of the OS by tracing: ProcessMonitor (Windows), dtrace (macOS), strace (Linux), etc.
  * Isolate the wrong part of your code: Find breaking change by binary searching commits, step through working/breaking versions in parallel, disable code until bug dissappears, etc.
  * Improve code to find the problem: Use asserts a lot for invariants, use temporary asserts to narrow down problems for complex checks, introduce RAII in legacy code, etc.
  * Reverse debugging tools: WinDbg, Undo (Linux), rr (Linux).
  * Get at least passive assembly skills.
  * Write debug visualizers for your data types.
* Quiz.
* Classify the bug.
  * You didn't write what you meant: Uninitialised data, memory management problem, stack corruption, data corruption, etc.
  * You wrote what you meant, but meant wrong: wrong use of internal and external API, use of OS facilities that don't work like you thought they did, you did not understand your own requirements, etc.
* Fixing bugs.
  * What should the ideal solution look like?
  * Given my constraints, what should I change now?
  * Why did the bug happen in the first place?
  * How can we prevent it from happening again?
  * Missing abstraction.
* Delivering Fix:
  * Documentation in the code and outside of the code.
  * Code reviews.
  * Good version control practices.
  * Tests.
* Debugging Process summary:
  * Bug report, Reproduction, Identify the Problem, Classify the bug, Fix the bug, Deliver the Fix.




