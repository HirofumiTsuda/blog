---
title: "Snowflake Architectures: Query Processing"
date: 2023-12-28T09:16:47+09:00
draft: false
categories: ["tech"]
tags: ['snowflake', 'architectures']
---

<!--more-->

## Introduction

In [the previous post]({{< ref "/posts/snowflake1/index.md" >}}), a service called `Could Service` has been shown. That service does not execute queries although result cache and metadata are managed there.
Here another service called `Query Processing` is shown and this service is where queries are processed and executed.

As shown in [this article](https://docs.snowflake.com/en/user-guide/cost-understanding-compute), costs of Snowflake heavily depend on computing. To reduce those costs, it is necessary to understand this Query Processing service.

The core of this Query Processing service is a warehouse. Let us start with a warehouse.

## Warehouse

A warehouse is where queries are processed and executed. On AWS, it means EC2 instances (Snowflake does not publish what instance type is used though). 
As a parameter assigned to a warehouse, a size is what you have to choose. Its size follows ones of T-shirts like XS, S and M... Once you choose an one size larger warehouse,
then the speed to process and execute queries would be twice faster than one of an one size smaller warehouse. 

From the above explanations, you may think it is the best way to choose the warehouse with the maximum size. However, there are three facts to be known.

- Using an one size larger warehouse means costs get twice larger.
- Costs involving a warehouse depend on how long the warehouse has been on (not depend how lond the warehouse has worked!)
- The minimum duration for calculating costs is 1 minute. Even if a warehouse has been on for less than 1 minute, the cost is calculated as one for 1 minute.

The first fact is the relation between a size and a cost. Since using an one size larger warehouse leads to achieve twice faster processing-speed (time taken to process a query would get half), the total cost would not change a lot by changing a warehouse. The total cost for a query mainly depends on the query itself.

Second, the costs for a warehouse is calculated based on how long the warehouse has been on. If a warehouse does not process any queries but is on, a cost is incurred.
One tip to deal with reducing such a cost is using the shutdown and resume services. On Snowflake, a shutdown function is provided and using that a warehouse gets down while no queries are submitted. Once a query is submitted to the warehouse, that gets turned on (the resume function).
While that warehouse sleeps, no costs are incurred.

Finally, the minimum duration is 1 minute. If you don't use a warehouse for less than 1 minute, it is considered that you use that warehouse for 1 minute.
Therefore it is necessary to pay attention to execute a query taking short time.





