## [How to Simulate a Low Latency Exchange in C++ - Benjamin Catterall - C++ on Sea 2023](https://www.youtube.com/watch?v=QQrTE4YLkSE)
### Topics covered:
* The High Frequency Trading Landscape.
  * What is an exchange?
  * How do exchanges work?
  * What is a Central Order Book? Price-Time priority.
  * What generates the order requests? A trading system!
  * High Frequency Trading System.
  * What is a Trading Strategy?
  * Components of an Exchange: Matching Engine, Order Gateway, Feed Publisher.
  * Reaction time.
* Why simulate an exchange?
  * Develop profitable trading strategies, evaluate them before pushing them into production and after having run them in production.
  * Requirements.
* Simulating an exchange. We need:
  * Feed data.
  * An Order Request and Response data model.
  * A Simulation loop.
  * An Event Queue.
  * Delay Models.
  * A Matching Engine.
  * Strategies to simulate.

## [C++ Electronic Trading for Cpp Programmers - Mathias Gaunard - ACCU 2023](https://www.youtube.com/watch?v=ltT2fDqBCEo)
### Topics covered:
* C++ jobs in Trading.
  * Back-Office, Mid-office, Front-office.
* Trading in a nutshell.
  * Exchange assets for profit.
  * Matching. Continuous matching. Active vs Passive.
  * Order book: Data structures.
  * Strategy: Capture the spread, Aim for no risk. Asset Management.
* Connectivity.
  * Feeds.
  * Protocol considerations. Unicast vs Multicast. Recovery and reliability.
  * Serialization formats. Decimal numbers.
* Modeling and pricing.
  * Generalities.
  * Microstructure.
  * Infer price from the order book. Simple BBO models. Correlations.
  * Derivatives. Futures. Options.
* Low-Latency Execution.
  * Why speed matters. Asynchronous change requests. Fairness. Determinism. Pick-offs. Achieve good priority. Time on the wire. Ethernet, IP, TCP.
  * System architecture. Soft real-time constraints. Hybrid trading systems. Low-latency networking. Threading model.
* Data analysis and research.
  * Data pipeline. Recording time series. Recording metrics. Ingesting and working with data.
  * Research platform. Quality metrics. Simulation. Network simulation. Optimization.




