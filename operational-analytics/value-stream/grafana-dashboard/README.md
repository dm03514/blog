# ValueStream: DevOps OpenCensus Metrics & Grafana Dashboard! 

ValueStream now supports exporting metrics to Prometheus as well as Jaeger/ElasticSearch!  ValueStream provides DevOps and Software Engineering metrics in a free easy to operate service and we're excited to announce support for Prometheus through [OpenCensus](https://opencensus.io/exporters/supported-exporters/go/).  We're also shipping a grafana dashboard to allow teams to begin to consume these critical metrics and get a pulse on organizational deployment performance.

<p align="center">
  <img src="static/grafana_dashboard_1.png" width="750px">
</p>

This post describes the structure of the dashboard, and some ways to use it. In later posts we'll cover each one of these metrics in depth.  

## Deployment Rates & Results
Deployments are the conerstone to delivery.  This is why they are featured as the first item. If the end goal is delighting customers and creating amazing experiences for them, deployments are how orgs make that into a reality:

<p align="center">
  <img src="static/deploy_rate_change_failure.png" width="750px">
</p>

The upper left hand graph shows the deployment rate by datasource, and in aggregate.  This answers "How frequently are deploys happening?", and "By Which Datasources?".  The Deployment success ratio is another strong indicator of operational flakiness and general maturity. High failure rate is a strong indicator of operational instability, and jeopardizes smoothly deliverying to customers.  This can answer "How often are deployments failing in the given interval?", and "By which datasources are they failing?".

## Deployment Durations
The length of deployments are another indicator of operational maturity.  Long deployment times often cause backpressure to an organization which can cause batching of deploys in order to reduce the total time spent in deployment.  For many organizations, deployments are often a "hands-on" action, meaning that an engineer is manually executing and monitoring the deployment and rollout. Deployment duration is a great candidate for automation and improvement and often directly correlates with saved time.  This helps to make it very easy to calculate ROI on deployment initiatives and ValueStream helps to show the affect of that over time:

<p align="center">
  <img src="static/deploy_duration.png" width="750px">
</p>

On the left hand side is the quick view of delivery durations over the interval by event source. The right side shows a timeseries view over the interval. 

## Issue Duration

<p align="center">
  <img src="static/issue_duration.png" width="750px">
</p>

--- 

Drop us a line ([@OpAnValueStream](https://twitter.com/OpAnValuestream)) if you’d like help getting started or do you have in an integration request.  We'd love to hear feedback!