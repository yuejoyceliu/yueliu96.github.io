---
title: Scientific Computing
date: 2019-01-02 13:28:18
tags:
- AMATH
categories:
- NoteBook
---

*A manual for individual use, which focuses on how to solve ordinary and partial differential equation numerically, including how to solve initial value problem with Euler, 2nd- and 4th- order Runge-Kutta and Adams-Bashford method; how to handle boundary value problem with shooting method and direct method and how to deal with PDE with finite difference schemes and spectral methods. Quantum Harmonic Oscillator, Vorticity-Streamfunction Equations, Reaction-Diffusion Systems are are discussed.*

# Initial Value Problem

$$
\frac{d\overrightarrow{y}}{dt}=f(t,\overrightarrow{y}) \quad \overrightarrow{y}(0)=\overrightarrow{y_0} \quad t\in[0,T]
$$

## Forward Euler Method

This is the simplest algorithm for solving this problem, which is derived from the definition of the derivative:

$$
\frac{d\overrightarrow y}{dt}=\lim_{\Delta t \to 0} \frac{\Delta\overrightarrow y}{\Delta t} \approx \frac{\overrightarrow y_{n+1}-\overrightarrow y_n}{t_{n+1}-t_n}
$$

From the above equation, we can get:

$$
\overrightarrow{y}_{n+1} = \overrightarrow y_n + \Delta t \cdot f(t_n,\overrightarrow y_n)
$$

Note that each subsequenct approximation in Euler Method is generated from the slope of the previous point. Considering the error coulde be very large, we need to find some ways to improve it.

## Improved from Euler Method

 One way we can think of is to use the slope of other points instead of that of the previous one to predict the next point. For example, the average slope (Heun's Method), or the slope of the midpoint (RK2).
 
### Heun's 
  
  $$y_{n+1}=y_n+\frac{\Delta t}{2}[f(t_n,y_n)+f(t_{n+1},y_{n+1})]$$

### RK2 
  
  $$y_{n+1}=y_n+\Delta t \cdot f[t_n+\frac{\Delta t}{2},y(t_n+\frac{\Delta t}{2})]$$

### In general 
  
  $$y_{n+1}=y_n+\Delta t[A \cdot f(t_n,y_n)+B \cdot f(t+P\Delta t,y_n+Q\Delta t \cdot f(t_n,y_n)]\\where\quad A+B=1\quad B\cdot P=\frac{1}{2}\quad B\cdot Q=\frac{1}{2}$$

- If $A=\frac{1}{2}\Rightarrow B=\frac{1}{2}\Rightarrow P=1\Rightarrow Q=1\Rightarrow$Heun's Method
- If $A=0\Rightarrow B=0\Rightarrow P=\frac{1}{2}\Rightarrow Q=\frac{1}{2}\Rightarrow$RK2 Method
  
### RK4
  
$$y_{n+1}=y_n+\frac{\Delta t}{6}(f_1+2f_2+2f_3+f_4)\\
f_1=f(t_n,y_n)\\
f_2=f(t_n+\frac{\Delta t}{2},y_n+\frac{\Delta t}{2}\cdot f_1)\\
f_3=f(t_n+\frac{\Delta t}{2},y_n+\frac{\Delta t}{2}\cdot f_2)\\
f_4=f(t_n+\frac{\Delta t}{2},y_n+\frac{\Delta t}{2}\cdot f_3)$$

### Summary and Error Analysis

| Scheme | Local Error | Global Error | Matlab | Python
|----|----|----|----|----|
|Forward Euler|$\Delta t^2$|$\Delta t$||
|Heun's/RK2|$\Delta t^3$|$\Delta t^2$|ode23|Method=RK23
|RK4|$\Delta t^5$|$\Delta t^4$|ode45|Method=RK45

The error in numerical algorithm not only comes from the local error (truncated error) in the algorithm iteself, but also arises from round off error since computer can only keep limit digits of number: $Error_{total}=\varepsilon_{round\ off}+\varepsilon_{truncate}$. If the round-off error is dominant, our algorithm can be unstable to be used. That's why Backward Euler Method is introduced.

## Backward Euler Method

It is an implicit method, which is more stable

$$y_n=y_{n+1}-\Delta t \cdot f(t_{n+1},y_{n+1})$$

Example:

$$\frac{dy}{dt}=\lambda y\quad y(0)=y_0$$

- FE:
  $$y_{n+1}=y_n+\Delta t \cdot f(t_n,y_n)=y_n+\Delta t \cdot \lambda y \Rightarrow y_n=(y_0+\varepsilon_{round\_off})(1+\Delta t \lambda)^N$$
  set  $r_{FE}=(1+\Delta t \lambda)^N\Rightarrow y_n=y_0\cdot r_{FE}^N+\varepsilon_{round\_off}\cdot r_{FE}^N$
  
  - $\lambda>0\Rightarrow |r_{FE}|>1\Rightarrow$ unconditionally unstable
  - $\lambda<0\Rightarrow |r_{FE}|<1\Rightarrow \begin{cases} \Delta t<\frac{2}{|\lambda|} & stable\\ \Delta t>\frac{2}{|\lambda|} & unsatble\\ \end{cases}$
  
- BE:
  
  $$y_n=y_{n+1}-\Delta t\cdot \lambda\cdot y_{n+1}\Rightarrow y_{n+1}=r_{BE}\cdot y_n,\ where\ r_{BE}=\frac{1}{1-\Delta t\lambda}
  \\y_n=y_0\cdot r_{BE}^N+\varepsilon_{round\_off}\cdot r_{BE}^N$$
    - $\lambda<0\Rightarrow |r_{FE}|<1\Rightarrow$ unconditionally stable
    - $\lambda>0\Rightarrow |r_{FE}|<1\Rightarrow \begin{cases} \Delta t>\frac{2}{|\lambda|} & stable\\ \Delta t<\frac{2}{|\lambda|} & unsatble\\ \end{cases}$
 
## MultiStep Method

 - Adams-Bash forth (explicit method)
  $$y_{n+1}=y_n+\frac{\Delta t}{2}(3f_n-f_{n-1})$$ 
 - Adams-Moulthon (implicit method)
  $$y_{n+1}=y_n+\frac{\Delta t}{2}(f_{n+1}+f_n)$$
 - Predictor-Corrector
  $$y_{n+1}^P=y_n+\frac{\Delta t}{2}(3f_n-f_{n-1})\\y_{n+1}=y_n+\frac{\Delta t}{2}[f(t_{n+1},y_{n+1}^P)+f_n]$$

## Matlab for ODE45

solve this equation $\frac{d^2y(t)}{dt^2}+\epsilon[y^2(t)-1]\frac{dy(t)}{dt}+y(t)=0$ with $\epsilon$=0.1, t=[0:0.5:32], y(t=0)=$\sqrt 3$ and $\frac{dy(t=0)}{dt}$=1 by ode45 method.

```
function f = fvdposc(t,y,epsilon)
f1 = y(2);                          %f1=y'
f2 = -epsilon*(y(1)^2-1)*y(2)-y(1);%f2=y''
f = [f1;f2];    %f must be a column vector	
```

```
abstol=10^-6;reltol=10^-6;
options = odeset('AbsTol',abstol,'RelTol',reltol);
%if options not specified, use the default one. the other items must be there.
[T,Y] = ode45( @(t,y) fvdposc(t,y,epsilon),tspan,y0,options);
```

In this way, we can get Y is a [65 $\times$ 2] matrix. This first column is the y values in tspan, and the other columne is y' values in tspan.


# Boundary Value Problem

There might be multiple solutions to this kind of problem, and we should choose those suit boundary conditions. Let's start with a simple case:

$$
\frac{d^2y}{dt^2} = f(t,y,\frac{dy}{dt})\quad y(a) = \alpha\quad y(b) = \beta
$$

## Shooting Method

Actually, BVP is  comparable to IVP:

-    IVP: y(a)=$\alpha$, y'(a)=A
-    BVP: y(a)=$\alpha$, y(b)=$\beta$

So we can guess an initial condition to see how difference the result from the other boundary value; and decide a new initial guess to repeat the above process until the result reaches the other boundary value.

## Direct-Linear BVP

Here we can consider a general case:

$$
\frac{d^2y}{dt^2}=p(t)\frac{dy}{dt}+q(t)y+r(t)\\
\alpha_1y(a)+\beta_1y'(a)=\gamma_1\\
\alpha_2y(b)+\beta_2y'(b)=\gamma_2
$$

Combine Taylor series and central difference method $y'=\frac{y(t+\Delta t)-y(t-\Delta t)}{2\Delta t}+O(\Delta t^2)$, we can get $y''=\frac{y(t+\Delta t)-2y(t)+y(t-\Delta t)}{\Delta t^2}+O(\Delta t^2)$. Finally, we can get: 

$$[1-\frac{p(t)\Delta t}{2}]\cdot y(t+\Delta t)-[2+q(t)\Delta t^2]\cdot y(t)+[1+\frac{p(t)\Delta t}{2}]\cdot y(t-\Delta t)=r(t)\Delta t^2$$

Convert it in to matrix form:

$$A\times \overrightarrow x = \overrightarrow b$$

$$ \begin{pmatrix} 1 & 0 &\cdots &\cdots &\cdots & 0 \\ a & b & c & 0 &\cdots &0 \\0&a&b&c&\cdots&0\\\vdots&\ddots&\ddots&\ddots&\ddots&\vdots\\\vdots&\ddots&\ddots&a&b&c\\0&\cdots&\cdots&\cdots&a&1 \end{pmatrix} \times \begin{pmatrix}y(t_0)\\y(t+\Delta t)\\y(t+2\Delta t)\\\vdots\\\vdots\\y(t_N) \end{pmatrix}=\begin{pmatrix} \alpha\\r(t+\Delta t)\Delta t^2\\ r(t+2\Delta t)\Delta t^2\\\vdots\\\vdots\\\beta \end{pmatrix}$$

In Matlab, we can use function `X=A\b` or `eig(A)` to solve it; in python(numpy), function `linalg.solve(A,b)` or `eig(A)` also works.

## Newton-Raphson Method

One thing must be noted that, initial guess for this method should be close to the real value, otherwise it may diverge.
$$x_{n+1}=x_n-\frac{f(x_n)}{f'(x_n)}$$

## Summary

1. Approximate y', y'' using central difference formula;
2. Approximate boundary condition using FDF, DBF
3. Solve $A\overrightarrow x=\overrightarrow b$
4. solution--O($\Delta t^2$)

## Quantum Harmonic Oscillation

$$\frac{d^2\phi_n}{dx^2}-[Kx^2-\varepsilon_n]\phi_n=0$$
we expect the solution $\phi_n(x)\rightarrow 0$ as $x\rightarrow \pm \infty$ and $\varepsilon_n>0$ is the quantum energy. Note that $K=km/\hbar^2$ and $\varepsilon_n=E_nm/\hbar^2$. Here take K=1, and always normalize so that $\int_{-\infty} ^{+\infty} {|\phi_n|^2} \,{\rm d}x=1$. Calculate the first five normalized eigenfunctions ($\phi_n$) and eigenvalues($\varepsilon_n$) up to tolerance of $10^{-4}$ in increasing order such that the first eigenvalue is the lowest one.

- Shooting method

```
function f=pdefunc(x,y,e)

f1 = y(2);
f2 = (x^2-e)*y(1);

f = [f1;f2];
```

```
L=4; dx=0.1; e_start=0.5; tol=10^-4;

xspan = -L:dx:L;
A = 1; % suggest A=phi(-L)=phi(L)

for modes=1:5
    e = e_start;
    de=0.01;
    for j=1:1000
        y0 = [A;A*sqrt(L^2-e)];
        
        [x,phi] = ode45( @(x,phi) pdefunc(x,phi,e), xspan ,y0);
        
        rightbc = phi(end,2)+sqrt(L^2-e)*phi(end,1);
        if abs(rightbc)<tol
            eigen_e(modes,1)=e;
            break;
        end
        
        if (-1)^(1+modes)*rightbc>0
            e = e+de;
        else
            de = de/2;
            e = e-de;
        end
    end
    eigen_phi(:,modes) = phi(:,1)/sqrt(trapz(x,phi(:,1).^2));
        e_start = e+0.2;
end

%eigen_phi,eigen_e are what we want
```

- Direct Method

```
L=4; dx=0.1; 
xspan = -L:dx:L;
max = length(xspan)-2;
A = zeros(max,max);
phi_sort = zeros(max+2,max+2);
% build up A matrix which doesn't consider phi(x1) and phi(xn). A is built
% based on 2nd order central difference. The first and last row don't
% consider x1 and xn, use FDF and BDF and approximation to make phi(x2) and
% phi(x3) express phi(x1); phi(xn-2) and phi(xn-1) express phi(xn).
A(1,1:2) = [2/3/dx^2+xspan(2)^2,-2/3/dx^2];
A(end,end-1:end) = [-2/3/dx^2,2/3/dx^2+xspan(end-1)^2];
i = 2;
while i<max
    A(i,i-1) = -1/dx^2;
    A(i,i+1) = -1/dx^2;
    A(i,i) = 2/dx^2+xspan(i+1)^2;
    i=i+1;
end
%phi function only contains [phi(2),phi(3),...phi(n-2),phi(n-1)]
[phi,e]=eig(A);

%sort phi function based on ascending energy.
for i=1:max
    eng(i,1) = e(i,i);
end

[eng, Index_eng] = sort(eng);

%only get the first five phi functions. 
%phi(1)/phi(N) are calculated based on FDF/BDF method without approximation.
for i =1:5
    phi_sort(2:end-1,i) = phi(:,Index_eng(i));
    phi_sort(1,i) = (4*phi_sort(2,i)-phi_sort(3,i))/(3+2*dx*sqrt(L^2-eng(i)));
    phi_sort(end,i) = (4*phi_sort(end-1,i)-phi_sort(end-2,i))/(3+2*dx*sqrt(L^2-eng(i)));
    phi_sort(:,i) = phi_sort(:,i)/sqrt(trapz(xspan,phi_sort(:,i).^2));
end

%phi_sort,eng is the result
```

- Shooting for nonlinear cases
  
$$\frac{d^2\phi_n}{dx^2}-[\gamma |\phi_n|^2+Kx^2-\varepsilon_n]\phi_n=0$$\

Still use $x\in [-L,L]$ with L=2 and choose xspan = -L:0.1:L. Find the first two normalized modes for  $\gamma=0.05$:

```
L=2; dx=0.1; e_start=0.5; tol=10^-4; gama=0.05; A_start=0.2;
xspan = -L:dx:L;

for modes=1:2
    e = e_start;
    de=0.01;
    for j=1:1000
        A = A_start;
        dA = 0.1;
        for a=1:1000
            y0 = [A;A*sqrt(L^2-e)];
            
            [x,phi] = ode45( @(x,phi) nolinpdefunc(x,phi,gama,e), xspan ,y0);
         
            AA = trapz(x,phi(:,1).^2);
           
            if abs(AA-1)<tol
                opt_A(modes,1)=A;
                break;
            end
            if AA>1
                A = A-dA;
            else
                dA = dA/2;
                A = A+dA;
            end       
        end
        
        rightbc = phi(end,2)+sqrt(L^2-e)*phi(end,1);
        if abs(rightbc)<tol
            eigen_e(modes,1)=e;
            break;
        end
        
        if (-1)^(1+modes)*rightbc>0
            e = e+de;
        else
            de = de/2;
            e = e-de;
        end
    end
    e_start = e+1;
    A_start = A+1;
    eigen_phi(:,modes) = phi(:,1)/sqrt(trapz(x,phi(:,1).^2));    
end
```

# Partial Differential Equations

Solving PDE is harder than ODE, because we need to consider both initial conditions and boundary conditions, also need to solve both in time and in space. The classic PDE is vortivity-streamfunction equations and reaction-diffusion systems. We will go through these two systems to show how to slove PDE.

## Finite Scheme Method for Vorticity-Streamfunction Equations

$$\omega_t+[\psi,\omega]=\mu\nabla^2\psi\quad \nabla^2\psi=\omega\\
where\; [\psi,\omega]=\psi_x\omega_y-\psi_y\omega_x \; and \; \nabla^2=\partial_x^2+\partial_y^2$$

- Steps:
 1. Elliptic Solve: given $\omega_0 \rightarrow$ compute $\psi_0$ by using $ \nabla^2\psi=\omega$
 2. Time-Stepping: choose step $\Delta t$ compute $\omega '$ using $\omega_{k+1}=\omega_k+\Delta t\cdot f(\psi^k,\omega^k)$
 3. Iterate

- Step 1: the elliptic problem
$$(\psi_{mn})_{xx}+(\psi_{mn})_{yy}=\omega_{mn}$$
By using CDF:
$$\frac{\psi_{m-1,n}-2\psi_{m,n}+\psi_{m+1,n}}{\Delta x^2}+\frac{\psi_{m,n-1}-2\psi_{m,n}+\psi_{m,n+1}}{\Delta y^2}=\omega_{m,n}\delta^2$$
If we set $\Delta x=\Delta y$, and reshape the matrix $\psi_{m,n}$ and $\omega_{m,n}$ (m=n)to vectors (the same thing as matlab fucntion `reshape(matrix,n^2,1)`), we can write the above equation into a matrix form:
$$A\overrightarrow \psi = \overrightarrow \omega $$
where $A=A'/\delta^2$, $A'=A_D+A_x+A_y$, $A_D=-4\psi_{m,n}$, $A_x=\psi_{m-1,n}+\psi_{m,n-1}$ and $A_y=\psi_{m,n-1}+\psi_{m,n+1}$

- *Matlab script*
    
    $A=\nabla^2$, $B=\partial_x$, $C=\partial_y$

```
function [A B C] = derivmatrix(dx,dy,n)

e1 = ones(n^2,1);
%A = dx^2+dy^2

%A = (AD+AX+AY)/dx/dy; AD=-4y(m,n),AX=y(m-1,n)+y(m+1,n), AY=y(m,n-1)+y(m,n+1)
AD = spdiags(-4*e1,0,n^2,n^2); 
AD(1,1)=2;%set the first element not -4 to avoid denominator too small
AX = spdiags([e1 e1 e1 e1],[-(n-1)*n -n n n*(n-1)],n^2,n^2);
AY = spdiags([e1 e1],[-1 1],n^2,n^2);
for i=1:n
    AY(1+n*(i-1),n*i) = 1;
    AY(n*i,1+n*(i-1)) = 1;
    if i<n
        AY(n*i,1+n*i) = 0;
        AY(1+n*i,n*i) = 0;
    end
end
A = (AD+AX+AY)/(dx*dy);

%B = dx
%B = (y(m+1,n)-y(m-1,n))/(2*dx)
B = spdiags([e1 -e1 e1 -e1],[-(n-1)*n -n n n*(n-1)],n^2,n^2)/(2*dx);

%C = dy
%C = (y(m,n+1)-y(m,n-1))/(2*dy)
C = spdiags([-e1 e1],[-1,1],n^2,n^2);
for i=1:n
    C(1+n*(i-1),n*i) = -1;
    C(n*i,1+n*(i-1)) = 1;
    if i<n
        C(n*i,1+n*i) = 0;
        C(1+n*i,n*i) = 0;
    end
end
C = C/(2*dy);
```

then, we could use one of these two method to slove $\psi$

```
psi = A\w;
```

```
 [L,U,P] = lu(A);
 y=L\(P*w);
 psi = U\y;
```

- Step 2: Method Line

$$
\nabla^2\psi(x,y)=f(x,y)\qquad+b.c.\\
u_t(t,x)=u_x(t,x)\quad+i.c.,b.c.\\
u_x(t,x)\approx\frac{u(x+\Delta x)-u(x-\Delta x)}{2\Delta x}
$$
We have to condiser the stability of this method. Choose $\lambda$ carefully to make sure it is stable and also will not run forever.
$$u_n^{(m)}=g^mexp(i\zeta\Delta x)\\
$$\lambda =\frac{\Delta t^{num-t-der}} {\Delta x^{num-x-der}}$$

## Spectral Method for Vorticity-Streamfunction Equations

expand u(x,t):

$$u(x,t)=\sum_{k=1}^N a_k(t)\phi_k(x)\qquad$$
 where $\phi_k(x)$are orthogonal
Using Fourier Series

$$\widehat{u}(t)=u(k,t)=\sum_{n=1}^N u(n,t)e^{-i2\pi(k-1)(n-1)/N}\\\qquad\;u(n,t)=1/N\sum_{n=1}^N \widehat u(t)e^{i2\pi(k-1)(n-1)/N}$$
Derivative property:
$$\widehat u^{(m)}(x,t)=(ik)^{(m)}\widehat u(k,t)$$
PDE  Fourier Space
$$u_t=Lu+N(u) \Longrightarrow \widehat(u)_t=\alpha(k)\widehat u+\widehat N(u)$$
Here attached the script for solve VSE by the above two methods.

```
clear all; clf; close all; clc
nu = 0.001;
n=64;
L=10;
tspan = 0:0.5:4;

w1 = runvs(L,n,tspan,nu,1);

w2 = runvs(L,n,tspan,nu,2);

w3 = runvs(L,n,tspan,nu,3);
```

```
function wfsol = runvs(L,n,tspan,nu,choice)

x2 = linspace(-L/2,L/2,n+1);
x = x2(1:n);
dx = x(2)-x(1);

[X,Y] = meshgrid(x);%grid
[A,B,C] = derivmatrix(dx,dx,n);%apply to vector [64*64,1]

wfinit = exp(-X.^2-Y.^2/20);%grid
wfinitvect = reshape(wfinit,n^2,1);%vector

[t,wfsol] = ode45(@(t,wfvec) vortstream(t,wfvec,n,nu,A,B,C,choice,1),tspan,wfinitvect);

if choice==3
    kx = (2*pi/L)*[0:(n/2-1) (-n/2):-1];
    kx(1) = 1e-6;

    [KX,KY]=meshgrid(kx);
    K = KX.^2+KY.^2;
    
    [t,wfsol] = ode45(@(t,wfvec) vortstream(t,wfvec,n,nu,A,B,C,choice,K)tspan,wfinitvect);
end
```

```
function rhs = vortstream(t,w,n,nu,A,B,C,choice,K)

if choice==1
    psi = A\w;%vector
elseif choice==2
    [L,U,P] = lu(A);
    y=L\(P*w);
    psi = U\y;
else
    wf = fft2(reshape(w,n,n));
    psif = -wf./K;
    psi = reshape(real(ifft2(psif)),n^2,1);
end

rhs = -(B*psi).*(C*w)+(C*psi).*(B*w)+nu*A*w;%vector
```

## Chebishev Polynomials

$$\phi_k(x)=T_k(x)\quad T_k(cos\theta)=cosk\theta$$
Matlab Script:

```
function [D,x] = cheb(N)
  if N==0, D=0; x=1; return, end
  x = cos(pi*(0:N)/N)'; 
  c = [2; ones(N-1,1); 2].*(-1).^(0:N)';
  X = repmat(x,1,N+1);
  dX = X-X';                  
  D  = (c*(1./c)')./(dX+(eye(N+1)));      % off-diagonal entries
  D  = D - diag(sum(D'));                 % diagonal entries
```

Solve reaction-diffusion system with both spectral and cheb methods
$$U_t=\lambda(A)U-\omega (A)V+D_1\nabla^2U\\V_t=\omega (a)U+\lambda(A)V+D_2\nabla^2V$$
where $A^2=U^2+V^2$ and $\nabla^2=\partial_x^2+\partial_y^2$. Consider $\lambda(A)=1-A^2$ and $\omega(A)=-\beta A^2$

```
clear all; close all; clc
L=20;n=64;beta=1;d1=0.1;d2=d1;m=1;
tspan=0:0.5:4;

uv1 = runrds_fft(tspan,L,n,beta,d1,d2,m);
A1 = real(uv1);
A2 = imag(uv1);

n=31;
uv2 = runrds_cheb(tspan,L,n,beta,d1,d2,m);
A3 = uv2;
```
we consider $x,y \in[-10,10]$, n=64, $\beta =1$, $D_1=D_2=0.1$, m=1, tspan=0:0.5:4 and $u_f$ stacked on top of $v_f$.
The following is FFT(spectral) method:

```
function xfsol = runrds_fft(tspan,L,n,beta,d1,d2,m)

x2 = linspace(-L/2,L/2,n+1);
x = x2(1:n);
y=x;

kx = (2*pi/L)*[0:(n/2-1) (-n/2):-1];
kx(1) = 1e-6;
ky=kx;

[X,Y]=meshgrid(x,y);
[KX,KY]=meshgrid(kx,ky);
K = KX.^2+KY.^2;
Kvec = reshape(K,n^2,1);

uint = tanh(sqrt(X.^2+Y.^2)).*cos(m*angle(X+i*Y)-(sqrt(X.^2+Y.^2)));%grid
vint = tanh(sqrt(X.^2+Y.^2)).*sin(m*angle(X+i*Y)-(sqrt(X.^2+Y.^2)));
ufint = fft2(uint);
vfint = fft2(vint);
ufvecint = reshape(ufint,n^2,1);
vfvecint = reshape(vfint,n^2,1);
xfvecint = [ufvecint;vfvecint];

[t,xfsol] = ode45(@(t,xfvec) rds_fft(t,xfvec,beta,Kvec,n,d1,d2),tspan,xfvecint);

```

```
function rhs = rds_fft(t,xfvec,beta,Kvec,n,d1,d2)

ufvec = xfvec(1:n^2);
vfvec = xfvec(n^2+1:end);

u = real(ifft2(reshape(ufvec,n,n)));
v = real(ifft2(reshape(vfvec,n,n)));
A = u.^2+v.^2;
l = 1-A;
w = -beta*A;

uft = reshape(fft2(l.*u-w.*v),n^2,1)-d1*Kvec.*ufvec;
vft = reshape(fft2(w.*u+l.*v),n^2,1)-d2*Kvec.*vfvec;

rhs = [uft;vft];
```

The following is cheb method with n=30 and m=1

```
function xsolvec = runrds_cheb(tspan,L,n,beta,d1,d2,m)

[D,x2] = cheb(n-1);
D2= D^2;
D2(1,:) = zeros(1,n);
D2(n,:) = zeros(1,n);%boundary should be 0
I = eye(length(D2));
Lap = kron(D2,I)+kron(I,D2);

x = x2*L/2;
[X,Y]=meshgrid(x);

uinit = tanh(sqrt(X.^2+Y.^2)).*cos(m*angle(X+i*Y)-(sqrt(X.^2+Y.^2)));%grid
vinit = tanh(sqrt(X.^2+Y.^2)).*sin(m*angle(X+i*Y)-(sqrt(X.^2+Y.^2)));

uvecinit = reshape(uinit,n^2,1);
vvecinit = reshape(vinit,n^2,1);
xvecinit = [uvecinit;vvecinit];

[t,xsolvec] =ode45(@(t,xvec) rds_cheb(t,L,xvec,beta,Lap,n,d1,d2),tspan,xvecinit);

```

```
function rhs = rds_cheb(t,L,xvec,beta,Lap,n,d1,d2)

uvec = xvec(1:n^2);
vvec = xvec(n^2+1:end);

Avec = uvec.^2+vvec.^2;
lvec = 1-Avec;
wvec = -beta*Avec;

ut = lvec.*uvec-wvec.*vvec+d1*4/L^2*Lap*uvec;
vt = wvec.*uvec+lvec.*vvec+d2*4/L^2*Lap*vvec;

rhs = [ut;vt];

```



