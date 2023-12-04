## [Inside Stormgate: Ex-StarCraft Devs Use Unreal Engine 5 For Brand New RTS](https://www.youtube.com/watch?v=54xWRLdNZIw)
### Genre: RTS.
### Topics covered:
* Game pilars: Campaign, Competitive, Cooperative and Custom Games.
* SnowPlay for gameplay, simulation.
  * Custom solution to handle high unit counts.
  * Main bottlenecks for going over 50 or 100 units are on the network side (having to replicate that much data - client server model) and having fully functional actors running on the simulation.
  * James Anhalt is the Chief Architect. He takes all the experience from Blizzard to support that many units, running all of their collisions and pathfinding. The target was 3 times the speed of Starcraft 2.
  * The objective is responsive gameplay.
  * The original Pathfinding target was to be at least as good as Starcraft 2. Refer to James Anhalt's Starcraft 2 GDC talk "Pathing". The lessons learnt are being put into Stormgate, now improving all nuances and edge cases.
  * No gameplay advantage with higher spec machines. One of the core values is Gameplay Comes First.
  * Netcode: Deterministic simulation. Being as performant as possible, optimizing from the get-go. Needs to support features like replay, observe and spectate, etc.
  * One of the Netcode techniques is rollback (traditionally used in Fighting games, one of the first implementations was Street Fighter 3). RTS simulations are more expensive that fighting games due to the unit counts.
  * One of the downsides of Rollback is the potential for visual artifacts when we resimulate. In the most common case you don't notice it at all. Examples of things to notice: A unit dies and comes back up again, a projectile briefly goes away.
  * The gameplay feels much better with Rollback.
  * Deterministic simulation challenges: Making sure all clients always stay in sync. Rollback increases the likelihood of desyncs, having to resimulate. Find and fix all desyncs during development.
  * The rollback solution is built as a `dll`. It's the first RTS game using Rollback.
  * The deterministic simulation for now is a single thread, we are targeting 64 Hz. We get a lot of performance by simulating many frames by one thread (everything being in cache and so on). Being multithreaded brings challenges for being deterministic.
* Unreal 5 for sights and sounds, the presentation: Audio, animation, UI.
  * Animation, skinning, rendering and non-deterministic physics are handled on the Unreal side.
  * Started with UE4, immediately updated to UE5. Relatively easy to update UE versions.
  * Supporting both DX11 and DX12. Currently getting better results with DX11.
  * Using Niagara for visual effects.
  * Exploring Nanite in the next couple of months.
  * Lumen assumes it's a 1st or 3rd person perspective, so it doesn't support RTSs just out of the box.
  * Supports DLSS frame generation.
  * Using Unreal's Terrain Editor. As you are painting, we dynamically generate a pathing mesh for path finding (computed close to real time as you are painting).
  * We built a Compute Shader to handle the visual side of units in proximity to trees, without needing any physics calculations.
* Minimum spec for the game looking good: Windows 10, 6 cores (1 for SnowPlay, the rest for UE5, the faster the CPU the more frames you can resimulate), 2.3 GHz for decent performance, 16 GB of RAM, GeForce GTX 1060.




