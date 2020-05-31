# SRE: Alerting on SLOs

Alerting on SLOs is an SRE practice which enables teams to quantify and alert on their client's experiences. When an SLO alert fires teams can be confident that a client is impacted. Alternative alerting techniques have difficulty quantifying customer impact, which can complicate incident response. This post describes SLO alerts and the benefits they provide over alternatives. The Google SRE book describes *how* to alert on SLO's, and this post aims to describe *why* to alert on SLOs.

# Terminology Refresher

SLOs are a quantifiable target representing a client's experience. SLOs are built on SLIs, and SLIs are ratios. The numerator counts "successful" events and the denominator are total events. There are two common types of SLIS:

- Availability
- Latency

Availability is commonly calculated as successful operations over total operations. Consider an HTTP based service. Availability is calculated by the number of successful (non-5xx requests) over the total number of requests. In prometheus this could look like:

```
sum(rate(http_requests_total{status!~"5.."})) 
/ 
sum(rate(http_requests_total{}))
```

Latency based SLIs are calculated using the total number of operations occurring within a latency threshold over the total number of requests. Consider a web service aims to complete requests in <= 100ms. The latency based SLI calculates what percentage of requests complete in <= 100ms. In Prometheus this looks like:

```
sum(rate(http_request_duration_seconds_bucket{le="0.1"}))
/
sum(rate(http_request_duration_seconds_count))
```

All SLIs produce a measurements between 0 and 100 inclusive. 

An SLO is a *target* which is built on an SLI. In the availability example of the SLO may be:

`99% of requests should result in successful response`

Identifying and defining SLIs is difficult and takes practice. Google published many resources including their Site Reliability engineering books, and an online course -- Art of SLOs to teach strategies for identifying and modeling SLIs.

**SLO Alerts**

SLO alerts constantly monitors a target service level and triggers an alert when that service level is not met. Google provides in depth implementation details in their [SRE Workbook](https://landing.google.com/sre/workbook/chapters/alerting-on-slos/). SLO alerts are built on the concept of an error budget. Consider a service with a 99% availability target. This means that the service can tolerate an error rate of 1%. SLO alerts project that error rate over a time frame. At the beginning of the period the full 1% of errors are tolerable, but as errors occur the error budget becomes depleted. With 0.5% errors, only have the budget remains, when the budget becomes exhausted the service is no longer able to meet its target level. Each SLO alert strategy described by Google builds on foundation of an error budget.

# Why? - Client Experience

Good SLIs represent client experience. This means that SLO alerts are able to monitor client experience in real time. When an SLO alert triggers, there is a high level of confidence that clients are being affected. SLO alerts are a subset of [symptom based alerts](https://www.datadoghq.com/blog/monitoring-101-alerting/#page-on-symptoms). Symptom based alerts focus on the *behavior* of systems and not the causes. Alerting on high resource usage or low disk space are two common examples of cause based alerts. When cause-based alerts trigger there's little context into the effects, they provide no context to help answer -- Are client's affected? The first step in responding to cause based alerts is investigation, instead of remediation. The responder has to research and understand the affect of the resource. The first step in responding to an SLO alert is remediation. SLO alerts **remove ambiguity** from the incident response process. 

## Objective Quantities

SLO alerts quantify impact to clients: when an SLO-alert fires the responder *knows* that a client is impacted. Not only do SLO alerts indicate that client's are affected, they also indicate how many requests are affected. Consider an operation with a 99% availability SLO. If an alert triggers and the current performance is 98% it's know that 2% of requests (2 / 100) are failing. Alerting on objective measurements quantifies the impact of incidents. A 50% failure rate may warrant a different response than a 0.1% error rate. SLO alerts provide a gradient of performance instead of a binary Yes|no, alerting|not-alerting feedback. Another common type of alert is a threshold alert. The threshold represents a "do-not-cross" line. An alert triggers when the threshold is breeched. Threshold based alerts can be setup to trigger on symptoms, but provide little insight into the degree to which clients are affected. SLO alerts help quantify an incident.

## Call to Action

When an SLO alert triggers a responder knows that clients are being affected and the degree to which clients are affected. SLO alerts are highly actionable. They tell the responder clients **are** being affected and then quantify the impact of the effect in terms of number of requests. Since SLOs represent a level of service, an alert represents that level of service is not being met. The alert triggers a call to action: an error budget is exhausted, a certain level of service was committed to, and it needs to be addressed immediately, without any ambiguity nor investigation.

## Generic Tooling

SLO alerts benefit from generic tooling. Since SLOs are ratios ad generate values between 0 and 100 it's easy to build tooling around these. A user can specify a numerator metric a denominator metric and a target level of service and then automatically generate alerts based on one of Google's SLO alert strategies. Tooling removes moving parts and one off alerting solutions and strategies. Instead of one team using threshold based alerts and another using a different strategy, the alert logic can be codified in the tooling. Google also [outlines a way to bucket alert levels](https://landing.google.com/sre/workbook/chapters/alerting-on-slos/#alerting_at_scale) which provides a default alerting strategy. Using the bucketed approach services can set a tag representing a bucket of service such as `CRITICAL` or `LOW` and it will automatically be monitored and alerted on. This is possible through generic tooling and expressing each SLO as a ratio.

# Conclusion

SLO alerts enable teams to monitor their commitments to their customers. When an SLO alert triggers responders know that clients are being affected and can quantify the impact. SLO alerts are not trivial to implement but are great candidates for automation. This means they can be implemented a single time and then reused without reimplementing the alerts each time.

## Resources:

- https://www.datadoghq.com/blog/monitoring-101-alerting/#page-on-symptoms
- https://landing.google.com/sre/workbook/chapters/alerting-on-slos/
- https://engineering.bitnami.com/articles/implementing-slos-using-prometheus.html
- https://medium.com/dm03514-tech-blog/sre-strategy-deploying-slos-across-an-organization-59906c0d8f5
- https://medium.com/dm03514-tech-blog/sre-debugging-getting-to-impact-through-slos-dd369ccf1f75
- https://www.circonus.com/2018/08/latency-slos-done-right/
- https://landing.google.com/sre/resources/practicesandprocesses/art-of-slos/
- https://www.usenix.org/system/files/nsdi20spring_hauer_prepub.pdf