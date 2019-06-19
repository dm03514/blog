# SRE: Strategy: Deploying SLOs Across An Organization

Google SRE book gave us theory behind SLOs but fall short in understanding why and having a a plan for how.  This post outlines a strategy for deploying SLO's across an organization based on the one successful.  It outlines the principles/constraints around the osolution and then proposses a solution that respects those constraints.  This posts outlines a technincal strategy that allows every team to incorporates SLO's into their specific services and beging makingn decisions based on those SLO's. 

## What is An SLO?
This post largely assumes that the reader is already familiar with SLO's as defined by google (LINK).  SLO's establish a link behind a service prodier (engineers) and a client, and makes that link visibile.  This linkn creates a feedback loop which allows a service provider to understand their clients experiennce annd take action on that. It is also necessary to understand that an SLO PROxies a client experiencinng, by choosing signals that provide high fidelity for what a client is experiencing.

<p align="center">
  <img src="static/service_provider_vs_consumer.png">
</p>
SHOW LINK

SHOW NO-FEEDBAKC VS FEEDBACK

## Principles
- Proxy client experience
- Actionable (Alerts, Data informed decisions)
- Minimal investment (low technical overhead) Minimal moving parts
- Low false positive rate - Low flakiness For adoption the breadth of testingn is nont as important as minimizing overhead

### Represent the client experience

This principle favors a solution that generates the client data closest to the client.The closer to the client experience that the SLO data is generated.  Ideally there would be perfect visiability into all clients. Most of the time this is not possible because clients can be outside the organization, or custom.  

Client -> DNS -> LB -> Service

Since SLO is focused on client its favorable to have metrics originating.  This means that measure at the client request level is preferable to the LB or the service level.  Some SLO's will NEED to be measured aat these levels (and each of these will surface critical metrics), but the rollout will favor metrics closer to the client.

### Actionable

In order for SLO's to succeed they need to be actionable.  This can be thought of as "alertable".  Teams need to be alerted when their client experiences are degraded, and should be woken up when the client experieince is fully inhibited.  This is basically a chat and alert integration with some basic threshold and arithmetic alerting support.

### Minimal Investment / Low Techncinal Overhead

This should be called about because teams may have a wide variety of operation experience, experience instrumnenting observing and respondningn to their services.  Additionally, implemenntation should be able to change fluidly under the chosen strategy.  A team using ELB vs ALB, or one Middleware vs another middlware HTTP framework, should have a uniform alerting, monitoringn and operational SLO experience.

### Low false positive
This is critically importantn for the initial rollout.  Just the concept of SLO and alertinng, and infrastructure monintoring may be new to teams.  A Low false positive for SLO metric collection is required in order to facilitate adoption andn to increase faith in SLOs.  The signal that is chosen should be a high fidelity representation nof the clietn experiennce.  If the signal is in the red, it should mean there is a serious issue with the client's experience.


## Proposal

Availability using black box probes fulfuills the constraints above.  Availability is if a service is reachable or not.  It can easily be executed as an indnividual client (on the public internet through a service like pingdom) or on an internal network (for the case of itnernal clients).

Is the service reachable from a client? It is a precursor to all other monitoring and Service levels.  By using such a primitive it optimizes ease of opeorationn minimizes flakinnness, and enables teams to start leaning on signals representingn their client's experience, collecting, measuring and responding.

Availability probes provide a strong signal for correlationn of failures during incidents. Being able to quickly undnerstannd if if a failure is at the network/application level is a huge insight.  This signal supports triangulating an experience with a known experieince (the prober).

This enables teams to understand what proactive monitoring is, and enables them to begin to catch issues before clients. 


## References
- https://landing.google.com/sre/workbook/chapters/alerting-on-slos/
- https://medium.com/dm03514-tech-blog/sre-availability-probing-101-using-googles-cloudprober-8c191173923c
- https://landing.google.com/sre/sre-book/chapters/service-level-objectives/
- https://medium.com/dm03514-tech-blog/sre-debugging-strategies-triangulation-efc5f796205c
- https://lethain.com/strategies-visions/
