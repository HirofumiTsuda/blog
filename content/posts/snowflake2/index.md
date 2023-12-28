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