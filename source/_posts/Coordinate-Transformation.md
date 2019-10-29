---
title: Coordinate Transformation
date: 2019-10-28 16:34:41
tags:
- Math
- Probabality
categories:
- Probability & Random Process
---

# Jacobian Matrix

If $\mathbf{f}:\mathbb{R}^n\rightarrow \mathbb{R}^m$ is a function  that maps from n-dimensional Euclidean space to m-dimensional Euclidean space. The Jacobian matrix of $\mathbf{f}$ is defined to be a $m\times n$ matrix, denoted by $\mathbf{J}$, with $\mathbf{J}_{ij} = \frac{\partial f_i}{\partial x_j}$, or

$$\mathbf{J^f_x} = \begin{bmatrix} \frac{\partial f_1}{\partial x_1} & \cdots & \frac{\partial f_1}{\partial x_n}\\
\vdots &\ddots &\vdots\\
\frac{\partial f_m}{\partial x_1} & \cdots & \frac{\partial f_m}{\partial x_n} \end{bmatrix} $$


where $\mathbf{f} = \mathbf{J_x^f}\cdot \mathbf{x}$. Similarly, $\mathbf{x} = \mathbf{J_f^x}\times \mathbf{f}$ and $\mathbf{J_f^x} = \mathbf{J_x^f}^{-1}$

# Coordination Transformation

Given a function $f_X(\mathbf{x})$ and two vectors withe the same dimension $\mathbf{x}$ and $\mathbf{z}$, how to find $f_Z(\mathbf{z})$?

## one-to-one map
Find Jacobian matrix $J^z_x$ or $J^x_z$, so that $z = J^z_x \cdot x$ and $x = J_z^x \cdot z$

$$f_Z(\mathbf{z}) = \left|\mathbf{J^x_z}\right| \cdot f_X(\mathbf{\mathbf{J_z^x}\cdot\mathbf{x}}) = f_X(\mathbf{\mathbf{J_z^x}\cdot\mathbf{x}})/|\mathbf{J^z_x}| $$

## many-to-one map

$$\begin{aligned}f_Z(\mathbf{z}) &= \sum_{x: g(x)=z} \left|\mathbf{J^x_z}\right| \cdot f_X(\mathbf{\mathbf{J_z^x}\cdot\mathbf{x}}) \\
&= \sum_{x: g(x)=z} f_X(\mathbf{\mathbf{J_z^x}\cdot\mathbf{x}})/|\mathbf{J^z_x}| \end{aligned}$$

- note: sum can be integral, see [example](#eg)
  
# <jump id="eg">example</jump>

## Question

Let X, Y be continuous random variables with the following joint probability distribution function (p.d.f.)
$$f_{X,Y} = 2e^{-(x+y)},\; 0<x<y$$
Define $z=x+y$, $w=\frac{y}{x}$, determine the joint p.d.f. of z, w. Are they independent?

## Answer

$$ x=\frac{z}{w+1}, \; y= \frac{zw}{w+1}\\$$

- To find the joint p.d.f.

$$\begin{aligned}
J_{xy}^{zw} &= \begin{bmatrix} 1 & 1\\ -\frac{y}{x^2} & \frac{1}{x}\end{bmatrix} \\
|J_{xy}^{zw}| &= \frac{1}{x}+\frac{y}{x^2} = \frac{(w+1)^2}{z}\\
f_{Z,W} &= 2e^{-z} \times |J^{xy}_{zw}| = \frac{2ze^{-z}}{(w+1)^2} \end{aligned}$$

- How to find the marginal p.d.f.?
  - For a given value z, $f_Z(z)$ equals the sum of all $f_{X,Y}(x,y)$ satisfying $x+y=z$. This means, for a given z, if x is set, then y is uniquely determined (i.e. z-x). We can integral over x in the range of $(0,\frac{z}{2})$ since $x<y$ and $x+y=z$.

    $$f_Z(z) = \int_{0}^{\frac{z}{2}} 2e^{-(x+z-x)} \mathrm{d}x = ze^{-z}$$

  - Similarly, to get $f_W(w)$, we can integral over x for all $y = wx$ from $0$ to $+\infty$.
    
    $$f_W(w) = \int_{0}^{+\infty}2e^{-(x+wx)}\mathrm{d}x = \frac{2}{w+1}$$

- Since $f_{Z,W}\neq f_Z(z)f_W(w)$, they are not independent.

# Relevant Note

- $A=\begin{bmatrix}a&b\\c&d\end{bmatrix}$, $A^{-1}=\frac{1}{|A|}\begin{bmatrix}d&-b\\-c&a\end{bmatrix}$, where $|A|=ad-bc$
