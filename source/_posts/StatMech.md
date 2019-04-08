---
title: Statistical Mechanics
date: 2019-04-01 10:32:25
tags:
- PChem
categories:
- NoteBook
---

Lecture notes for course CHEM553 in University of Washington...

 # Basics of Probability Theory

## "probability space" 

It consists of three things:
1. $\Omega$: sample space: "set of all outcomes", "state space"
2. $\Sigma$: $\sigma$-algebra: "set of all possible subsets of $\Omega$"
3. P: probability measure

Rules:
1. Fore every element(A)$\in \Sigma$, $\ 0\leq P(A) \leq 1$
2. $P(\emptyset)=0$
3. $\ P(A\bigcup B)=P(A)+P(B)$, if $A\bigcap B=\emptyset$

Example:
1. If $\Omega$ discrete: $\Omega=\lbrace \omega_1,\omega_2,\omega_3,\cdots\rbrace$
   - assign a probability for each "atomic event" $\omega \in \Omega$
   - for subsets of $\Omega$ that contain more than one element, use Rule 3

    Roll a die: $\Omega=\lbrace 1,2,3,4,5,6 \rbrace$
     - P(k)=1/6 for k in {1,2,3,4,5,6}
     - $\Sigma=\lbrace \emptyset,\{ 1 \},\{2\},...,\{1,2\},\{1,3\},...,\{1,2,3\},...,\{2,4,6\},...,\Omega \rbrace$
     - P({1,2})=P({1}U{2})=P({1})+P({2})=1/3

2. If $\Omega \subseteq R$ (not discrete)
   
   define a function p(x) (probability density) for each $x\in \Omega$ such that
   - $p(x) \geq 0$
   - $\int_\Omega \text{d}x p(x) = 1$
   
   Example: pick a random number between 0 and 1 ($\Omega$=[0,1]), probability that the number is in [1/4,1/2]:
   $$p(x) =
    \begin{cases}
    1,  & \text{if } 0\leq x \leq 1 \\
    0, & \text{if } x<0 \ or\ x >1
    \end{cases}\\
    \int_{\frac{1}{4}}^{\frac{1}{2}} p(x)dx=\frac{1}{4}$$
    
## Random Variable

State space can be everything besides number, so that we don't do math directly on them but map them onto real numbers, which is described with random variable. 

$$\hat X: \Omega \rightarrow R^n$$

Example: Rolling a die
  - case 1

    $$\hat X = \begin{cases}0 &\text{if $\omega$ is odd}\\1 &\text{if $\omega$ is even}\end{cases}$$

    State space $\omega$ can be 1, 2, 3, 4, 5, or 6 with probability of 1/6, respectively. $\hat X$ reflect each $\omega$ to a new state space with new probability. $P_{\hat X}(x)=P(\{\omega \in \Omega:\hat X(\omega)=x\})$. x can be 0 or 1. So, $P_{\hat X}(0)=P(\{1,3,5\})=P(\{1\})+P(\{3\})+P(\{5\})$

  - case 2:

    $$\hat Y(\omega)=\begin{cases}0 &\text{if } \omega \leq 3\\1 &\text{if } \omega >3\end{cases}$$

  - Two RVs $\hat X$, $\hat Y$ are independent, if $P(\hat X=x \text{ and } \hat Y=y)=P(\hat X=x)P(\hat Y=y)$ for all x and y
  
    $P(\hat X=x \text{ and } \hat Y=y)=P(\{1,3\})=\frac 2 6 \\
    P(\hat X=0)\cdot P(\hat Y=0)=P(\{1,3,5\})\cdot P(\{1,2,3\})=\frac 1 4$

After we know the distribution, we can know:
  1. Expectation Value
      - $<\hat X>=\sum_{\omega \in \Omega} P(\omega)\hat X(\omega)$ (discrete)
      - $<\hat X>=\int_\Omega d\omega\ p(\omega)\hat X(\omega)$ (continuous)
  2. Variance: Var$(\hat X)=<\hat {X^2}>-<\hat X>^2$
  3. Standard deviation: $\sqrt {Var(\hat X)}$

But in chemistry, we do experiment first to get expectations and hope to find their distributions. It can be achieved if we choose the observation carefully. Useful trick:

1. discrete RV $\hat X$. 
   
   Define a new RV: 
    $$\hat Y(\omega)=\begin{cases}1 &\text{if } \hat X(\omega)=x\\0 &\text{if } \hat X (\omega) \neq x\end{cases}=\delta_{\hat X(\omega),x}\\
<\hat Y>=<\delta_{\hat X(\omega),x}>= \sum_{\omega=\Omega} P(\omega) \delta_{\hat X(\omega),x}\\
=P\{\omega\in\Omega:\hat X(\omega)=x\}=P_{\hat X}(x)$$

2. continuous:
   $$\hat Y(\omega)=\delta (\hat X(\omega)-x)\\
   <Y>=<\delta(\hat X(\omega)-x>\\
   =\int_{\Omega}d\omega p(\omega)\delta (\hat X(\omega)-x)=p(x)$$

   - Delta function
    $$\delta (x)=\begin{cases}\infty & x=0\\ 0 & x \neq 0\end{cases}\\
    \delta (x)=\int_{-\infty}^\infty f(x)\delta (x)=f(0)\\
    \int_{-\infty}^\infty dx f(x)\delta (x-a)=f(a)$$

## Different Types of RVs

1. Two RVs $\hat X$, $\hat Y$ are independent, if $P(\hat X=x \text{ and } \hat Y=y)=P(\hat X=x)P(\hat Y=y)$ for all x and y
2. Two RVs are uncorrelated if $<\hat X\hat Y>=<\hat X><\hat Y>$

- Examples: roll a die

  $$\hat X(\omega)=\begin{cases}0 &\text{if $\omega$ odd}\\1 & \text{if $\omega$ even}\end{cases} \;  <\hat X>=\frac 1 2 \\
  \hat Y(\omega)=\begin{cases}0 &\text{if $\omega\in${1,2,3}}\\1 &\text{if $\omega\in${4,5,6}}\end{cases} \; <\hat Y>=\frac 1 2$$

  $<\hat X\hat Y> \\
  =\sum_{\omega\in\Omega}P(\omega)\hat X(\omega)\hat Y(\omega)\\
  =P(1)0+P(1)0+P(3)0+P(4)1+P(5)0+P(6)1\\
  =\frac 1 3\\
  \Rightarrow \hat X, \hat Y$  are correlated

3. conditional probability

$$P(\hat X=x|\hat Y=y)=\frac{P(\hat X= x\ and\ \hat Y=y)}{P(\hat Y =y)}$$

- Examples: $P(\hat X=0|\hat Y=0)=\frac{P(\{1,3\})}{P\{1,2,3\}}=\frac 2 3$

## Central Limit Theorem

So far, $\Omega$ was the set of possible outcomes of one experiment. Now: perform N independent experiments. Examples: roll a die 3 times: $\Omega^1=${(1,1,1),(1,1,2),(1,1,3),...}$=\Omega^3$, $P^1(\omega_1,\omega_2,\omega_3)=P(\omega_1)P(\omega_2)P(\omega_3)$

If $\hat X$ is a RV on $\Omega$, we can define new RVs on $\Omega '$:

$$\hat X_i (\omega_1,\omega_2,\cdots ,\omega_N)=\hat X(\omega_i) \tag{i=1,...,N}$$

**central limit theorem**

$\hat X_1,\hat X_2,\cdots ,\hat X_N$ are independent identically distributed (iid) RVs with mean $\mu$ and variance $\sigma^2$.Then $p(\hat S=s)$ can represent normal distribution with mean $\mu$ and variance $\sigma^2/N$

$$\hat S = \frac 1 N \sum_{i=1}^N X_i(\omega)\\
p(\hat S=s)\stackrel{N\rightarrow \infty}{\longrightarrow} \frac{1}{\sqrt {2\pi\sigma^2/N}}e^{-\frac{(s-\mu)^2}{2\sigma^2/N}}$$

The more experiments have been done, the smaller the standard deviation $\sqrt{\sigma^2/N}$. The center (mean) doesn't relate with the number of experiments. s can have more variables than $\omega$ (e.g. $\omega$ can only be 0 or 1, the s can be any real number in [0,1].) So here we use probability density p instead of probability of a certain number.

# Statistical Mechanics

classical: gaseous atoms in a cubic box with length of L. what should to know to describe this system (N atoms)? 

positions: $\vec r_1,\vec r_2,\cdots ,\vec r_N$ and momentums: $\vec p_1,\vec p_2,\cdots,\vec p_N$. Each r and p contains three elements (x,y,z). so microstate $\omega=(\vec r_1,\vec r_2,\cdots ,\vec r_N;\vec p_1,\vec p_2,\cdots,\vec p_N)$ contains 6N elements. $\Omega=[0,L]^{3N}\times \bf{R}^{3N}$