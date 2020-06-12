---
layout: article
title: Notes on econometrics
key: 20200612
tags: Economics
pageview: false
mathjax: true
aside:
  toc: true
---


Notes for final exam.

<!--more-->

# Basic Concept

$\{(y_i,x_i), i=1, ..., n\}$

- **Regressand**: $y_i = (y_1, ..., y_n) (n\times 1)$
- **Regressor**: $x_i=(x_{i1}, ..., x_{ip}) (n\times p)$  
- **estimater**:$\beta=(\beta_0, \beta_1,..., \beta_p)(p\times 1)$

$$
\begin{eqnarray*}
y_i&=&\beta_0 + \beta_1x_{i1}+...+\beta_px_{ip}+\epsilon_i \\
    &=&X_i^T\beta + \epsilon_i
\end{eqnarray*}
$$

$$
\begin{equation}\nonumber
    \left(
  \begin{array}{c}
          y_1 \\
          \vdots \\
          y_N
 \end{array}
 \right)=
  \left(
  \begin{array}{ccc}
          x_{11} & \cdots & x_{1P}\\
          \vdots & \ddots & \vdots\\
          x_{N1} & \cdots & x_{NP}
  \end{array}
  \right)
  \left(
  \begin{array}{c}
          \beta_0 \\
          \vdots \\
          \beta_P
 \end{array}
 \right) + 
  \left(
  \begin{array}{c}
          \epsilon_0 \\
          \vdots \\
          \epsilon_N
 \end{array}
 \right)
\end{equation}
$$

## Example: Cross-country growth regression

- $y_i:$ growth rate of GDP in country
- $x_{ij}: P$ different charateristics of country

### Case 1 Traditional Setteing

p << n (# of x << # of y)

### Case 2 Model Setting

p >> n(# of y << # of x)

> $$
> \begin{eqnarray*}
> y_i &=& \beta_0 + \beta_1x_{i1}+...+\beta_{200}x_{i200}+\epsilon_i \\
> \beta&=&(\beta_0,\beta_1,...,\beta_200)^T \\
     &=&(\beta_0,\beta_1,...,\beta_5,0,...,0)^T \\
     n&=&200,p=5 \\
> \end{eqnarray*} 
> $$
> 
> Assume:$\{\beta_j:\beta_j\neq0\}$ << n  
> $$
 \hat{\beta_j}^{Lasso} = \mathop{\arg\min}_{b \in \mathbb{R}} \{\frac{1}{n}\sum_{i=1}^{n}(y_i-x_i^Tb)^2+\lambda\left \|b\right \|\}
 $$
> 
> ex.) x = {3,4}  
> $\quad \quad\left \|x\right \| = |3| + |4| = 7$


# 0. Recal Linear Algebra

## 0.1 Vector Space

- vectors space:  
$\mathbb{R}^n, i.e. \{x=(x_1,...,x^n)^T:x_i \in \mathbb{R },\forall i=1,...,n\}$  
- Addition: for any vector $x=(x_1,...,x_n)^T$ and $y=(y_1,...,y_n)^T$   
$$
\begin{equation}
x+y=(x_1+y_1,x_2+y_2,...,x_n+y_n)^T
\end{equation}
$$
- (Scalor) multiplication: for any $a \in \mathbb{R}$ and $x=(x_1,...,x_n)^T$  
$ax=(ax_1,...,ax_n)^T$

### Def 01 Linear Subset
A subset $w \in \mathbb{R}$ is called a **linear subset** of $\mathbb{R}^n$ if   
$(a)W\neq\varnothing$  
$(b)x,y\in w \Rightarrow x+y \in w$   
$(c)x \in w,a \in w\Rightarrow ax\in w$

> **Example**   
> Consider $\mathbb{R}^2$ with n=2 for any $x \in \mathbb{R}$, the line $w=\{ax,a \in R\}$ is a linear subset of $\mathbb{R}^2$.   

We check (a)-(c):   
$(a)W\neq\varnothing$  
$(b)Let\ y,z \in w$   
$\quad Then\ \exists\ a,b \in \mathbb{R}\ with\ y=ax \in w,z=bx \in w$   
$\quad s.t\ y+z=ax+bx=(a+b)x \in w$   
$(c)Let\ a \in \mathbb{R}, y \in w$   
$\quad Since\ y=bx$   
$Then\ \exists\ a \in \mathbb{R}, s.t.\ ay=(ab)y \in w$

### Def 02 Linear combination