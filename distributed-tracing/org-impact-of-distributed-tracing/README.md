Distributed Tracing: Impact to Organizational System

[Distributed Tracing](https://opentracing.io/docs/overview/what-is-tracing/) traces actions as they travel throughout a system and across multiple subsystems. Distributed tracing provides high cardinality metrics which allow for performance tuning and failure analysis.  Due to its ability to dynamically generate real time data, Distributed Tracing has a profound impact on a software organization.  This impact comes from the democratization of information and provides real time, living documentation, architectural knowledge, provides an information layer that removes silos from teams, and provides detailed experience of clients.  Clients.  People, Process, Client.

This post will look at a general engineers journey as they are onboarding, developing and operating a service and how Distributed Tracing positively affects each of these stages.  This post assumes familiarity with distributed tracing (opentracing) data model.

Each of the following benefits are derived from distributed tracing being able to dynamically capture high cardinality metrics which include:
- Service communication
- Library versions
- and compares to even the best documentation becoming outdated.

Distributed tracing democratizes information by providing "living" centralized documentation.


## On boarding
Largest beneift from DYNAMICLY generated real time view of the system.


### Documentation
Engineer on boarding often involves learning one more more services in depth.  This involves learning where services sit in relation to each other and  understanding specific service transactions.  Hopefully there is some documentation available for the service topology. The largest issues with on boarding is gaining a mental model of the system, transactions and dependencies. Because its manual relatively time consuming to constantly keep architecture up to date documentation is usually out of date (if there is any documentation at all). Static Documentation  is dead documentation

DOCUMENTATION GRAPH
NO FEEDBACK LOOP
OUT OF DATE
DOESNN"T REFLECT REALITY
Separate from systems requiring frequent updates, updates aren't enforceable
MISSING FEEDBACK LOOP

### Topology
Dynamically generated based on service name.

Since distributed tracing stores information as a graph (DAG) it becomes trivial to build a dynamic up to date service topology:

<p align="center">
  <img src="static/https://blog-assets.risingstack.com/2015/07/trace_topology_view-1.png">
</p>

The image above is from [Trace by RisingStack](https://trace.risingstack.com/) but all the major tracing platforms offer this functionality.  It's essentially free information that is critical for on boarding.

### Transactions
Another key part of engineer on boarding are key transactions and flows involved.

## Developing
Largest benefits are around centralizing information.

IMAGE SHOWS A CENTRALIZED Store
SHOWS A DISPARATE STORE



### System/Client Directory
if you're updating a client dependency and want to see all the clients of that how do you do it? Grep Github? hope and pray? backwards compatibility?

db.type=redis
span.kind=client

## Operating
Largest benefit around CONTEXT :-> centralization and data modeled

SILOED TEAMS FOCUSAED ON THEIR services
LONG FEEDBACK LOOPS CROSS TEAMS INVOLVED IN Debugging

TRACING provides

- On call
- Debugging (Default Hypothesis, Correlations)
