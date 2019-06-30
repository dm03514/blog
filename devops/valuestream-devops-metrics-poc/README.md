ValueStream: DevOps Metrics - Observing Delivery Across Multiple Systems

DevOps focus on reducing feedback loops in order to reduce lead time to increase velocity and the rate of successful software deliveries. Inherent in this are 3 key metrics:BLANK.  Recently accelerate found that measuring these metrics are a cornerstone of high performance teams.the way we gather these metrics are often through proxies and vary from company to company.  Gathering delivery data is often the wild west Jeera swim lanes are used as proxies there are gaps some data does not need to be the case this post tracing is an excellent candidate for modeling organizational software delivery across multiple disparate systems like jira github and Jenkins Modeling delivery as a distributed trace across multiple different subsystems to be an effective way to operationalize these metrics.  ValueStream is a project that aims to be a solution to this by providing a single application to ease colleciton of devops metrics across all dependencies invovled.  This post walks through the current state of the industry, the major issues with the current approaches to gathering devops metrics, and how ValueStream can help address these issues.



Current State


SOftware is developed across many Systems. The minimum usually required are an Issue Tracker, Version Control, and Delivery Sysetm.  

SHOW GRAPH

The process (with each stage) software takes from an idea to running (hopefully providingn vaalue) is called a Valuestream.  Lead time, (the total time an issue takes from idea to running in production) is a cordernerstone metric, and encompasses the total amount of time an item spends from start to delivery:

SHOW GRAPH OF LEADTIME.


Understanding the total time work takes to delivery is just as important as BLANK.



