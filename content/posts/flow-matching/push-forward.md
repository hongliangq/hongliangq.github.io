---
date: '2025-09-27T14:46:00+08:00'
draft: false
title: 'How to Understand Push-Forward Map'
---

# How to understand push-forward?

### 1. Problem

We start with a random variable $X \sim p_X$ and we apply a transformation $Y = \psi(X)$.

**Question:** what is the distribution of $Y$?

If we know how to transform densities, then we can generate new random variables, compute expectations, and model distributions in a flexible way.

------

### 2. Why Not Simulate?

Sure, one could sample from $X$ and apply $\psi$. But often in theory, statistics, and ML, we need an **explicit formula for the density** $p_Y$. For example:

- in **change of variables for integrals** (probability, Bayesian inference),
- in **normalizing flows** (deep generative models),
- in **transport maps** (optimal transport, flow matching, diffusion).

So we need the density $p_Y$ written down.

------

### 3. Conditions

Assume $\psi$ is a diffeomorphic map.

The formula:
$$
p_Y(y) = p_X(\psi^{-1}(y)) \; \big|\det \partial_y \psi^{-1}(y)\big|,
$$
which tells us how the density ***reshapes*** when the space itself is distorted by $\psi$.

- The $\psi^{-1}(y)$ part finds where $y$ came from in the original space.
- ***The determinant part adjusts for local stretching/squeezing of volumes***.

------

### 4. The Push-Forward

Because $\psi$ is literally ***pushing forward*** the probability measure $p_X$ into a new measure $p_Y$.
$$
p_Y = \psi_\# p_X.
$$
This is the same idea as saying: if I know how probability is distributed in one space, and I warp the space smoothly, I can figure out the new distribution.

## Q: How is this explained as a probability path in flow matching?

In flow matching, We have two distributions: a source $p_0$ and a target $p_1$. Flow matching constructs a **probability path** $\{p_t\}_{t\in[0,1]}$ that smoothly transforms $p_0$ into $p_1$. The path is defined via a **diffeomorphic map** $\psi_t : \mathbb{R}^d \to \mathbb{R}^d$ (smooth, invertible).

At each time $t$, the distribution is defined as the **push-forward** of the source by the map $\psi_t$:
$$
p_t = \bigl( \psi_t \bigr)_\#p_0,
$$
which means take samples from $p_0$, push them through the transformation $\psi_t$, and that gives you the distribution $p_t$.

Therefore, push-forward explains how each $\psi_t$ reshapes densities.
