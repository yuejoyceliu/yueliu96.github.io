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
    0, & \text{if } x<0 \text{ or } x >1
    \end{cases}\\
    \int_{\frac{1}{4}}^{\frac{1}{2}} p(x)dx=\frac{1}{4}$$
    
## Random Variable

State space can be everything besides number, so that we don't do math directly on them but map them onto real numbers, which is described with random variable. 

$$\hat{X}: \Omega \rightarrow R^n$$

Example: Rolling a die
  - case 1

    $$\hat{X} = \begin{cases}0 &\text{if $\omega$ is odd}\\1 &\text{if $\omega$ is even}\end{cases}$$

    State space $\omega$ can be 1, 2, 3, 4, 5, or 6 with probability of 1/6, respectively. $\hat{X}$ reflect each $\omega$ to a new state space with new probability. $P_{\hat{X}}(x)=P(\{\omega \in \Omega:\hat{X}(\omega)=x\})$. x can be 0 or 1. So, $P_{\hat{X}}(0)=P(\{1,3,5\})=P(\{1\})+P(\{3\})+P(\{5\})$

  - case 2:

    $$\hat{Y}(\omega)=\begin{cases}0 &\text{if } \omega \leq 3\\1 &\text{if } \omega >3\end{cases}$$

  - Two RVs $\hat{X}$, $\hat{Y}$ are independent, if $P(\hat{X}=x \text{ and } \hat{Y}=y)=P(\hat{X}=x)P(\hat{Y}=y)$ for all x and y
  
    $P(\hat{X}=x \text{ and } \hat{Y}=y)=P(\{1,3\})=\frac 2 6 \\
    P(\hat{X}=0)\cdot P(\hat{Y}=0)=P(\{1,3,5\})\cdot P(\{1,2,3\})=\frac 1 4$

After we know the distribution, we can know:
  1. Expectation Value
      - $<\hat{X}>=\sum_{\omega \in \Omega} P(\omega)\hat{X}(\omega)$ (discrete)
      - $<\hat{X}>=\int_\Omega d\omega\ p(\omega)\hat{X}(\omega)$ (continuous)
  2. Variance: Var$(\hat{X})=<\hat {X^2}>-<\hat{X}>^2$
  3. Standard deviation: $\sqrt {Var(\hat{X})}$

But in chemistry, we do experiment first to get expectations and hope to find their distributions. It can be achieved if we choose the observation carefully. Useful trick:

1. discrete RV $\hat{X}$. 
   
   Define a new RV: 
    $$\hat{Y}(\omega)=\begin{cases}1 &\text{if } \hat{X}(\omega)=x\\0 &\text{if } \hat{X} (\omega) \neq x\end{cases}=\delta_{\hat{X}(\omega),x}\\
<\hat{Y}>=<\delta_{\hat{X}(\omega),x}>= \sum_{\omega=\Omega} P(\omega) \delta_{\hat{X}(\omega),x}\\
=P\{\omega\in\Omega:\hat{X}(\omega)=x\}=P_{\hat{X}}(x)$$

2. continuous:
   $$\hat{Y}(\omega)=\delta (\hat{X}(\omega)-x)\\
   <Y>=<\delta(\hat{X}(\omega)-x>\\
   =\int_{\Omega}d\omega p(\omega)\delta (\hat{X}(\omega)-x)=p(x)$$

   - Delta function
    $$\delta (x)=\begin{cases}\infty & x=0\\ 0 & x \neq 0\end{cases}\\
    \delta (x)=\int_{-\infty}^\infty f(x)\delta (x)=f(0)\\
    \int_{-\infty}^\infty dx f(x)\delta (x-a)=f(a)$$

## Different Types of RVs

1. Two RVs $\hat{X}$, $\hat{Y}$ are independent, if $P(\hat{X}=x \text{ and } \hat{Y}=y)=P(\hat{X}=x)P(\hat{Y}=y)$ for all x and y
2. Two RVs are uncorrelated if $<\hat{X}\hat{Y}>=<\hat{X}><\hat{Y}>$

- Examples: roll a die

  $$\hat{X}(\omega)=\begin{cases}0 &\text{if $\omega$ odd}\\1 & \text{if $\omega$ even}\end{cases} \;  <\hat{X}>=\frac 1 2 \\
  \hat{Y}(\omega)=\begin{cases}0 &\text{if $\omega\in${1,2,3}}\\1 &\text{if $\omega\in${4,5,6}}\end{cases} \; <\hat{Y}>=\frac 1 2$$

  $<\hat{X}\hat{Y}> \\
  =\sum_{\omega\in\Omega}P(\omega)\hat{X}(\omega)\hat{Y}(\omega)\\
  =P(1)0+P(1)0+P(3)0+P(4)1+P(5)0+P(6)1\\
  =\frac 1 3\\
  \Rightarrow \hat{X}, \hat{Y}$  are correlated

3. conditional probability

$$P(\hat{X}=x|\hat{Y}=y)=\frac{P(\hat{X}= x\ and\ \hat{Y}=y)}{P(\hat{Y} =y)}$$

- Examples: $P(\hat{X}=0|\hat{Y}=0)=\frac{P(\{1,3\})}{P\{1,2,3\}}=\frac 2 3$

## Central Limit Theorem

So far, $\Omega$ was the set of possible outcomes of one experiment. Now: perform N independent experiments. Examples: roll a die 3 times: $\Omega^1=${(1,1,1),(1,1,2),(1,1,3),...}$=\Omega^3$, $P^1(\omega_1,\omega_2,\omega_3)=P(\omega_1)P(\omega_2)P(\omega_3)$

If $\hat{X}$ is a RV on $\Omega$, we can define new RVs on $\Omega '$:

$$\hat{X}_i (\omega_1,\omega_2,\cdots ,\omega_N)=\hat{X}(\omega_i) \tag{i=1,...,N}$$

**central limit theorem**

$\hat{X}_1,\hat{X}_2,\cdots ,\hat{X}_N$ are independent identically distributed (iid) RVs with mean $\mu$ and variance $\sigma^2$.Then $p(\hat{S}=s)$ can represent normal distribution with mean $\mu$ and variance $\sigma^2/N$

$$\hat{S} = \frac 1 N \sum_{i=1}^N X_i(\omega)\\
p(\hat{S}=s)\stackrel{N\rightarrow \infty}{\longrightarrow} \frac{1}{\sqrt {2\pi\sigma^2/N}}e^{-\frac{(s-\mu)^2}{2\sigma^2/N}}$$

The more experiments have been done, the smaller the standard deviation $\sqrt{\sigma^2/N}$. The center (mean) doesn't relate with the number of experiments. s can have more variables than $\omega$ (e.g. $\omega$ can only be 0 or 1, the s can be any real number in [0,1].) So here we use probability density p instead of probability of a certain number.

# Statistical Mechanics

classical: gaseous atoms in a cubic box with length of L. what should to know to describe this system (N atoms)? 

positions: ${\vec r}_1,{\vec r}_2,\cdots ,{\vec r}_N$ and momentums: ${\vec p}_1,{\vec p}_2,\cdots,{\vec p}_N$. Each r and p contains three elements (x,y,z). so microstate $\omega=({\vec r}_1,{\vec r}_2,\cdots ,{\vec r}_N;{\vec p}_1,{\vec p}_2,\cdots,{\vec p}_N)$ contains 6N elements. $\Omega$ : all positions of N atoms and their momentum, i.e. $\Omega = \{({\vec r}_1,{\vec r}_2,\cdots ,{\vec r}_N;{\vec p}_1,{\vec p}_2,\cdots,{\vec p}_N)\} = \{(\vec r^N;\vec p^N)\}$ whose size is $[0,L]^{3N}\times \bf{R}^{3N}$

## 1. Microcanonical ensemble (NVE)
- specify number of atoms, volume of box, and energy of all atoms; contains possible micro-states with same N, V and E
- probability density of all these states:
  - $p(\vec r^N,\vec p^N)=\frac {\delta (\hat H (\vec r ^N, \vec p ^N)-E)}{\int_{d\vec r,d\vec p}\delta (\hat H (\vec r ^N, \vec p ^N)-E)}$
  - only microstates with energy equals E can occur
  - one trick here is p only relates with one micro-state, while the right hand side depends on all micro-states
## 2. Canonical ensemble (NVT)
- contains possible micro-states with same N, V and T(temperature)
- probability density:
  - $p(\vec r^N,\vec p^N)=\frac{e^{-\hat H(\vec r^N, \vec p^N)/(k_BT)}}{\int_{d\vec r^Nd\vec p^N}e^{-\hat H(\vec r^N, \vec p^N)/(k_BT)}}$
  - microstates with lower energy are more likely to exist
- partition function $Q=\frac 1 {h^{3N}N!}\int_{d\vec r^Nd\vec p^N}e^{-\hat H(\vec r^N, \vec p^N)/(k_BT)}$
  - N!: for degeneracy; h for unit
  - Q is important since it connects mechanics with thermo-chemistry
  - free energy can be got from it: $F(N,V,T)=-k_BT\ln Q$
- If $\hat X$ is an observable RV
  $$< \hat X> = \int_{d\vec r^Nd\vec p^N}\hat X(\vec r^N,\vec p^N)p(\vec r^N,\vec p^N) \\
  = \frac{\int_{d\vec r^Nd\vec p^N}\hat X(\vec r^N,\vec p^N)e^{-\hat H(\vec r^N, \vec p^N)/(k_BT)}}{\int_{d\vec r^Nd\vec p^N}e^{-\hat H(\vec r^N, \vec p^N)/(k_BT)}}$$

  Typically, energy consists of two part: potential energy and kinetic energy: $\hat H(\vec r^N,\vec p^N) = U(\vec r^N)+E_{kin}(\vec p^N)$. If $\hat X$ only depends on $\vec r^N$, not on $\vec p^N$. So,
    $$<\hat X> = \frac{\int_{d\vec r^N}\hat X(\vec r^N)e^{-\frac{U(\vec r^N)}{k_BT}}\int_{d\vec p^N} e^{-\frac{E_{kin}(\vec p^N)}{k_BT}}}{\int_{d\vec r^N}e^{-\frac{U(\vec r^N)}{k_BT}}\int_{d\vec p^N} e^{-\frac{E_{kin}(\vec p^N)}{k_BT}}}$$

## Ergodieity Hypothesis for $<\hat X>$

The intergrient is complicated and hard to calculate for the average of observable random variable. So **Ergodieity hypothesis** comes up: time average can substitute ensemble average. But it can break, e.g. 2 big balls in a narrow box: time average only has ball 1 at the left/right side of ball 2; while both can exist for ensemble average. 

$$<\hat X> = \lim _{\tau\rightarrow \infty}\frac 1 \tau \int_0^\tau \hat X(\vec r^N(t),\vec p^N(t)) \text{d}t$$

Here comes a question: how long is long enough? It depends on different system and we don't want to wait forever. Another question is to create a trajectory $\hat X$

### Newtonian Dynamics

$$\begin{aligned}
\vec a &= \frac {\vec F} m  &\vec F = -\vec \nabla U(\vec r) \\
\vec a &= \frac {d\vec v}{dt} = \frac {d^2 \vec r}{d t^2}= \dot {\vec v} = \ddot{\vec r}
\end{aligned}$$

We are looking for $\vec r(t),\vec p(t)$ given $\vec r(0),\vec p(0)$, but it's hard. One thing is we can generate Taylor expansion:

$$\vec r (t+\Delta t) = \vec r(t)+\Delta t \dot {\vec r}(t) +\frac 1 2 (\Delta t)^2 \ddot {\vec r}(t) +\frac 1 6 (\Delta t)^3 \vec r'''(t) + \cdots \tag{1}$$

But we don't want to include infinity terms, so **Euler method**: truncate at the second direvatives with error $O(\Delta t^3)$.

$$\vec r (t+\Delta t) = \vec r(t)+\Delta t \dot {\vec r}(t) +\frac 1 2 (\Delta t)^2 \ddot {\vec r}(t) \tag{2}$$

What else can do is to do Taylor expansion in the backward of time:

$$\vec r (t-\Delta t)=\vec r (t)-\Delta t \dot {\vec r}(t) +\frac 1 2 (\Delta t)^2 \ddot {\vec r}(t) -\frac 1 6 (\Delta t)^3 \vec r'''(t) + \cdots \tag{3}$$

add equation (1) and (3),

$$\vec r (t+\Delta t)+\vec r (t-\Delta t)=2\vec r(t)+(\Delta t)^2\ddot {\vec r}(t)+ O(\Delta t^4)$$

**Verlet algorithm** with Error $O(\Delta t^4)$

$$\vec r (t+\Delta t)=2\vec r(t)-\vec r (t-\Delta t)+(\Delta t)^2\ddot {\vec r}(t) \tag{4}$$

HW: Velocity Verlet algorithm

## Miss 1

## Miss 2


## April 17

- 1 point in space: 

  $$\begin{aligned}
  \omega_1^{(1)}(\vec r) &= \text{prob dens that atom 1 is at $\vec r$}\\
  &= <\delta (\vec r_1 -\vec r)> \\
  &= \frac {\int d\vec r^N d\vec p^N \delta (\vec r_1 -\vec r)e^{-\beta H}}{\int d\vec r^N d\vec p^Ne^{-\beta H}}\\
  &= \frac{\int d\vec r_1\vec r_2\cdots d\vec r_N \delta (\vec r_1 -\vec r)e^{-\beta U(\vec r_1,\vec r_2,\cdots,\vec r_N)}}{\int d\vec r_1\vec r_2\cdots d\vec r_N e^{-\beta U(\vec r_1,\vec r_2,\cdots,\vec r_N)}}\\
  &= \frac{\int d\vec r_2\cdots d\vec r_N  e^{-\beta U(\vec r,\vec r_2,\cdots,\vec r_N)}}{\int d\vec r^N  e^{-\beta U}}\\

  \omega_2^{(1)}(\vec r)&=<\delta (\vec r_2 -\vec r)>=\omega_1^{(1)}(\vec r) \text{ independent of atom index}\\

  \rho^{(1)}(\vec r) &= N\cdot \omega^{(1)}(\vec r) \text{ Avg number density at }\vec r\\

  \int d\vec r \rho (\vec r) &= N \text{ if the system is translationally invariant}\\
   \rho^{(1)}(\vec r) &= const. = \frac N V = \rho
  \end{aligned}
  $$

- Make it more interesting, 2 points in space:

  $$
  \omega_{1,2}^{(2)}(\vec r,\vec r') = \text{pro dens that atom 1 is at $\vec r$ and atom 2 is at $\vec r'$}\\
  = <\delta (\vec r_1-\vec r)\delta(\vec r_2-\vec r')>$$

  $$
  \int d\vec r\int d\vec r' \omega_{1,2}^{(2)}(\vec r,\vec r') =1
  $$

  This is independent of which atom pair you choose $\omega^{(2)}(\vec r,\vec r')$

  $$\rho^{(2)}(\vec r,\vec r')=N(N-1)\omega^{(2)}(\vec r,\vec r')$$

- Pair correlation function:
  $$g(\vec r,\vec r' )= \frac{\rho^{(2)}(\vec r,\vec r')}{\rho^{(1)}(\vec r)\rho^{(2)}(\vec r')}$$
  If the system is translationally invariant (i.e. same everywhere) and also isotropic:   
  $$g(\vec r,\vec r') = g(|\vec r' -\vec r|)$$

Why it is interesting? it is enough to calculate some expectations:

- example: calculate potential energy $<U>$
  $$U(\vec r_1,\cdots,\vec r_N) = \sum_{i=1}^{N-1}\sum_{j=i+1}^N u(\vec r_i,\vec r_j)$$

  $$
  \begin{aligned}
  <U> &=\sum_{i<j}<u(\vec r_i,\vec r_j)> \\
  &= \frac {N(N-1)}{2}<u(\vec r_1,\vec r_2)> \text{ if all atoms same}\\
  &=\frac{N(N-1)} 2 \frac{\int d\vec r_1,d\vec r_2,\cdots,d\vec r_N u(\vec r_1,\vec r_2)e^{-\beta U}}{\int d\vec r^N e^{\beta U}}\\
  &= \frac{N(N-1)} 2 \frac{\int d\vec r_1d\vec r_2 u(\vec r_1,\vec r_2)\int d\vec r_3\cdots d\vec r_N e^{-\beta U}}{\int d\vec r^N e^{\beta U}}\\
  &= \frac{N(N-1)} 2 \int d\vec r_1d\vec r_2 u(\vec r_1,\vec r_2)\rho^{(2)}(\vec r_1,\vec r_2)\\
  & = \frac 1 2 \rho^2\int d\vec r_1 d\vec r_2 u(\vec r_1,\vec r_2)g(|\vec r' -\vec r|)\\
  & \overset{\vec s = \vec r_2=\vec r_1}{=} \frac 1 2 \rho^2\int d\vec r_1 d\vec s u(|\vec s|)g(|\vec s|)\\
  &= \frac 1 2 \rho^2 V \int_0^\infty ds s^2\int_0^\pi d\theta sin\theta \int_0^{2\pi}d\phi u(s)g(s)\\
  &= 2\pi \frac {N^2} V\int_0^\infty ds s^2 u(s)g(s)
  \end{aligned}
  $$

  g(s) is the how atoms correlate in the sample (structure), u(s) is pair potential.

## Correlation function

So,

$$<U> = 2\pi \frac {N^2} V\int_0^\infty dr r^2 u(r)g(r)\\
g(\vec r,\vec r') = \frac {\rho^{(2)}(\vec r,\vec r')}{\rho^{(1)}(\vec r)\rho^{(1)}(\vec r')}$$

If homogeneous, $\rho^{(1)}(\vec r) = frac N V = \rho$

$$\begin{aligned}
g(\vec r,\vec r') &= g(|\vec r'-\vec r|)\\
\rho g(\vec r,\vec r') &= \frac {N(N-1)\omega^{(2)}(\vec r, 
\vec r')}{N\omega^{(1)}(\vec r)}\\
&= (N-1)\frac {<\delta (\vec r_1-\vec r)\delta (\vec r_2 - \vec r')>}{<\delta (\vec r_1 -\vec r)>}\\
&= (N-1) \frac {\text{Prob does that atom a at $\vec r$ and atom 2 at $\vec r'$}}{\text{Prob does that atom 1 at $\vec r$}}\\
&= (N-1) \text{Prob(atom 2 at $\vec r'$ | atom a at $\vec r$)}\\
&= \text{Avg density at $\vec r'$ given that atom 1 at $\vec r$}
\end{aligned}$$

$$g(\vec O,\vec r') = g(|\vec r'|)= \text{Avg density at $\vec r'$ given that there is an atom at the origin}$$

- What is the density of the quantum space? N/V
- What is the density here given that an atom is at another point? the probability at that point is 0.

What does $g(r)$ look like?

1. Ideal gas: no interaction, 2 atoms are independent
  - g(r) = 1, means no correlation
2. Solid: g(r) only has sharp peak at distince at $d, \sqrt 2d, 2d, \cdots$, if the origin is at one solid atom.
  $$\begin{aligned}
  \bullet\underline{ d }\bullet\underline{ d }\bullet\underline{ d }\bullet \\
  \bullet\underline{ d }\bullet\underline{ d }\bullet\underline{ d }\bullet \\
  \bullet\underline{ d }\bullet\underline{ d }\bullet\underline{ d }\bullet \\
  \bullet\underline{ d }\bullet\underline{ d }\bullet\underline{ d }\bullet
  \end{aligned}
  $$

3. liquid: dense, atoms touch each other but no order. If set the position of one atom is origin, and the distance between it and its neighboring atom centers is $\sigma$. So,
   $$g(r)=\begin{cases} 0 &r<\sigma\\
   \approx 2 &r=\sigma &\text{1st solution shell}\\
   1-2 &r=2\sigma &\text{2nd}\\
    >1 &r=3\sigma &\text{3rd}\\
    1 &r>3\sigma\end{cases}$$

## pressure

$\Lambda$ is deBroglie wavelength

$$p=-\left.\frac{\partial F}{\partial N}\right|_{N,T}\\
Q = \frac 1 {h^{3N}N!}\int d\vec r^N d\vec p^N e^{-\beta \hat H} = \frac {\int d\vec r^N e^{-\beta U}}{N!\Lambda^{3N}}\\
F(N,V,T) = -k_B T \ln Q(N,V,T)$$