# Distributed Tracing: Impact to Organizational System

[Distributed Tracing](https://opentracing.io/docs/overview/what-is-tracing/) traces actions as they travel throughout a system and across multiple subsystems. Distributed tracing provides high cardinality metrics which allow for performance tuning and failure analysis.  Due to its ability to dynamically generate real time data, Distributed Tracing has a profound impact on a software organization.  This impact comes from the democratization of information and provides real time, living documentation, architectural knowledge, provides an information layer that removes silos from teams, and provides detailed experience of clients.  Clients.  People, Process, Client.

This post will look at a general engineers journey as they are onboarding, developing and operating a service and how Distributed Tracing positively affects each of these stages.  This post assumes familiarity with distributed tracing (opentracing) data model.

Each of the following benefits are derived from distributed tracing being able to dynamically capture high cardinality metrics which include:
- Service communication
- Library versions
- and compares to even the best documentation becoming outdated.

Distributed tracing democratizes information by providing "living" centralized documentation.


## On boarding
Largest benefit from DYNAMICALLY generated real time view of the system.  Source of truth is the source code, tracing provides a concrete


<p align="center">
  <img src="static/documentation_vs_tracing.png">
</p>



### Documentation
Engineer on boarding often involves learning one more more services in depth.  This involves learning where services sit in relation to each other and  understanding specific service transactions.  Hopefully there is some documentation available for the service topology. The largest issues with on boarding is gaining a mental model of the system, transactions and dependencies. Because its manual relatively time consuming to constantly keep architecture up to date documentation is usually out of date (if there is any documentation at all).

Static Documentation  is dead documentation

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
  <img src="static/trace_topology_view-1.png">
</p>

The image above is from [Trace by RisingStack](https://trace.risingstack.com/) but all the major tracing platforms offer this functionality.  It's essentially free information that is critical for on boarding.

### Transactions
Another key part of engineer on boarding are key transactions and flows involved. This involves understanding entry points, protocols, collaborators, upstream services:

All of this information is available dynamically in a centralized place using tracing:

<p align="center">
  <img src="static/trace_view.png">
</p>

Without this information getting this info would require tribal knowledge, understanding, or potentially searching repos for where & when dependencies are called within the context of a transaction.

The *worst* case (Which i found to be the *normal* case) is to find this information out from the source of truth, by grepping the code.

## Developing
Largest benefits are around centralizing information.


<p align="center">
  <img src="static/centralized_vs_disparate.png">
</p>

IMAGE SHOWS A CENTRALIZED Store
SHOWS A DISPARATE STORE

### Mental Models

<p align="center">
  <img src="static/software_mental_model_vs_tracing_system_view.png">
</p>

### System/Client Directory
If you're updating a client dependency and want to see all the clients of that how do you do it? Grep Github? hope and pray? backwards compatibility?

Which service are clients of a given service? which versions are those services on of the client library?

db.type=redis
span.kind=client

## Operating
Largest benefit around CONTEXT :-> centralization and data modeled


Feedback loops exist at the team level (tribal knowledge) and software level (source of truth)

Incidents may involved many engineers from many teams just to establish a base understanding of what's going on.

Contrast this with tracing which has a cross service and cross team representation of the system.  Any team is able to quickly gain a base context on all services without having to coordinate across teams.  Able to rely on Distributed tracing as a system representation instead of engineers mental models or rooting through the source code.  IF the chart on the left looks complicated, it's because it is.  Think of the last time you were involved in a cross team incident.  Multiple service dashboards, multiple engineers from different services, everyone working together to develop a cross service view of the system and get context around the issue.  Distributed tracing provides a base view of the system that can drastically shorten these feedback loops and number of people involved incidents.  Tracing provides much more context, allowing an oncall responder to better understand the system and get farther on their own before involving more people.

SILOED TEAMS FOCUSED ON THEIR services
LONG FEEDBACK LOOPS CROSS TEAMS INVOLVED IN Debugging

<p align="center">
  <img src="static/siloed_teams_vs_distributed_tracing.png">
</p>


TRACING provides


- On call
- Debugging (Default Hypothesis, Correlations)

<p align="center">
  <img src="static/c5474b8-corr_overview.png">
</p>


While this is still in its infancy Having operational data centralized this data opens up possibilities for anomaly detection, correlation, and other advanced automated analysis techniques to shorten debugging.  While anomaly detection techniques have been offered by monitoring like DD and New relic they are often focused on single dimension time series. Having centralized store to store all operational data provides access to much more context and significantly increases the impact of anomaly detection .


## Conclusion
Because distributed provides up to date, dynamic "living documentation" which democratizes information within an organization. This provides significant benefits in terms of on boarding documentation, centralized information about a system, and context.  Furthermore modeling systems as graphs allow for accurately modeling system structures.


## References

- https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941
- https://docs.lightstep.com/docs/correlations
- https://engineering.salesforce.com/anomaly-detection-in-zipkin-trace-data-87c8a2ded8a1
