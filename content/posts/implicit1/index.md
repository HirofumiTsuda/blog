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
This method uses an implicit feedback like the number of clicks of a certain user.

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

$$ 
\begin{equation}
\min_{P, Q} \|| R - PQ\||_F + \lambda (\|| P \||_F + \|| Q \||_F),
\end{equation}
$$

where $R$ is a matrix whose $(u,i)$-th component is $r_{u, i}$ and $\|| X \||_F$ denotes the Frobenius norm of $X$. Here there is a parameter you choose about the dimension. If the number of users and the number of items denote $m$ and $n$ respectively, then the two matrices $P$ and $Q$ belong to $P \in \mathbb{R}^{m \times k}$ and $Q \in \mathbb{R}^{k \times n}$. The parameter $k$ is what you have to choose. 

Of course the above problem is not convex with respect to the two variables $P$ and $Q$. However, if the matrix $P$ is fixed, then the problem is convex with respect to $Q$. It means that solutions are obtained after solving with respect to either of P and Q alternatively.

The above is a fundamental of a matrix factorization model. Let us see an implicit feedback model.

## Matrix Factorization for Implicit Feedback 

In the above model, it is assumed that there is no missing value. However in a practical case some values may be missed. For example, if you consider a case where the number of clicks are used, all the users do not click all the items: some items are never seen by some users.

Furthermore, the number of clicks is not a explicit feedback from users. In an EC sites, an explicit feedback is purchase-records. The number of clicks are thought as an implicit-feedback.

To overcome those obstacles, an implicit feedback model has been introduced. The optimization model is written as follows.

$$
\begin{equation}
\begin{split}
& \min \sum_{r_{u,i} \mbox{ exists}} c_{u, i}(s_{u,i} - \mathbf{p}_u^\top \mathbf{q}_i)^2 + \lambda (\\|\mathbf{p}_u\\| + \\|\mathbf{q}_i\\|) \\\
s.t. & \mbox{ } \mathbf{p}_u, \mathbf{q}_i \in \mathbb{R}^k,
\end{split}
\end{equation}
$$

where $\||\mathbf{x}\||$ denotes the $l_2$ norm of $\mathbf{x}$,

$$
\begin{equation}
\begin{split}
s_{u,i} &= \left\\{ \begin{array}{cc}
1 & r_{u,i} > 0 \\\
0 & r_{u,i} = 0
\end{array}
\right. \\\
c_{u,i} &= (1 + \alpha r_{u,i}),
\end{split}
\end{equation}
$$

and $\alpha > 0$ is a parameter you choose. After solving the above problem in the same manner as a matrix factorization model, a matrix $\hat{R}$ can be constructed as

$$
\begin{equation}
\hat{R}_{u,i} = \hat{\mathbf{p}}_u^\top \hat{\mathbf{q}}_i.
\end{equation}
$$

In the above equation, we have written the obtained solutions as $\hat{\mathbf{p}}_u$ and $\hat{\mathbf{q}}_i$. You can recommend items using the values of $\hat{R}$ (values are thought as scores!).

The differences between an implicit model and an explicit one (shown in the matrix factorization model) are as follows.

- An implicit feedback is normalized to 0 and 1 and the normalized values are used in norms.
- The value observed in an implicit feedback is directly used in weights.

As seen in the implicit feedback model, an implicit feedback like the number of clicks is transformed into either of 0 or 1. Those values are approximated using vectors $\mathbf{p}_u$ and $\mathbf{q}_i$.

The original feedback is contained in the weight $c_{u,i}$. If the number of clicks against a given item by a certain user is large, then it is considered as important and the corresponding weight is set larger.

## Conclusion

This post shows models of a matrix factorization and an implicit feedback model. Those two have similarities and we have seen them.

Next a developed model using Bayesian would be shown!

## References
- [Hu] Hu, Yifan, Yehuda Koren, and Chris Volinsky. "Collaborative filtering for implicit feedback datasets." 2008 Eighth IEEE international conference on data mining. Ieee, 2008.
