---
title: Jointly Gaussian Variables
date: 2019-10-29 19:12:09
tags:
- Math
- Probability
categories:
- Probability & Random Process
---

# Gaussian Variables

$$x \sim \mathcal{N}(\mu,\sigma^2) : f(x | \mu , \sigma^2) = \frac{1}{\sqrt{2\pi \sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$$

- $\mu$ is the mean or expectation of the distribution
- $\sigma$ is the standard deviation
- $\sigma^2$ is the variance

# Jointly Gaussian Variables

$$\mathbf{X} \sim \mathcal{N_k}(\mathbf{\mu},\mathbf{\Sigma}): f_{\mathbf{X}}(x_1,\cdots,x_k) = \frac{\exp(-\frac{1}{2}(\mathbf{x}-\mathbf{\mu})^T\mathbf{\Sigma}^{-1}(\mathbf{x}-\mathbf{\mu}))}{\sqrt{(2\pi)^k|\mathbf{\Sigma}|}}$$

- $\mathbf{\mu} = E[\mathbf{X}] = (E[X_1],E[X_2],\cdots,E[X_k])^T$
- $\mathbf{\Sigma}$: $\Sigma_{ij} = E[(X_i-\mu_i)(X_j-\mu_j)] = Cov[X_i,X_j]$

## Linear Transformation of Gaussian Variables

If $X\sim \mathcal{N_n}(\mu_x,\Sigma_x)$ and $Y^m = A^{m\times n}X^n$, then $Y \sim \mathcal{N}(A\mu_x,A\Sigma_x A^T)$

Prove for $n=m$:
$$\begin{aligned}
f_Y(y) &= f_X(A^{-1}y)/|A|\\
&= \frac{\exp(-\frac{1}{2}(A^{-1}y-\mu_x)^T\Sigma_x^{-1}(A^{-1}y-\mu_x))}{(2\pi)^{n/2}|\Sigma_x|^{1/2}|A|}\\
&= \frac{\exp(-\frac{1}{2}(y-A\mu_x)^T(A\Sigma_x A^T)^{-1}(y-A\mu_x))}{(2\pi)^{n/2}|A\Sigma_x A^T|^{1/2}}\\
\end{aligned}$$

## Example

$\mathbf{X}$: independent, zero-mean, unit-variance Gaussian random variables. Build $\mathbf{Y}$ in terms of $\mathbf{X}$ so that $\mathbf{Y} \sim \mathcal{N}(\mathbf{\mu},\mathbf{\Sigma})$

Solutions:

- Find the matrix satisfying $\Sigma = AA^T$
- $Y = A\mathbf{X}+\mathbf{\mu}$