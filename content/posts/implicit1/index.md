---
title: "Fundamental of Matrix Factorization in Recommendation"
date: 2024-01-09T19:40:18+09:00
draft: false
math: true
categories: [ "math" ]
tags: ["optimization", "recommendation"]
---

<!--more-->

## Introduction

Have you seen recommendation logics? Probably you say "Yes" because they are used in EC sites like amazon.
To attract users those recommendation systems are necessary.

Even in those systems, mathematics is used. As seen in [Hu's article](#references), a recommendation logic called `implicit feedback` lies on matrices and optimizations.
This method uses an implicit feedback like the number of clicks of a certain user. The implicit feedback method can be regarded as an optimization with a given metric.

This post shows logics for those matrix factorization methods. Let's start with defining formulae! 


## Matrix Factorization

Here the following symbols are used.

- $u$: the index of an user
- $i$: the index of an item
- $r_{u, i}$: the value given to the item $i$ by the user $u$

A set of values $r_{u, i}$ is regarded as a matrix when they are aligned with respect to the two kinds of indices $u$ and $i$. As a value, for example, a rate is often chosen.
Please think of a movie-rate: the number 1 denotes the worst and the number 5 denotes the best. A set of those values is one of rates given by users.

If rates of all the items are given by all the users, all the entities in the matrix $\\{r_{u,i}\\}$ are given, that is, there are no missing values in the matrix.
The main idea of Matrix Factorization is to estimate two matrices $P$ and $Q$. Those two are minimizers of the following optimization problem.




## Matrix Factorization for Implicit Feedback 
aaa

## References
- [Hu] Hu, Yifan, Yehuda Koren, and Chris Volinsky. "Collaborative filtering for implicit feedback datasets." 2008 Eighth IEEE international conference on data mining. Ieee, 2008.
