## Graph Based Alerts

Graph-based Alerts should allow for all alerts to be connected to any other alert providing more context
around alerts, related alerts, and potential future alerts.  Modeling alerts as a graph should allow operators
to apply policies to manage alert suppression, or to provide context around downstream systems that may be affected
by cascading failures.

### Problem

When responding to alerts, it can be difficult to understand which services are affected by an alert.  Many alert systems 
lack a concept of related alerts.  Each alert is isolated, and relies on naming, or tagging to achieve some semblance
of dependency between alerts.  Simple server health check alerts in a system like nagios don't show the services running
on those boxes, by default.  There is also a difficulty in associating services with alerts.  This is often accomplished
with naming conventions, making establish service to service depdendencies difficult.

### Solution

Modeling alerts as a graph allows for codification of explicit relationships allowing for:

- Suppression of nth degree downstream alerts
- Inform: Dynamic dashboard generation based on downstream alerts
- Inform: Hooks services can be nodes in the alert graph allowing for greater context around alerts

### Use Cases

- As an operator, I'd like to take down a service and suppress alerts for all 1st degree services, while the service is in maintanence mode
- As an operator, when an alert fires, I'd like to have dashboards automatically created with metrics of all second degree alerts

### Implementation (POC)

In a graph based alerting system each alert or resource is a node, and all nodes can be connected to any other node.
Thinking of a system that sits on top of most common alerting systems, which stores the graph, and has "providers" for
handling concrete implementations. The operator would have to manually create the graph.  There will be "policies" available 
("supress", "inform", etc...) to target nodes based on tags, n degree connections.  The underlying reporting system
must be able to provide some sort of api for the graph system to interact with programatically.

### Caveats (POC)

- Graph is manually created/maintained manually (how can we leverage automation?)

