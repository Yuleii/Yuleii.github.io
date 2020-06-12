---
layout: article
title: Notes on Econometrics
key: 20200612
tags: Economics
modify_date: 2020-06-12
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

$p<<n$ (# of x << # of y)

### Case 2 Model Setting

$p>>n$(# of y << # of x)

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

### Def 0.1 Linear Subset

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

### Def 0.2 Linear Combination

Let $v_1,..,v_d \in \mathbb{R}$ is called a **linear combination** of $v_1,..,v_d$ if there exists constants $a_1,...,a_n\in \mathbb{R}\ s.t.\ v=a_1v_1+...+a_dv_d$.

> **Example**   
> Let $v_1=(1,0,0)^T\in \mathbb{R}^3, v_2=(0,1,0)^T\in \mathbb{R}^3$, for any $a,b\ \in \mathbb{R}$,the vector $v=(a,b,0)^T$ is a linear combination of $v_1$ and $v_2$, since

$$
\begin{equation}\nonumber
  v=a
  \left(
  \begin{array}{c}
          1 \\
          0 \\
          0
 \end{array}
 \right)+b
  \left(
  \begin{array}{c}
          0 \\
          1 \\
          0
 \end{array}
 \right)= 
  \left(
  \begin{array}{c}
          a \\
          b \\
          0
 \end{array}
 \right)
\end{equation}
$$

### Def 0.3 Span

For $v_1,..,v_d \in \mathbb{R}^n$, we call **span**$=\{v_1,..,v_d\}=\{v \in \mathbb{R}^n, v=a_1v_1+...+a_dv_d\}$ the space spanned by the vector $v_1,..,v_d \in \mathbb{R}$. Put differently, span$\{v_1,..,v_d\}$ is the set of linear combination of $v_1,..,v_d$.

> **Example**   
> Let $v_1=(1,0,0)^T\in \mathbb{R}^3, v_2=(0,1,0)^T\in \mathbb{R}^3$

$$
\begin{eqnarray*}
span\{v_1,v_2\}&=&\{v \in \mathbb{R}^3,v=a_1v_1+a_2v_2\} \\
&=&\{v \in \mathbb{R}^3,v=\left(\begin{array}{l}
a \\
b \\
0
\end{array}\right)\}\ for\ some\ a,b \in \mathbb{R}
 \end{eqnarray*} 
$$

### Lemma 0.4 Linear Subspace

For any $v_1,..,v_d \in \mathbb{R}^n$, span$=\{v_1,..,v_d\}$ is a **linear subspace** of  $\mathbb{R}^n$.

### Def 0.5 Linear Independence

- The vector $v_1,..,v_d \in \mathbb{R}^n$ are called **linearly independent** of for any $a_1,..,a_d \in \mathbb{R}$ with $a_1v_1+...+a_dv_d=0$, it holds that $a_1=...=a_d=0$.
- If there exists $a_1,..,a_d \in \mathbb{R}$ with $a_i \neq 0$ for some i and $a_1v_1+...+a_dv_d=0$, we say that $v_1,..,v_d$ are **linearly dependent**.

### Remark 0.6 Linear dependence & Linear Combination

$v_1,..,v_d$ **linearly dependent** $\Longleftrightarrow$   
some vector can be written as a linear combination of the other vectors   
$v_1,..,v_d$ **linearly dependent** $\Longleftrightarrow$  
none of the vectors $v_i$ can be written as a linear combination of the other vectors.   

> **Example**
> The vectors $v_1=
\left(\begin{array}{l}
1 \\
0 
\end{array}\right),v_2=
\left(\begin{array}{l}
1 \\
1 
\end{array}\right)$ are linearly independent.

$$
\nonumber
av_1+bv_2=
\left(\begin{array}{l}
a \\
0
\end{array}\right)+
\left(\begin{array}{l}
b \\
b
\end{array}\right)=
\left(\begin{array}{c}
a+b \\
b
\end{array}\right)=0 
\Longleftrightarrow
a=b=0
$$

### Def 0.7 Generating System & Basis

- A family of vector $B=\{v_1,..,v_d\}$ is a **generating system** of $\mathbb{R}$ if $\mathbb{R}^n=span\{v_1,..,v_d\}$.
- A family of vector $B=\{v_1,..,v_d\}$ is a **basis** of $\mathbb{R}$ if B is a **generating system** of $\mathbb{R}$ and that vectors v_1,..,v_d are **linearly dependent**.

### Remark 0.8 Length

- let $B=\{v_1,..,v_d\}$ be a **generating system** in $\mathbb{R}^n$, then $d>>n$
- let $B=\{v_1,..,v_d\}$ be a **basis** in $\mathbb{R}^n$, then $d=n$
That is, every basis of $\mathbb{R}^n$ has length(dimension).

### Def 0.9 Equivalent statement of generating system

Let $B=\{v_1,..,v_d\}$ be a family of vectors in $\mathbb{R}^n$. The following statement are equivalent:   
- B is a **basis** in $\mathbb{R}^n$.
- B is a **generating system** of $\mathbb{R}^n$ that can be standard. That is, for any $i,\{v_1,..,v_{i-1},v_{i+1},...,v_d\}$ is not a **generating system** of $\mathbb{R}^n$.
- for any $v \in \mathbb{R}^n$, there exists unique constant $a_1,..,a_d \in \mathbb{R}, s.t\ v=a_1v_1+...+a_dv_d$.
- B is a maximun **linear independent system**. That is, for any $v \in \mathbb{R}^n,v_1,v_1..,v_d$ are not **linear independent**.

### Prop 0.10 Basis in linearly independent vectors

Let $v_1,..,v_d \in \mathbb{R}^n$ **linearly independent** vectors with $d<n$. Then we can find $v_{d+1},...,v_n \in \mathbb{R}^n\ s.t\ B=\{v_1,..,v_d\}$ is a **basis** of $\mathbb{R}^n$.


## 0.2 Linear Mappings and Matrix

### Def 0.10 Linearly Mapping

A function $F:\mathbb{R}^n \to \mathbb{R}^p$ is called a **liearly mapping** if for all$v,w \in \mathbb{R}^n$ and $a \in \mathbb{R}$:
$(i)\ F(v+w)=F(v)+F(w)$
$(ii)\ F(av)=aF(v) $

### Prop 0.11 Linear mapping represented by matrix

For **linear mapping** $F:\mathbb{R}^n \to \mathbb{R}^p$, there exists a unique matrix $A \in \mathbb{R}^{p \times n}\ s.t\ F(x)=A(x)$ for all $x \in \mathbb{R}^n$.

### Remark 0.12 Linear Mapping & Basis

Let $\{v_1,..,v_d\}$ be a **basis** of $\mathbb{R}$ and $F,G:\mathbb{R}^n \to \mathbb{R}^p$ two **linear mappngs** with$F(v_1) \to G(v_1),\ v_1=1,...,n$. Then $F=G$. Hence, a **linear mappng** is fully determined by the values with it assigns to the basis vectors $v_1,...,v_n$.

### Def 0.13 Rank

The **rank** of a matrix $A=(a_1,...,a_n) \in \mathbb{R}^{p \times n}$ with $a_j \in \mathbb{R}^p$ for $j=1,...,n$ is the maximum numbers of **linear independent** column vector $a_j$.

> **Example**   
> $$
> A=\left(
  \begin{array}{ccc}
          1 & 1 & 1\\
          0 & 1 & 1\\
          0 & 0 & 1
  \end{array}
  \right),   
> rank(A)=3
$$

### Def 0.14 Transpose

Let $A=(a_1,...,a_n) \in \mathbb{R}^{p \times n}$ with $a_j \in \mathbb{R}^p$ for $j=1,...n$. The **transpose** $A^T$ is $$A^T = \left(
  \begin{array}{c}
          a_1^T\\
          \vdots\\
          a_n^T
  \end{array}
  \right) \in \mathbb{R}^{n \times p}$$

### Def 0.15 Invertable
A (quadratic)matrix $A \in \mathbb{R}^{n \times n}$ is called **invertable** if there exists some matrix 
$$
A' \in \mathbb{R}^{n \times n}\ s.t\ AA'=A'A=
\left(\begin{array}{cc}
1 & 0 \\
0 & 1
\end{array}\right)\in \mathbb{R}^{n \times n}
$$
  

One can show that matrix $A'$ in def 0.15 is uniquely determined. We use the notation $A'=A^{-1}$ is what follows and call $A^{-1}$ the **inverse (matrix)** of $A$.

calculation rule: $(A^T)^{-1}=(A^{-1})^T$


