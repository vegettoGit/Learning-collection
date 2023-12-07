## [Simulating Tropical Weather in 'Far Cry 6' - Emily Zhou (Ubisoft Montreal) & Colin Weick (Ubisoft Toronto) - GDC 2022](https://www.youtube.com/watch?v=mGHCOOnI5aE)
### Topics include: 
* Intro to Far Cry 6.
* Inspiration.
  * Tropical Weather References.
* Core controls of the weather system.
  * Goals: Weather states, dynamic weather, natural transitions, efficient.
  * Weather Manager.
  * Weather Presets: Few Clouds, Broken Clouds, Mist, Heavy Fog, Light Rain, Moderate Rain, Heavy Rain, Thunderstorm.
  * Weather Forecast.
  * Regional weather.
  * Weather at Runtime. Weather State Flow.
* Material wetness.
  * Tech art driven.
  * Wetness Type (Static, Dynamic).
  * Static Wetness: Wetness Shadow Map. Store the wetness shadow in the deferred shadow pass. Porosity.
  * Dynamic Wetness: Wetness Component. Characters, weapons, vehicles. Perform a raycast every few frames to check if exposed to rain.
* Rendering features.
  * Atmospheric Scattering, Volumetric Clouds, Volumetric Fog, Reflections and Cubemaps, Rain and Lighting.
* Lighting.
  * Physically based.
  * Multi-scattering diffuse and specular BRDFs.
  * Translucency.
* Global Illumination.
  * Light probes.
  * GI Data: 13 packed frames.
* Sky Lighting: Atmospheric Scattering.
  * Humidy, Turbidity.
* Volumetric clouds.
  * Lighting Model Recap. Extinction, Single Scattering, Multiscattering, Phase function.
  * Generated Noise Data. Base Noise, Detail Noise, Weather Map, Curl Noise.
  * Cirrus Cloud Data.
  * Raymarching.
  * Runtime Textures. Checkerboard Rendering and Encoding.
  * Projected Cloud Shadows.
* Volumetric Fog.
  * Frustum Aligned Volume, Temporal filtering, Sum Cells, Blur Summed, Exponential Blurred Shadows.
* Reflections.
* Cubemaps: Needed fallback for when SSLR is not viable.
  * Cubemaps Relighting.
* Rain (GPU Particles).
  * GPU Particle System, GPU Particle Sorting (Bitonic Sort).
  * Particle FX: Streaks, Splashes, Lightning. 
  * Rain Shadow Map.
  * Rain Particle Lighting.
  * Ocean (iSUBD Tessellation). Wave Simulations.
* Tree Bending.
* Conclusion.

## [Static vs. Dynamic Lighting - Natalia Torres - Unreal Fest 2022](https://www.youtube.com/watch?v=gqKka4dAyJQ)
### Topics include: 
#### Tips for better Static Lightning quality:
* GPU lightmass usage.
* Viewport Realtime set to on.
* Lightmass importance volume.
* Usage of lightmass portals, etc.
#### Dynamic Global Illumination (when all lights are set to movable):
* Dynamic Lightning.
* Ray Tracing: In UE4, Real Time Ray Tracing allowed creating interactive experiences with subtle lightning effects. In UE5, Unreal has its own ray tracing code both for the offline and real time paths.
* Lumen:
  * It's the new dynamic global illumination and reflections system, set by default in UE5. 
  * It provides infinite diffuse bounces, which are merged with Nanite's geometry for achieving great detail.
  * Emissive materials propagate light through Final Gather with no additional performace cost.
  * We can see on a reflective material the full scene's reflection.
  * It relies on mesh distance fields.
#### Good Practices.

