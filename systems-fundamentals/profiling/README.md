# Systems Fundamentals: Profiling

Successfully changing systems requires an understanding of the current system's state. Profiling is a tool for understanding systems at a point in time. Without a good understanding of the current state, changes can be suboptimal, counter productive, or even dangerous. Profiling is used to breakdown a system's current state using dimensions, and is a prerequisite for successfully modifying systems.

# What?

Profiling describes the current state of a system. Knowing the current state helps to inform changes. Consider the following goals and how profiling helps each.

- Reduce monthly spending. Requires understanding current spending.
- Eat healthier. Requires understanding what you're currently eating.
- Reduce electricity. Requires understanding the current breakdown of usage.
- Promote hiring diversity. Requires understanding employee breakdown by gender/demographic.
- Reduce / Consolidate debt. Requires understanding debt sources by lender.
- Diversify an investment portfolio. Requires understanding investments by category/risk.

Profiling shows a snapshot of a system at a point in time broken down by a series of dimension. Consider the goal to reduce monthly spending. Cutting spending requires understanding the breakdown of spending, and this is what profiling does. Profiling takes an overall number such as the amount of money someone spends in a month and splits it across a dimensions, such as "spending category". Online banks such as Bank of America provide this view with their accounts:

<p align="center">
  <img src="static/profile_spending_absolute.png">
</p>

The profile shows the total monthly spending of $2400 broken down by spending category. The categories follow including the amount of spending:

- Rent - $700
- Grocery - $600
- Child expenses - $400
- Incidentals - $300
- Transportation (payment, insurance, fuel) -$290
- Utilities - $110

Each category shows the total amount of monthly budget spent. It's easy to see that rent is the largest contributor to monthly spending for this month. Choosing a relevant dimension is part of profiling. This type of profile is called an "absolute" profile, since it includes the total amount of dollars for each dimension. 

A "relative" profile is another type of profile. Relative profiles list each value of the dimension along with the percentage of the total. 

<p align="center">
  <img src="static/profile_spending_relative.png">
</p>

Below lists the percentage based profile using the data from the absolute profile above:

- Rent - 29% ($700 / $2400)
- Grocery - 25% ($600 / $2400)
- Child expenses - 17% ($400 / $2400)
- Incidentals - 12.5% ($300 / $2400)
- Transportation (payment, insurance, fuel) - 12% ($290 / $2400)
- Utilities - 5% ($110 / $2400)

Profiling makes it easy to comparer dimensions. The profile above shows that rent is responsible for 29% of total monthly spending, while utilities only account for 5% of the total spending. When profiling it's useful to include both an absolute and percentage profile. This makes it easy to analyze the relative impact of a change in a dimension and then convert that to an absolute impact.

A profile of your own spending may produce different categories. Visualizations aren't necessary for profiling but can help to easily compare dimensions. The profile could be listed as a table or plain text, which is common for many business accounting reports. Profiling is frequently done within the context of accounting since data is often plentiful.

# Why / Risk

Profiling is essential to system design. Consider the example above. Pretend the person is trying to reduce expenses to put more money in savings, but has not performed a profile. The person feels like they are spending a lot of money on utilities so they resolve to try really hard to reduce their electricity consumption by cutting costs and are able to cut $15 off each month. The full profile informs 

Profiles show an objective breakdown of all sources for a certain behavior. If profiling isn't performed information can be missed. Effort There are a few risks with not performing a profile:

- Information can be missed since a complete view of the current state of the system is missing, may think that the breakdown is x, y, z and focus on x, but it is missing t
- If policies or solutions are crafted to address or redistribute allocations then the profile must be known. 

# How

The process of profiling is simple once data is acquired. Profiling relies on rich data and data acquisition is often the hardest part of profiling.

- Identify dimensions
- Observe the system
- Collect data
- Break down data: Percentage & Absolutes

## Profile Profiles "drilling-down"


# Conclusion

Profiling defines: What's happening right now in a system. Profiling focuses on understanding a system at a current point in time. Profiling defines the state of the system by dimensions, which are attributes of the system. It is a primitive tool that helps to perform more detailed system analyses.  
