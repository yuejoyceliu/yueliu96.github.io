---
title: Machine Learning on Coursera
date: 2019-04-07 15:17:21
tags:
- MachineLearning
categories:
- NoteBook
---

[This Machine Learning course ](https://www.coursera.org/learn/machine-learning?) is taught by Andrew Ng and offered by Standford University.

# Octave/MatLab Tutorial

## Matrix & Size & Index

```MatLab
A = [1 2 ; 3 4 ; 5 6]
size(A) % ans =  3  2 
size(A,1) % 3
size(A,2) % 2

v = [1 2 3 4]
length(v) % 4
length(A) % 3
length([1;2;3;4;5]) % 5

A(3,2) % 6
A(2,:) % 3 4
A([1 3],:) % 1 2; 5 6
A(:,2) = [10; 11; 12] % 1 10; 3 11; 5 12
A = [A,[100; 101; 102]] % append another column  vector to right
A(:) % put all elements of A into a single vector

A = [1 2 ; 3 4; 5 6];
B = [11 12; 13 14; 15 16];
C = [A B] % [1 2 11 12; 3 4 13 14; 5 6 15 16]
D = [A; B] % [1 2; 3 4; 5 6;11 12; 13 14; 15 15]

A = rand(2); B = rand(2);
C = max(A,B) % C = [max(a11,b11) max(a12,b12);max(a21,b21) max(a22,b22)]
```
## load, save & clear data

```MatLab
pwd %print working directory
cd %change directory
load A1.dat % load data
load('A1.dat') % another way
who % variables in the current scope
whos % details of variables
clear A1 % delete A1.dat
save hello.mat A1 % save A1 to hello.mat file
save hello.txt A1 -ascii % save A1 as text (ASCII) 
```

## computation
- simple arithmetic
```MatLab
A = [1 2; 3 4; 5 6]
B = [11 12; 13 14; 15 16]
C = [1 1; 2 2]
A.*B % [a11*b11 a12*b12; a21*b21 a22*b22; a31*b31 a32*b32]
A.^2 % [1 4; 9 16; 25 36]
1./A % [1 1/2; 1/3 1/4; 1/5 1/6]
A' % [1 3 5; 2 4 6]
(A')' % A
pinv(A) % sudo inverse of A

v= [1; 2; 3]
-v % -1*v [-1;-2;-3]
v+ones(length(v),1) % [2;3;4]
v+1 
```
- max sum & find function
```MatLab
a = [1 15 2 0.5]
val = max(a) % 15
[val, ind] = max(a) % 15 2
max(A) % 5 6
a < 3 % 1 0 1 1
find(a<3) % 1 3 4

magic(N) % N-N matrix who has same diganal sum, horizontal sum and vertical sum
A = magic(3) %[8 1 6; 3 5 7; 4 9 2]
[r,c] = find(A >=7) % r = [1; 3; 2] c = [1; 2; 3]

sum(a) % sum of every elements
prod(a) % 15
floor(a) % [1 15 2 0]
ceil(a) % [1 15 2 1]

max(A) == max(A,[],1) % max(a11,a21) max(a12,a22)
max(A,[],2) % max(a11,a12) max(a21,a22)

sum(A) == sum(A,1) % a11+a21 a12+a22
sum(A,2) % a11+a12 a21+a22
sum(sum(A)) % sum of all elements of A
```

## plot the data

```MatLab
t = [0:0.01:0.98];
y1 = sin(2*pi*4*5);
plot(t,y1);
y2 = cos(2*pi*4*t);
hold on; % plot a new figure on the old one
plot(t,y2.'r'); % red color

xlabel('time')
ylabel('value')
legend('sin','cos')
title('my plot')
cd 'my/directory'; print -dpng 'myplot.png' % save it to a file
close % close the figure

figure(1); plot(t,y1);
figure(2); plot(t,y2); % create 2 figures

subplot(1,2,1); % divides plot a 1x2 grid, access 1st element
plot(t,y1);
subplot(1,2,2); 
plot(t,y2);
axis([0.5 1 -1 1]) % x axis from 0.5 to 1  and y from -1 to 1

A =magic(5)
imagesc(A)
imagesc(A),colorbar, colormap gray;
```

## control statements

```Matlab
for i=1:10, v(i)=2^i; end;

i = 1; while i <=5, v(i)=100; i=i+1; end;

i =1; while true, v(i)=999; i=i+1; if i==6, break; end; end;

if v(1)==1, disp('the value is one.'); elseif v(1)==2, disp('the value is two.'); else, disp('the value isnot 1 or 2.'); end;

addpath('my/directory/of/function') % add this dirctory to search directory; otherwise you should at the directory which contains the external function you want to use
```

## vectorization

$h_\theta (x) = \sum_{j=0}^n \theta_j x_j = \Theta^T x$

simplify `prediction = 0.0; for j = 1:n+1, prediction = prediction + theta(j)*x(j); end;` to `prediction = theta' *x;` by vectorization

# Introduction to Machine Learning

## Definiation

- Arthur Samuel 1959: Machine Learning: Field of study that gives computers the ability to learn without being explicity programmed
- Tom Mitchell 1998: Well-posedLearning Problem: A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E.

## Algorithms

- Supervised learning: "right answers" given
  - regression: predict continuous valued output (e.g. price)
  - classification: dicrete valued output (e.g. 0 or 1)
- Unsupervised learning
- Others:
  - reinforcement learning
  - recommender systems

# Linear Regression with multiple variables

m training examples, n features
- gradient descent
  - needs to choose $\alpha$
  - many iterations
  - works well even when n is large
- normal equation
  - $\alpha$ not need
  - no iterations
  - needs $(X^TX)^{-1}$ ($O(n^3)$)
  - slow if n is very large ($n>10^3$)

## Gradient Descent

- hypothesis: $H_\theta (x) = \Theta^T x = \theta_0 x_0+\theta_1x_1+\theta_2x_2+\cdots +\theta_nx_n$
- parameters: $\Theta: \theta_0,\theta_1,\cdots,\theta_n$
- cost functions: $J(\Theta)=\frac 1 {2m}\sum_{i=1}^m\left(h_\theta(x^{(i)})-y^{(i)}\right)^2$
- gradient descent: repeat $\lbrace \theta_j := \theta_j - \alpha \frac \partial {\partial\theta_j} J(\Theta)\rbrace$ simultaneously update for every j=0,1,...,n; which is $\lbrace \theta_j := \theta_j - \alpha\frac 1 m \sum_{i=1}^m\left(h_\theta (x^{(i)})-y^{(i)}\right)x_j^{(i)}\rbrace$

Useful tricks:

1. feature scaling: $-1\leq x_i \leq 1$ to increase efficiency by $\frac{x_i-\mu_i}{max(x_i)-min(m_i)}$ or $\frac{x_i-\mu_i}{\sqrt{var(x_i)}}$
2. learning rate $\alpha$:
   - too small: always slow convergence
   - too large: $J(\theta)$ mya not decrease on every iteration; may not converge
   - try $\alpha$ from "..., 0.001, 0.003, 0.01, 0.03, 0.1, 0.3, 0,1, ..." to choose

## Normal equation:

The solution to 

$$\mathbf{X}\times \mathbf{\Theta} = \mathbf{y}$$
is 
$$\mathbf{\Theta} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

1. $\mathbf{X}$ is not always invertible
2. What if $\mathbf{X}^T\mathbf{X}$ is non-invertible?
   - redundant features (linearly dependent)
   - too many features (e.g. $m\leq n$)
      - delete some features, or use regularization
3. Octave: `pinv(X'*X)*X'*y`
   - `pinv`:sudo inverse, works for most cases even if X'*X non-invertible  