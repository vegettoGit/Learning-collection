# [Networking Challenges in Gaming - Philip Orwig & Malachi Middlebrook - Networking @Scale 2018](https://www.facebook.com/atscaleevents/videos/networking-scale-2018-networking-challenges-in-gaming/2090071161265977/)
## Topics covered:
* A high level overview of various Replication models such as Deterministic lockstep, Snapshot interpolation, Incremental State Changes, etc.
* Usage of unreliable datagrams (UDP).
* Artificial adaptive interpolation delay.
* Adaptive bandwidth.
* Client prediction.
* Server rewinding for hit detection.
* Data centers connectivity.

# [Networking Scripted Weapons and Abilities in 'Overwatch' - Dan Reed - GDC 2017](https://www.gdcvault.com/play/1024041/Networking-Scripted-Weapons-and-Abilities)
## Includes topics such as script behavior prediction and replication, networked gameplay responsiveness, security, bandwidth usage and seamlessness.

# [Developer Update | High Bandwidth Update | Overwatch - Tim Ford & Philip Orwig](https://www.youtube.com/watch?v=EqtNUFxgm38&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
## Brief description on Overwatch's adaptive bandwidth management for a better player experience.
* Players receive data from the server more often when in the High Bandwidth mode.
* Players send input data to the server more often when in the High Bandwidth mode.
* The interpolation delay can be decreased when in the High Bandwidth mode.
* The client prediction is closer to what the Server authority sees (example: shooting results) when in the High Bandwidth mode.
* Players who don't meet certain bandwidth requirements won't be under the High Bandwidth mode.

# [Let's Talk Netcode | Overwatch -  Tim Ford & Philip Orwig - 2016 Developer Update](https://www.youtube.com/watch?v=vTH2ZPgYujQ&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
## Covers some of the Multiplayer core values of Overwatch: Favoring the shooter, responsiveness, server authority and so on.

# [I Shot You First: Networking the Gameplay of Halo: Reach - David Aldridge - GDC 2011](https://www.youtube.com/watch?v=h47zZrqjgLc&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
## The talk is about Halo Reach's multiplayer competitive experience. It goes through basic concepts (replication, prediction, authority), the architecture for scalable gameplay networking in PvP (Network stack; protocols such as State data, Events and Control data; Prioritization, Relevance, Update period); measuring and optimizing networking (Tooling: Profilers to measure bandwidth and prioritization, Playback of gameplay sessions and  Playtests simulating adverse network conditions; Bandwidth optimizations); and designing solid networking for game mechanics (4 rules of gameplay networking; examples: throwing grenades, armor lock, assassination).
### Other notes: 
### It's a P2P network model. The game doesn't use dedicated servers.
### Halo's Campaign and Firefight networking model is different to that of this talk's PvP mode. It is based in Deterministic Lockstep.