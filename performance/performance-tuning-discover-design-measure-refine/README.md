# Software Performance Tuning Methodology: Discover, Design, Measure & Refine

Software performance tuning is often regarded as a dark art for low level hackers. In my experiences the majority of performance tuning is much more social and systems based, opposed to low level OS wizardry. This post outlines an approach to software performance which incorporates performance into the very beginning of the software development lifecycle. This post was adapted from an internal talk.

# What is Software Performance? And Why Should We Care?
Software performance is an overloaded term and can be used to mean a number of things:
- Responsiveness (latency)
- Stability (availability)
- -ilities (scalability, extensibility, maintainability, extensibility)

Without refining the definition yet, we should care because software performance:

- **Impacts** Customer Experience
- **Informs** Scaling & Provisioning
- **Indicates** Performance Regressions (relative changes)

<p align="center">
  <img src="static/why_3_is.png">
</p>

## What's the Problem?

Performance is (unfortunately) Emergent, meaning that individual systems performance may not inform the larger systems performance when they are combined.  Even if this is not strictly 100% true, it's difficult to predict the performance of end user system when system is put together.  This has 2 important implications:

- Difficult to predict performance (Favor Observation)
- System Specific (Local Doesn’t Predict Remote)

Because of this, we often see the mantra: Make it Work then Make it Fast emerge.  This suggests that we shouldn't worry about performance until we have a working project.  While I think this is better advice than the other end of the spectrum, there is plenty of low overhead work we can do to design performance in.

## Finally! Performance is:

Defined by clients, and a proxy for their experience!  Perofrmance is the executable validation of a design.  Performance will happen either Explicitly, under our control and guidance or Implicity, hitting against unforseen user expectations or unforseen physical limitations (such as the speed of light).

# How do we ensure Code is Performant?

<p align="center">
  <img src="static/discover_design_measure_refine.png">
</p>

# Discover
What are the known or discoverable constraints?  

## Explicit Constraints
These will often be viewed from a client's perspective.  These are often contractual ie a customer is paying for a certain level of service:

- Response must be served with 100ms
- 99.99% of requests need to be < 1 second

The two most common sources for these are:

- Contractual
- Product Management

## Implicit Constraints

Implicit constraints are performance limits hidden in requirements. If a program is doing *daily* reports or *hourly* rollups, the interval of those actions may defined the expected limit. These are constraints that are often end user usability experience (UX) focused. For example if an action is blocking in the user path there is a [~100ms limit for the site to feel "responsive"](https://www.nngroup.com/articles/powers-of-10-time-scales-in-ux/).

## Physical Limitations of Systems

Physical limitations are often dictated by the minimum achievable performance in the physical world! If certain latencies are required between largely separated locations performance will run up against the speed of light!  There are other performance critical constraints based on the current speed of hardware, seen in the ["Latency Numbers Every Programmer Shold Know"](https://gist.github.com/hellerbarde/2843375) infogram:

<p align="center">
  <img src="static/latency_numbers_should_know.png">
</p>

## Reasonable Ranges

Reasonable ranges are formed based on knowledge of physical system limitations and experience of observing systems in production.  Suppose that there is a go service that accepts and HTTP connection, makes a get request to redis and then writes and closes the HTTP connection.  The service is being tested locally by running both the service and redis and driving traffic using apache benchmark.  Locally is a 2019 macbook pro  with 6 core and 16GB of ram.  On the first test the service is only able to handle 50 requests per second!  Based on experiences this is unreasonable.  This service should be able to push a couple hundred requests per second easy.

<p align="center">
  <img src="static/new_york_latency.png">
</p>

# Design

Design phase is focused on materializing the structure of a concrete implementation.  This is where discovered constraints are combined with implementation strategies.  Most of the performance work shold be done here, as this is where the solution is most maleable and has the least cost associated with changing.

## Measurement Strategy

First step is to define a measuring strategy:  

- **What** is being measured?
- **Where** is it being measured?
- **How** will it be collected?

And finally what will we use to determine if this is “performant”?  [Google's strategies for choosing good SLOs highly align with this step](https://cloud.google.com/blog/products/gcp/building-good-slos-cre-life-lessons).

## Theoretical Performance

Theoretical Design takes into account theoretical performance and runtime complexity of implementation algorithms and datastructures:

<p align="center">
  <img src="static/big_o.png">
</p>

It also includes system specific implications of performance, like implications of schema choices on database query execution.

## Isolatable Components - Testable Design

This brings us to the code level.  There are a number of techniques that reduce [friction in isolating components](https://medium.com/dm03514-tech-blog/you-are-going-to-need-it-using-interfaces-and-dependency-injection-to-future-proof-your-designs-2cf6f58db192) for inidividual benchmarks and in providing stub (highly controllable) implementations for performance testing:

- Interfaces & Swappable Implementations
- Dependency Injection
- Exercise components in isolation using test harness
- Ability bring up and exercise the service using test load

<p align="center">
  <img src="static/clean_architecture.png">
</p>

# Measurement

## Strategies

Using the mesurements defined above its time to start determining if performance has been "achieved"!  Since this methodology puts client experience as first priority if performance meets the clients expectations then no more tuning is necessary:

<p align="center">
  <img src="static/perf_measurement_strat.png">
</p>

## Execution : Generate Load

Many different ways to load a system.  Best to start with the higher level (customer representative metrics) and slowly work down into implementation details as more data becomes available.  Many different test types:

- Performance
  - Local (relative) vs Remote in a Prod-like environment (absolute)
- Soak/Endurance/Stress
- Remote Long running, verifies steady state
- Canarying
- Service Test Harness
- Micro benchmarks (such as [go Benchmark](https://golang.org/pkg/testing/#hdr-Benchmarks))

## Establish Baseline

Establishing baseline is crucial for seeing relative change in performance.  Without a baseline it's difficult to understand the impact of a change:

<p align="center">
  <img src="static/baseline.png">
</p>

## Profile
Profiling is used to determine where an application is spending its time or other resources (ie memory).  

<p align="center">
  <img src="static/perf_profile.png">
</p>

## Visualize!

Once data is captured it's important to put it in a form that can be easily understood.  A common profile visiualization technique is called Flame Graphs and was created by Brendan Gregg:

<p align="center">
  <img src="static/flame_graph.png">
</p>

A detailed description on how it can be used to understand application [performance can be found on the acmqueue article here.](https://queue.acm.org/detail.cfm?id=2927301)

([Image belongs to Brendan Gregg and was Published on acmqueue](https://queue.acm.org/detail.cfm?id=2927301))

# Refine

Refining is the hands on act of combining the previous steps to generate data, observe the performance, create hypotheses, and execute expirments.  

## Scientific Method in Action

<p align="center">
  <img src="static/Scientific_Method_3.jpg">
</p>

## Strategies

Theory of Constraints ("a chain is no stronger than its weakest link") is a common tuning strategy.  It focuses on finding the largest bottleneck, or contributor to latency, to achieve desired performance.  It identifies the bottleneck, removes the bottleneck, and then remeasures to identify the next bottleneck.  In performance tuning there will always be a slowest operation.  Because of this performance tuning provides diminishing returns.  At some point it doesn't make economic sense to continue increasing performance.  

## Anti-Patterns

Performance Engineering has a number of insidious anti-patterns:

- Identifying bottlenekcs based on Intuition vs Facts 
  - Solution is to let reality (fact-based evidence) be the guide
- Using Local Performance to predict global
  - Performance is emergent so the best local performance can tell is a relative performance increase/decrease based on previous local baselines 
- Tuning without overarching client centric measurements
  - Choose a client representative performance metric in order to understand the impact of performance tuning on the client's experience.
- Choosing low impact candidates
  - If an operation is responsible for 5% of latency and can take 4 weeks to halve and another bottleneck is responsible for 10% of latency and takes 4 weeks to halve it should be intuitive to attack the 10% latency operation.  This can be addressed by using fact based evidence combined with a methodology like Theory of Constraints.
- Not collecting data because it's too difficult, low level, app wasn't designed properly etc.
  - There's ways to measure pretty much everything (BPF) now!

<p align="center">
  <img src="static/antipattern.png">
</p>

([antipattern image property of Martin Fowler](https://martinfowler.com/bliki/AntiPattern.html))

# Conclusion

- Performance is as much Design as it is Execution
- Performance is social 
- Performance is continuous 
- Performance is about uncovering what the program is actually doing by observing where it spends its time
- Performance is application of Scientific Method

Happy Performance Tuning!
