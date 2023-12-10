## [Integer Type Selection in C++: in Safe, Secure and Correct Code - Robert Seacord - CppNow 2023](https://www.youtube.com/watch?v=82jVpEmAEV4)
### Topics covered:
* Use strong typedefs.
* Integers basics.
  * Signed and Unsigned Types.
  * Signed Integers.
  * Representing Negative Values (Two's Complement).
  * Unsigned Integers.
  * Overflow and Wraparound.
  * Signed/Unsigned Optimizations.
  * Signed Operations.
  * Unsigned Operations.
  * `size_t`. Use Cases.
  * `make_signed`, `make_unsigned`.
  * `ssize_t`.
* Signedness.
  * Use case: Loop Limited by Lower Bound.
  * Using a Signed Integer.
  * Conversion to Signed Integer.
  * Unsigned Integer with Wraparound.
  * `do`-`while` loop.
  * Unsigned Integer Problems.
  * Problem Areas.
  * Misconception: Signed Integers are Faster: 64-bit Architecture Code Example, Reality.
  * Misconception: Google C++ Style Guide.
  * UndefinedBehaviorSanitizer (UBSan).
  * Lesson.
  * Operators That Wraparound (division and remainder cannot).
  * Operators That Can Overflow (division and remainder can).
  * Integer Division, Remainder.
  * Lesson: Easier and Faster to check for unsigned wraparound than signed overflow.
  * Signed vs. Unsigned Summary.
* Exact width types.

