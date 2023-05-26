# [Unreal Engine Game Optimization on a Budget - Tom Looman - JetBrains GameDev Day Online 2022](https://www.youtube.com/watch?v=G51QWcitCII&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
## Topics include: 
### - Built-in Profiling Tools and Commands:
Unreal Insights: Provides detailed insights into the frame timings: CPU/GPU, Memory, File Loading and Threading. Bookmarks are used for context and transitions (example: level streaming start/complete). <br><br>
Memreport: Runs a number of commands for memory profiling. How much memory is certain category (example: objects of type Animation Sequence) using? Is any object larger than expected? Use it on Package games as opposed to the Editor. <br><br>
DUMPTICKS: Output all Actor and Component Ticks. <br><br>
RENDERDOC: Shows up Occlusion results. It allows us to easily find wasteful queries on tiny/far objects. <br><br>
FreezeRendering: Fly with DebugCamera. Verify Occlusion is working as expected. <br><br>
Use the Animation Compression Library (ACL). <br><br>
Oodle Data & Oodle Texture: Rate Distortion Optimization (RDO) Compression. <br><br>
SYNTHBENCHMARK: Run CPU/GPU benchmark and apply Scalability Settings. <br><br>
SizeMap: Find unexpected references and bloated content. <br><br>
Others: Profile GPU, stat unitgraph, stat detailed. <br>
### - Easy optimization opportunities:
"Collision Enabled" (Physics + Query) might be set to on by default, when we just need a Query (example: unreachable objects or objects we cannot interact with). <br>
Oclussion Culling: HLOD can greatly reduce occlusion cost. <br>
Distance Culling: Set a Max/Min Draw Distance on PrimitiveComponent. Distance Cull Volume maps "Size" with "CullDistance". <br>
Level Streaming: Using Streaming Volumes vs Manual Load/Unload. It can be Camera Location based. Use "Loadtimes.dumpreport" to show how long specific assets took to load. It reduces the initial level load time. <br>
Animation Fast Path: Move Computations out of AnimGraph into EventGraph. Update Rate Optimization (URO) for distant SkelMeshes. <br> 
Shadow Proxies: Single low-poly silhouette mesh (RenderMainPass=False), Bespoke mesh or using built-in Mesh Tools (Merge Actors). <br> 
### - Significance Manager:
Scale down fidelity based on game specific logic (example: distance to). It scales down based on the "significant value". It reduces / culls tick rates, queries, animation updates, audio / particles update rate, etc. <br>

# [Maximizing Your Game's Performance in Unreal Engine - Ari Arnbjörnsson - Unreal Fest 2022](https://www.youtube.com/watch?v=GuIav71867E&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)
## Topics include: 
### - Profiling in general:
Frame budget, When do I optimize and Practical Optimization.
### - Profiling in Unreal Engine:
Unreal Insights and ProfileGPU.
### - Practical examples:
Low Editor Framerate, Tiny Actor and Huge Hitch, Foggy Horror and Memory Leak.

# [One Frame in 'Halo Infinite' - Daniele Giannetti - GDC 2022](https://www.youtube.com/watch?v=IUiNUky-ibM&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

# [Game Server Performance on Tom Clancy's The Division 2 - David Lind - GDC 2020](https://www.youtube.com/watch?v=bcXxyKqgV0c&list=LL6MKUgGZ9Q8c2Ff7GnoRoqA)

