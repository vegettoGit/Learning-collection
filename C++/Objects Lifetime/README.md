## [Back to Basics: RAII in C++ - Andre Kostur - CppCon 2022](https://www.youtube.com/watch?v=Rfu06XAhx90&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
### Topics covered:
* What is a "Resource".
  * Memory (new, delete), POSIX File (fopen, fclose), Joinable threads (pthread_create, pthread_join), Mutex locking (pthread_mutex_lock, pthread_mutex_unlock).
* What issues do we have handling Resources.
  * Leak, Use-after-disposal, Double-disposal.
* RAII to manage resources.
  * Resource Acquisition is Initialization.
  * Take advantage of Object Lifetimes in C++ (constructor, destructor).
  * Ownership.
  * Reclaim Responsibility.
* Examples in the Standard.
  * std::lock_guard.
  * std::unique_lock.
  * std::jthread.
  * std::fstream.
  * std::unique_ptr.
  * std::shared_ptr.
* Implementing a RAII class.

## [C++ Weekly - Ep 351 - Your 5 Step Plan For Deeper C++ Knowledge](https://www.youtube.com/watch?v=287_oG4CNMc&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

## [Leak-Freedom in C++... By Default - Herb Sutter - CppCon 2016](https://www.youtube.com/watch?v=JfmTagWcqoE&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)



