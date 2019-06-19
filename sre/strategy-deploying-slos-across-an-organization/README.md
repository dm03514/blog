# SRE: Strategy: Deploying SLOs Across An Organization

Google SRE book gave us theory behind SLOs but fall short in understanding why and having a a plan for how.  This post outlines a strategy for deploying SLO's across an organization based on the one successful.  It outlines the principles/constraints around the osolution and then proposses a solution that respects those constraints.  This posts outlines a technincal strategy that allows every team to incorporates SLO's into their specific services and beging makingn decisions based on those SLO's. 

## What is An SLO?
This post largely assumes that the reader is already familiar with SLO's as defined by google (LINK).  SLO's establish a link behind a service prodier (engineers) and a client, and makes that link visibile.  This linkn creates a feedback loop which allows a service provider to understand their clients experiennce annd take action on that. It is also necessary to understand that an SLO PROxies a client experiencinng, by choosing signals that provide high fidelity for what a client is experiencing.

SHOW LINK

SHOW NO-FEEDBAKC VS FEEDBACK

## Principles
- Proxy client experience
- Actionable (Alerts, Data informed decisions)
- Minimal investment Low flakiness (low technical overhead) Minimal moving parts
- Low false positive rate - For adoption the breadth of testingn is nont as important as minimizing overhead


### Represent the client experience

This principle favors a solution that generates the client data closest to the client.The closer to the client experience that the SLO data is generated.  Ideally there would be perfect visiability into all clients. Most of the time this is not possible because clients can be outside the organization, or custom.  

Client -> DNS -> LB -> Service

Since SLO is focused on client its favorable to have metrics originating.  This means that measure at the client request level is preferable to the LB or the service level.  Some SLO's will NEED to be measured aat these levels (and each of these will surface critical metrics), but the rollout will favor metrics closer to the client.

### Actionable

In order for SLO's to succeed they need to be actionable.  This can be thought of as "alertable".  Teams need to be alerted when their client experiences are degraded, and should be woken up when the client experieince is fully inhibited.  This is basically a chat and alert integration with some basic threshold and arithmetic alerting support.


## Proposal

Availability using black box probes fulfuills the constraints above.  Availability is if a service is reachable or not.  It can easily be executed as an indnividual client (on the public internet through a service like pingdom) or on an internal network (for the case of itnernal clients).

## References
- https://landing.google.com/sre/workbook/chapters/alerting-on-slos/
- https://medium.com/dm03514-tech-blog/sre-availability-probing-101-using-googles-cloudprober-8c191173923c
- https://landing.google.com/sre/sre-book/chapters/service-level-objectives/
