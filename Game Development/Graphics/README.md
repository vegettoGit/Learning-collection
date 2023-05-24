# [Static vs. Dynamic Lighting - Natalia Torres - Unreal Fest 2022](https://www.youtube.com/watch?v=gqKka4dAyJQ&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
## Topics include: 
### - Tips for better Static Lightning quality: GPU lightmass usage, Viewport Realtime set to on, lightmass importance volume, usage of lightmass portals, etc.
### - Dynamic Global Illumination (when all lights are set to movable)
####  . Dynamic Lightning
####  . Ray Tracing: 
####  In UE4, Real Time Ray Tracing allowed creating interactive experiences with subtle lightning effects. In UE5, Unreal has its own ray tracing code both for the offline and real time paths.
####  . Lumen: 
####   It's the new dynamic global illumination and reflections system, set by default in UE5.
####   Provides infinite diffuse bounces, which are merged with Nanite's geometry for achieving great detail.
####   Emissive materials propagate light through Final Gather with no additional performace cost.
####   We can see on a reflective material the full scene's reflection.
####   It relies on mesh distance fields.
### - Good Practices



