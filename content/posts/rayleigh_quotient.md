---
title: "Proof of Rayleigh Quotient"
date: 2023-12-26T19:51:06+09:00
draft: false
math: true
---

<!--more-->

Beginning with my favorite mathematics!

## Introduction

Rayleigh Quotient is one of my favorite theorems and a problem involving the theorem is a good example as a solvable optimization problem although that is not convex.
Here I give it a try to write down its proof and I am definitely glad if this post helps you!

## Reference
Everything is written here: [Optimization Algorithms on Matrix Manifolds](https://www.amazon.co.jp/Optimization-Algorithms-Matrix-Manifolds-Absil/dp/0691132984).

## What is `Rayleigh Quotient`?

A Rayleigh Quotient is a quadratic form with a norm-equality constraint. There is often a case where you consider a problem like:

$$min_{\mathbf{x} \in \mathbb{R}^n} \frac{\mathbf{x}^\top A \mathbf{x}}{\mathbf{x}^\top \mathbf{x}},$$ where $\mathbf{x}$ is a $n$-dimension vector and $A$ is an $n$ by $n$ symmetric matrix, respectively. Here the objective function is minimized. Of course you can maximize that. The following discussion is independent of which you choose.

The quantity stays through a transformation like $\mathbf{x} \rightarrow \alpha\mathbf{x}$, where $\alpha$ is a scalar. Thus without loss of generality, we assume $||\mathbf{x}||=1$. Here $||\mathbf{x}||$ denotes the $l_2$ norm of $\mathbf{x}$. Therefore, the Rayleigh Quotient equals to the following:

$$ 
\begin{equation}
\min_{\mathbf{x} \in \mathbb{R}^n} \mathbf{x}^\top A \mathbf{x} \\\
s.t. ||\mathbf{x}|| = 1.
\end{equation}
$$

Hence the Rayleigh Quotient is a problem with a norm constraint. Apparently this is not convex. However it is known that the problem is solvable and the optimal value and optimizer are the minimum (or maximum) eigenvalue and its corresponding eigenvector.

You may think of one with a metric. For example, a problem with a constraint like $\mathbf{x}^\top G \mathbf{x} = 1$, where $G$ is a positive definite matrix (since $G$ means a metric!). In such a case, $G$ can be decomposed as $G = L^\top L$ since $G$ is a Gram matrix. Using $\mathbf{y} = L\mathbf{x}$ that problem can be interpreted as the Rayleigh Quotient with $\mathbf{y}$.

## Proof

First thing we have to do is to decompose the matrix $A$. Since A is a symmetric matrix, $A$ is rewritten using its eigenvalues and eigenvectors. To write that, let us define $\lambda_{i}$ be the $i$-th eigenvalue and $\mathbf{v}_{i}$ be the  $i$-th eigenvector. 

It is known that the vectors $\\{\mathbf{v}_i\\}$ span the vector space $\mathbb{R}^n$. Using them a vector $\mathbf{x}$ is rewritten as 

$$
\mathbf{x} = \\sum_{i=1}^{n} a_i \mathbf{v}_i.
$$

We can assume each $\mathbf{v}_i$ is a vector with the $l_2$ norm being 1 and then the $l_2$ norm of a vector (a row sorted by the indices $i$) $\\{a_i\\}$ is 1. Using them, the quadratic form is rewritten as

$$
\mathbf{x}^\top A \mathbf{x} = \sum_{i=1}^n a_i^2 \lambda_i \geq \sum_{i=1}^n a_i^2\lambda_{\min} = \lambda_{\min},
$$
where $\lambda_{\min}$ is the smallest eigenvalue.
The bound comes from the fact $\\{a_i\\}$ has the $l_2$ norm-constraint.  
It is clear that the optimal value is achieved when a corresponding eigenvector is chosen as $\mathbf{x}$. In the same manner, one with maximization is achieved.

## Conclusion
Here a Rayleigh Quotient is shown. This problem often appears in cases where the value of a norm is fixed. For example, energy is given and fixed.

This quotient can be extended into manifolds like Stiefel manifold and Grassmann manifold...but honestly I have not understood them! Since they denote subspaces in a vector space, they often appear in our real world!
