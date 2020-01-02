# Creating Lasting Change in Organizations By Modifying Behavior

Creating sustainable long lasting change in human systems is only achievable though modifying human behavior. The difficulty is in modifying how people behave. Command and control telling people they have to change leads to hostility, resentment. On the opposite side of the spectrum not shepherding an organization leads to local fiefdoms emerging. This article describes a middle ground method to creating change through enhanced information management and system constraints.

This strategy is frequently seen in tech and especially relevant to distributed organizations, and is comprised of

\- **Informing** through structured data

\- **Alerting** of actions when they go out of bound

\- **Regulating** the set of possible allowed actions

# Inform

Inform structures and surfaces information to users

Informing requires understanding which metrics are important, where to instrument them, actually instrument them and then surface them through dashboards .

Informing is the foundation of change. Once data is available it makes it possible to empirically understand the problem, and profile the problem. Many times humans think there is a problem based on any number of common biases but when data is finally available it tells another story.

Informing helps to answer: what's the state of the system right now? Informing is required for later steps in order to measure the affects of any excitements. It's important that information is surfaced in a system that supports alerting, and programmatic querying.

# Alert

Alerting notifies a user in response to performing some action. The purpose of alerting is to establish a feedback loop between a person and actions that they take in order to help people understand the affect of their actions. Most alerts are setup to take place on certain important thresholds:

- "You submitted 3 Reviews Last week! Keep Up the Good Work!"
- A gas light has come on
- "The cost of this action costs \$X"

Alerts help establish consequences for actions, by actively notifying individuals of the affects of their actions. Without alerts it would be the individuals responsibility to consult the metrics surfaced through the **Inform** stage.

# Regulate

Regulation influences behavior by controlling (limiting) the number possible actions available to people. Regulation is frequently applied in traditional law and often has established consequences for certain sets of actions. In tech there are many ways to regulate actions without making explicit rules like "Thou shalt not \_\_\_\_". Explicit prohibition is absolutely effective in some cases: lead paint and CFCs, and many other laws.

Examples of regulation in tech are:

- Builds with failing tests are not promoted
- Build system only operates on Docker Images
- Service Scaffolding is created through a shared tool

It's really important to stress how profound and subtle the affects of Regulation can be. Regulation influences systems in its own ways, especially when there are competing concerns. If a team is being incentivized to deliver but have failing builds, and sufficient checks and balances don't exist throughout the process, when met with a failing test one option is to remove that test in order to get the build to "pass"!

# Example - Controlling Cloud Costs

In order to illustrate this in action consider the case of a tech organization with uncontrolled infrastructure spending. For this example, consider a company that uses a cloud provider like AWS. They have a global bill showing increasing AWS costs and would like to keep the costs from growing out of control.

## Inform

Informing requires surfacing data and presenting it in a structured human consumable way. For cloud costs this may involve tagging resources by key dimensions such as:

-   Team
-   Service
-   Resource Type
-   Resource Size

This information then has to be saved (surfaced) somewhere that supports creating actionable alerts. This may be a data warehouse, it may be a regular CSV dump from the cloud provider and load into a metric system. Surfacing may take place asynchronously through web hooks when resources are created.

Once data is surfaced to a metric store, a dashboard can be created in order to drill down costs by any supported dimension. This allows end users to see the cost of their resources. It also allows for profiling of the highest cost contributors and seeing the affect of different cost controlling experiments.

## Alert

There are many different strategies for alerting on cloud costs. An initial strategy may be to email or slack a weekly report to each team of their actual costs for the last week. There may be an alert when costs go above a certain threshold in an interval. More intelligent alerts could learn "normal" usage for a certain service or team, and then send out alerts when cost deviates over that norm.

It's important to consider the cadence of alerts in order to prevent alert "fatigue", but also to keep stakeholder and humans informed of their actions. This creates a spectrum: One end with no alerts ie humans have no automated notifications of the impact they are having on costs through the resources they are using. On the other end of the spectrum humans are alerted of every single action they are making. An acceptable solution that can be used to inform and affect human behavior usually sits somewhere in the middle. Targeted weekly rollups and high threshold based alerts are usually a good place to start.

## Regulate

There are many different ways to regulate cloud resource costs, each having their own tradeoffs in terms of throughput and latency. A naive approach may be to only allow key members the ability to provision or approve requests for resources. This requires that all resource requests be approved and enables the organization to tightly control cloud costs. The cost control that this method offers comes with serious throughput and latency tradeoffs, as it inserts a person for manual review.

Another way to regulate costs is to grant each team a static fixed amount of resources for certain intervals. It's then up to each team to use those resources effectively. A logical extension of this is to give each teams a fixed budget for resources.

Each of the examples above limits a teams ability to create cloud costs.

# Conclusion

Long lasting change requires influencing human behavior. Many times people will align with missions and change their behavior when presented with data that describes the affects of their actions. In other cases its necessary to actively alert individuals of the effects of their actions. Sometimes neither of these is enough to promote changing behavior and regulation is required.
