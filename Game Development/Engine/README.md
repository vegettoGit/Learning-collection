## [RE ENGINE's Past and Future - Tomofumi Ishida - CAPCOM Open Conference RE:2023](https://www.youtube.com/watch?v=ibv9319dIQA)
### Topics covered:
* RE ENGINE's Past.
  * What is RE ENGINE?
* RE ENGINE Titles.
* RE ENGINE Supported Platforms.
* Features of RE ENGINE.
  * High Performance and Stability.
  * High Development Efficiency.
  * Modular Design: Rendering, motion, etc.
  * Backwards Compatibility.
* RE ENGINE's Present.
* Improved Efficiency of Engine Management Systems.
  * Introduction and Visibility of RELauncher.
  * Ensure Engine Stability and Compatibility: Introduction of REQA, Engine Distribution Flow (Master/Release Git branches).
  * Reduction of Defect Investigation Costs: Steps to start investigating defects, Introduction of High-end PCs, Device Farm Implementation, Introduction of Cloud Saving for Development, Introduction of a Package Manager, Introducing the REProfiler.
  * Responding to Inquiries and Managing Issues: Utilizing Microsoft Teams, Title QA, Introducing TeamsView.
* RE ENGINE's Future.
  * RE ENGINE challenges (expansion and diversification of project scale, used by overseas team members, increase in new graduates with commercial engine experience).
  * Go beyond the boundaries of in-house engines.
  * REX: RE neXt ENGINE.

## [RE ENGINE Philosophy - Daisuke Sanekane - CAPCOM Open Conference RE:2023](https://www.youtube.com/watch?v=mqEMFJHUn3g)
### Topics covered:
* History of RE ENGINE.
  * Began in 2014. 
  * Prior to that, CAPCOM was using a game engine called MT FRAMEWORK.
  * In 2012, began developing Panta Rhei as a next-generation engine. It was halted and CAPCOM began building RE ENGINE using the assets of Panta Rhei.
  * RE ENGINE would be used for Resident Evil 7, so the features needed for that game were prioritized.
  * In 2015, other titles were launched and began to support multiple titles.
  * In 2017, we moved from svn to git for code version control. Adopted GitLab as our tool of choice. The tool made code reviews easier. The use of RE ENGINE started to diversify, the Osaka and Tokyo offices began to collaborate.
  * It took a long time to acquire Osaka server assets from Tokyo. The problem was solved by preparing a mirror server.
  * In 2018, started providing support for external partner companies (game development and assets outsourcing).
  * The number of titles adopted steadily increased, but the COVID pandemic began to affect engine development in early 2020. Shifted to online communication.
  * As of 2023, we support more than 20 projects simultaneously (not all of them are part of game development).
  * 20 developers in 2014, about 150 in 2023. From single floor to multiple locations.
* RE ENGINE Development Structure.
  * Each area of specialization is called a "unit": AI, CI, DCC, Editor, Effects, GUI, Motion, Network, Physics, Rendering, Runtime, Security, Sound, Timeline, Tool.
  * Each unit has a flat structure with no hierarchical relationship.
  * Management is a different type of unit. Acts as a "jack-of-all-trades" to solve any problems that may arise for engine units or game developers.
  * AI: Navigation, FSM and BehaviorTree.
  * CI: Creates and distributes engines. Automates build check systems. Develops QA tools for automatic installation of packages on each platform, for crash detection, etc. Visualizes the information obtained from these systems using the Web and tools.
  * DCC: Develops tools that run on RE ENGINE, such as SDM (Scene Data Manager, an asset management tool used by artists) and plug-ins for various types of DCC.
  * Editor: Develops a wide range of editors for graphics creation. Includes level design, background art creation and material editing.
  * Effects: Develops editors for creating effects in games and functions for various types of expressions.
  * GUI: Develops editors and functions for creating UI in games and systems for managing text in different languages.
  * Motion: Focuses on Character Animation (motion blending, posture control using IK), real-time preview of motion capture.
  * Network: Focuses on matchmaking and friend functions required for multiplayer, online functions such as ranking and network storage, HttpClient, WebSocketClient and capabilities for use in data analysis.
  * Physics: Develops systems for character hit detection and position correction, as well as simulation functions for rigid bodies and cloths.
  * Rendering: Develops rendering functions such as geometry, lighting and shading, materials and post-processing effects.
  * Runtime: Develops the core of the engine, wraps different APIs for each platform and develops tools such as profilers, script debuggers and package creation.
  * Security: Develops anti-cheating and anti-piracy systems for PC games, DLC and other content. They also develop crash reporting tools to collect and investigate information when crashes occur in user environments.
  * Sound: Develops in-house sound engines for game sounds, audio middleware and editors for sound effects.
  * Timeline: Develops key animation functions, mainly for use in cutscenes.
  * Tool: Develops the UI for RE ENGINE as a whole as well as UI parts used in the editor created by each unit. Provides a mechanism for tool development (Python based) for game developers. Develops version control systems for assets.
* Role of the Management Unit.
  * Ensure engine and game developers can develop without delays and holdups.
  * "Inbox" for queries.
  * Various clerical tasks.
  * Formation of RE ENGINE development culture.
* RE ENGINE Development Culture.
  * Open Environment: Microsoft Teams, Weekly video chat meetings, Internal website for information sharing.
  * Engine developers play a leading role, the Management Unit's role is to support their development.
  * Relationships with game developers: Quick response time and resolutions, Accumulation of technology, Support from title startup to release, Performance review (memory and performance bottlenecks), Conduct regular webinars to explain engine functions.
* RE ENGINE Development Workflow.
  * Engine developer onboarding process.
  * Receive training for engine developers. Includes code reviews for each assignment. Completed in 2 to 3 months.
  * Additional specific training for each unit.
  * Feature implementation flow. Implementing requests from game developers. Discussion, Implementation, Review, Check.
  * Runtime code is C++.
  * Tool code is C#.
  * Code reviews are done with GitLab's MergeRequest function.
  * Build checks performed with GitLab's Pipeline function.
  * "Experimental" checking engine version.
  * Automatic Check: The game is played from start to finish and checked for crashes and game progression problems.
  * Manual checks performed with the help of the QA team for non-crash problems such as visual defects.
  * RE ENGINE policy: All past titles must run on the latest engine to ensure compatibility.
  * LegacyFlag to switch between behaviors. For example, it can be on for released titles and off for titles under development.
  * CI builds are performed every day in the evening.
  * When working on a feature, the engine code is integrated into a single branch. We provide an engine for each title.
  * RE ENGINE's functionality is divided into modules. We can set which modules are used for which title.
  * Master branch vs Title branch.
* Final Thoughts.

