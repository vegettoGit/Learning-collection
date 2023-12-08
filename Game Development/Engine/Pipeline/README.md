# [Fast Iteration for Far Cry 4 - Optimizing Key Parts of the Dunia Pipeline - Remi Quenin - GDC 2015](https://www.youtube.com/watch?v=AhmlFG1u1wE)
## Topics include:
* Description of Far Cry 3's engine (Dunia) pipeline.
  * Compressing art assets into a binary package, etc.
* FC4's Compiling time Optimization.
  * FASTBuild adds Parallelization.
  * Caching.
  * Blobbing.
  * Distribution.
* FC4's Nightly Builds Optimization.
  * Remote Profiling of multiple processes.
  * Analyzing their interactions.
  * Resource Caching, populated by build machines, used by the Editor's JIT compilation. 
* FC4's Package Synchronization Optimization.
  * RTPAL Tool which slices Big Files into parts and just distributes what has changed.
  * Asset Store using Red Hat's Gluster File System in a cluster of PCs and supporting Replication.
* FC4's Local Change Testing Optimization.
  * DevPatcher which detects changes and patches BigFiles. 


