## [Performant Reflective Beauty: Hybrid Raytracing with Far Cry 6 - Stephanie Brenham (Ubisoft Toronto) & Ihor Szlachtycz (AMD) - GDC 2022](https://www.youtube.com/watch?v=nTZpKD600eQ)
### Topics include: 
* Reflections in Far Cry 6.
  * Generate Ray Buffer.
  * SSLR (Screen Space Local Reflections).
  * HW Ray Trace & Lighting.
  * Particles HW Ray Trace. Particles are a special case.
  * Integrate Results.
* Importance Sampling / Generate Rays.
  * GGX BRDF to obtain reflection lobe.
  * Importance sampling reduction.
  * Pre-generated Hammersley sequence.
  * Store rays in buffer for later use.
  * Reuse Neighbours, we want one ray texel per frame.
  * Shrink Hemisphere, Store in half resolution ray buffer.
* SSLR.
  * SS trace is faster than HW ray tracing.
  * SSLR is a fallback while BVH (Bounding Volume Hierarchy) builds.
  * Replaced Hierarchical Z with Linear Trace, but edges were some times missed.
  * Added Random Ray start offsets, resulting with edges becoming more stable.
  * Smooth surfaces like chrome need higher precision.
  * Cone angle varies by roughness.
* HW Ray Trace & Lighting.
  * Acceleration Structures (AS), Traversing the BVH, TLAS and BLAS.
  * Far distances: Only SSLR, Close distances: Only HW RT.
  * RayTrace Reflection Graph.
  * BVH Tree.
  * Lighting shader and ray trace shader in one.
  * Primitive Pool: Primitive Buffer, Primitive Offset Buffer.
* Particles HW Ray Trace.
  * Reuse ray length from SSLR / HW RT.
  * BLAS instance per particle.
  * Build separate TLAS for particles.
  * Extra Quads, masked by view space axis direction in BVH.
* Integration.
  * Reuse neighbors' color results to integrate rays from multiple directions.
  * Reflection Motion.
  * Temporal Accumulation.
* Optimizing Ray Tracing in Far Cry 6.
  * Radeon GPU Profiler (RGP).
  * Shader table management.
  * Hit shader design.
  * BVH building.

## [Lightning Talk: Ray Tracing on the GPU - Stephanie Brenham - ACCU 2023](https://www.youtube.com/watch?v=3SbtXzSa9DQ)
### Topics include: 
* We have light from a light source, it bounces around.
* We trace things as they are going backwards, and collecting information.
* Processing on the GPU vs Processing on the CPU.
  * CPU: Out of order execution, branch brediction, caching.
  * GPU: Lockstep.

