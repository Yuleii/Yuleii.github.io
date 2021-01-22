---
layout: article
title: Linear Algebra for Econometrics
key: 20200612
tags: LinearAlgebra Econometrics
modify_date: 2020-06-13
pageview: false
mathjax: true
aside:
  toc: true
---


Notes for final exam.

<!--more-->


# Basic Concept

$$\{(y_i,x_i), i=1, ..., n\}$$

- **Regressand**: $y_i = (y_1, ..., y_n) (n\times 1)$
- **Regressor**: $x_i=(x_{i1}, ..., x_{ip}) (n\times p)$  
- **estimater**:$\beta=(\beta_0, \beta_1,..., \beta_p)(p\times 1)$

$$
\begin{eqnarray*}
y_i&=&\beta_0 + \beta_1x_{i1}+...+\beta_px_{ip}+\epsilon_i \\
    &=&X_i^\mathsf{T}\beta + \epsilon_i
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

**Case 1 Traditional Setteing**

p<<n (# of x << # of y)

**Case 2 Model Setting**

p>>n(# of y << # of x)

> $$
> \begin{eqnarray*}
> y_i &=& \beta_0 + \beta_1x_{i1}+...+\beta_{200}x_{i200}+\epsilon_i \\
> \beta&=&(\beta_0,\beta_1,...,\beta_200)^\mathsf{T} \\
     &=&(\beta_0,\beta_1,...,\beta_5,0,...,0)^\mathsf{T} \\
     n&=&200,p=5 \\
> \end{eqnarray*} 
> $$
> 
> Assume:$\{\beta_j:\beta_j\neq0\}$ << n  
> $$
 \hat{\beta_j}^{Lasso} = \mathop{\arg\min}_{b \in \mathbb{R}} \{\frac{1}{n}\sum_{i=1}^{n}(y_i-x_i^\mathsf{T}b)^2+\lambda\left \|b\right \|\}
 $$
> 
> ex.) x = {3,4}  
> $\quad \quad\left \|x\right \| = |3| + |4| = 7$


# 0. Recal Linear Algebra

## 0.1 Vector Space

- vectors space:  
$$\mathbb{R}^n, i.e. \{x=(x_1,...,x^n)^\mathsf{T}:x_i \in \mathbb{R },\forall i=1,...,n\}$$  
- Addition: for any vector $x=(x_1,...,x_n)^\mathsf{T}$ and $y=(y_1,...,y_n)^\mathsf{T}$   
$$
\begin{equation}
x+y=(x_1+y_1,x_2+y_2,...,x_n+y_n)^\mathsf{T}
\end{equation}
$$
- (Scalor) multiplication: for any $a \in \mathbb{R}$ and $x=(x_1,...,x_n)^\mathsf{T}$  
$ax=(ax_1,...,ax_n)^\mathsf{T}$

### Def 0.1 Linear Subset

A subset $w \in \mathbb{R}$ is called a **linear subset** of $\mathbb{R}^n$ if   
$(a)W\neq\varnothing$  
$(b)x,y\in w \Rightarrow x+y \in w$   
$(c)x \in w,a \in w\Rightarrow ax\in w$

> **Example**     
> Consider $\mathbb{R}^2$ with n=2 for any $x \in \mathbb{R}$, the line $$w=\{ax,a \in R\}$$ is a linear subset of $\mathbb{R}^2$.   

We check (a)-(c):   
$(a)W\neq\varnothing$  
$(b)Let\ y,z \in w$   
$\quad Then\ \exists\ a,b \in \mathbb{R}\ with\ y=ax \in w,z=bx \in w$   
$\quad s.t\ y+z=ax+bx=(a+b)x \in w$   
$(c)Let\ a \in \mathbb{R}, y \in w$   
$\quad Since\ y=bx$   
$Then\ \exists\ a \in \mathbb{R}, s.t.\ ay=(ab)y \in w$

> **E0 Q1**
> Check whether W is a linear subspace of $\mathbb{R}^2$    
> $$(a)\ W=\{(0,0)^\mathsf{T}\}$$.    
> $$(b)\ W=\{(x_1,x_2)^\mathsf{T} \in \mathbb{R}^2:a_1x_1+a_2x_2=b\}$$ with $a_1,a_2,b \in \mathbb{R}$.     
> $$(c)\ W=\{(x_1,x_2)^\mathsf{T} \in \mathbb{R}^2:x_1 \geq 0,x_2 \geq 0\}$$ with $a_1,a_2,b \in \mathbb{R}$.      
> $$(d)\ W=\{(x_1,x_2)^\mathsf{T} \in \mathbb{R}^2:x_1 \cdot x_2  \geq 0\}$$.      
> $$(e)\ W=\{(x_1,x_2)^\mathsf{T} \in \mathbb{R}^2:x_1^2+x_2^2 \leq 1\}$$.      
> $$(e)\ W=\{(x_1,x_2)^\mathsf{T} \in \mathbb{R}^2:x_1^2+x_2^2 = 0\}$$.   

> **E0 Q2**
> Check whether W is a linear subspace of $\mathbb{R}^3$   
> $$(a)\ W=\{(x_1,x_2,x_3)^\mathsf{T} \in \mathbb{R}^3:x_1=x_2=2x_3\}\ with\ a_1,a_2,b \in \mathbb{R}$$.   
> $$(b)\ W=\{(x_1,x_2,x_3)^\mathsf{T} \in \mathbb{R}^3:x_1 \geq x_2\}\ with\  a_1,a_2,b \in \mathbb{R}$$.

### Def 0.2 Linear Combination

Let $v_1,..,v_d \in \mathbb{R}$ is called a **linear combination** of $v_1,..,v_d$ if there exists constants $a_1,...,a_n\in \mathbb{R}\ s.t.\ v=a_1v_1+...+a_dv_d$.

> **Example**   
> Let $v_1=(1,0,0)^\mathsf{T}\in \mathbb{R}^3, v_2=(0,1,0)^\mathsf{T} \in \mathbb{R}^3$, for any $a,b\ \in \mathbb{R}$,the vector $v=(a,b,0)^\mathsf{T}$ is a linear combination of $v_1$ and $v_2$, since

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

> **E0 Q5**
> Represent the vector $w=(2,1,1)^\mathsf{T}$ as a linear combination of the vectors $v_1=(1,5,1)^\mathsf{T},v_2=(0,9,1)^\mathsf{T}$ and $v_3=(3,-3,1)^\mathsf{T}$.

### Def 0.3 Span

For $v_1,..,v_d \in \mathbb{R}^n$, we call **span**$$=\{ v_1,..,v_d \}=\{v \in \mathbb{R}^n, v=a_1v_1+...+a_dv_d\}$$ the space spanned by the vector $v_1,..,v_d \in \mathbb{R}$. Put differently, span$$\{v_1,..,v_d\}$$ is the set of linear combination of $v_1,..,v_d$.

> **Example**   
> Let $v_1=(1,0,0)^\mathsf{T} \in \mathbb{R}^3, v_2=(0,1,0)^\mathsf{T}\in \mathbb{R}^3$

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

For any $v_1,..,v_d \in \mathbb{R}^n$, span$$=\{v_1,..,v_d\}$$ is a **linear subspace** of  $\mathbb{R}^n$.

### Def 0.5 Linear Independence

- The vector $v_1,..,v_d \in \mathbb{R}^n$ are called **linearly independent** of for any $a_1,..,a_d \in \mathbb{R}$ with $a_1v_1+...+a_dv_d=0$, it holds that $a_1=...=a_d=0$.
- If there exists $a_1,..,a_d \in \mathbb{R}$ with $a_i \neq 0$ for some i and $a_1v_1+...+a_dv_d=0$, we say that $v_1,..,v_d$ are **linearly dependent**.

> **E0 Q3**
> Are the vectors $(1,2,3)^\mathsf{T},(4,5,6)^\mathsf{T},(7,8,9)^\mathsf{T}$ linearly independent?

> **E0 Q4**
> For which $t \in \mathbb{R}$ are the vectors $(1,3,4)^\mathsf{T},(3,t,11)^\mathsf{T}$ and $(-1,-4,0)^\mathsf{T}$ linearly dependent?

> **E0 Q6**
> Prove the following statement: A single vector $v \in \mathbb{R}^n$ is linearly independent if and only if $v \neq 0$.

### Remark 0.6 Linear dependence & Linear Combination

$v_1,..,v_d$ **linearly dependent** $\Longleftrightarrow$   
some vector can be written as a linear combination of the other vectors   
$v_1,..,v_d$ **linearly dependent** $\Longleftrightarrow$  
none of the vectors $v_i$ can be written as a linear combination of the other vectors.   

> **Example**
> The vectors $$v_1=
\left(\begin{array}{l}
1 \\
0 
\end{array}\right),v_2=
\left(\begin{array}{l}
1 \\
1 
\end{array}\right)$$ are linearly independent.

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

- A family of vector $$B=\{v_1,..,v_d\}$$ is a **generating system** of $\mathbb{R}$ if $\mathbb{R}^n=$ span $$\{v_1,..,v_d\}$$.
- A family of vector $$B=\{v_1,..,v_d\}$$ is a **basis** of $\mathbb{R}$ if B is a **generating system** of $\mathbb{R}$ and that vectors v_1,..,v_d are **linearly independent**.

> **E0 Q7**
> Specify a basis of the linear subspace $W$, where      
> $$(a)\ W=\{(x_1,x_2,x_3)^\mathsf{T} \in \mathbb{R}^3:x_1=x_3\}$$.   
> $$(b)\ W=\{(x_1,x_2,x_3,x_4)^\mathsf{T} \in \mathbb{R}^4:x_1+x_3=0,x_2+x_4=0\}$$.

### Remark 0.8 Length

- let $$B=\{v_1,..,v_d\}$$ be a **generating system** in $\mathbb{R}^n$, then $d>>n$
- let $$B=\{v_1,..,v_d\}$$ be a **basis** in $\mathbb{R}^n$, then $d=n$
That is, every basis of $\mathbb{R}^n$ has length(dimension).

### Def 0.9 Equivalent statement of generating system

Let $$B=\{v_1,..,v_d\}$$ be a family of vectors in $\mathbb{R}^n$. The following statement are equivalent:   
- B is a **basis** in $\mathbb{R}^n$.
- B is a **generating system** of $\mathbb{R}^n$ that can be standard. That is, for any $$i,\{v_1,..,v_{i-1},v_{i+1},...,v_d\}$$ is not a **generating system** of $\mathbb{R}^n$.
- for any $v \in \mathbb{R}^n$, there exists unique constant $a_1,..,a_d \in \mathbb{R}, s.t\ v=a_1v_1+...+a_dv_d$.
- B is a maximun **linear independent system**. That is, for any $v \in \mathbb{R}^n,v_1,v_1..,v_d$ are not **linear independent**.

### Prop 0.10 Basis in linearly independent vectors

Let $v_1,..,v_d \in \mathbb{R}^n$ **linearly independent** vectors with $d<n$. Then we can find $$v_{d+1},...,v_n \in \mathbb{R}^n\ s.t\ B=\{v_1,..,v_d\}$$ is a **basis** of $\mathbb{R}^n$.


## 0.2 Linear Mappings and Matrix

### Def 0.10 Linearly Mapping

A function $F:\mathbb{R}^n \to \mathbb{R}^p$ is called a **liearly mapping** if for all$v,w \in \mathbb{R}^n$ and $a \in \mathbb{R}$:   
$(i)\ F(v+w)=F(v)+F(w)$   
$(ii)\ F(av)=aF(v)$

> **E0 Q8**
> Let $F:\mathbb{R}^n \to \mathbb{R}^p$ be a linear mapping. Prove the following:   
> (a) $F(0)=0$.   
> (b) If the vectors $v_1,...,v_d \in \mathbb{R}^n$ are linearly dependent, the the vectors $F(v_1),...,F(v_d) \in \mathbb{R}^n$ are linearly dependent as well.

>  **E0 Q9**
> Is there a linear mapping $F:\mathbb{R}^2 \to \mathbb{R}^2$ with   
$$F(2,0)=(0,1)^\mathsf{T},F(1,1)=(5,2)^\mathsf{T},F(1,2)=(2,3)^\mathsf{T}?$$

### Prop 0.11 Linear mapping represented by matrix

For **linear mapping** $F:\mathbb{R}^n \to \mathbb{R}^p$, there exists a unique matrix $A \in \mathbb{R}^{p \times n}\ s.t\ F(x)=A(x)$ for all $x \in \mathbb{R}^n$.

> **E0 Q10**
> Check whether the mapping $F:\mathbb{R}^2 \to \mathbb{R}^2$ defined by $F(x,y)=(3x+2y,x)^\mathsf{T}$ is linear?

### Remark 0.12 Linear Mapping & Basis

Let $$\{v_1,..,v_d\}$$ be a **basis** of $\mathbb{R}$ and $F,G:\mathbb{R}^n \to \mathbb{R}^p$ two **linear mappngs** with$F(v_1) \to G(v_1),\ v_1=1,...,n$. Then $F=G$. Hence, a **linear mappng** is fully determined by the values with it assigns to the basis vectors $v_1,...,v_n$.

> **E0 Q11**
> Let $$\{v_1,..,v_d\}$$ be a basis of $\mathbb{R}$ and $F,G:\mathbb{R}^n \to \mathbb{R}^p$ two linear mapping with
$$
F(v_i) = G(v_i)\  for\ i=1,..,n.
$$   
Prove that $F=G$.

> **E0 Q12**
> Compute the matrix product $A \cdot B$, where
$$
A=\left(
  \begin{array}{ccc}
          1 & -1 & 2\\
          0 & 3 & 5\\
          1 & 8 & -7
  \end{array}
  \right)\ and\  
  B=\left(
  \begin{array}{cc}
          1 & 4 \\
          0 & 5\\
          6 & 8 
  \end{array}
  \right).
$$


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

Let $A=(a_1,...,a_n) \in \mathbb{R}^{p \times n}$ with $a_j \in \mathbb{R}^p$ for $j=1,...n$. The **transpose** $A^\mathsf{T}$ is $$A^\mathsf{T} = \left(
  \begin{array}{c}
          a_1^\mathsf{T}\\
          \vdots\\
          a_n^\mathsf{T}
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

calculation rule: $(A^\mathsf{T})^{-1}=(A^{-1})^\mathsf{T}$


## 0.3 Orthogonality

### Def 0.16 Inner Product

For two vectors $x=(x_1,...x_n)^\mathsf{T}\in \mathbb{R}^n$ and $y=(y_1,...y_n)^\mathsf{T}\in \mathbb{R}^n$
$$
<x,y> = x^\mathsf{T}y=x_1y_1+...+x_ny_n
$$
is the **unit/scalor/innerproduct** of $x$ and $y$.

#### Properties of inner product:

For $x,x'$,$y,y'\in \mathbb{R}^n$ and $a \in \mathbb{R}$
- $\langle x+x',y \rangle=\langle x,y \rangle + \langle x',y \rangle$   
$\langle x,y+y' \rangle=\langle x,y \rangle + \langle x,y' \rangle$
- $\langle ax,y \rangle=a\langle x,y \rangle$   
$\langle x,ay \rangle=a\langle x,y \rangle$   
- $\langle x,y \rangle=\langle y,x \rangle$   
- $\langle x,y \rangle \geq 0 \Longleftrightarrow x=0$ 

### Def 0.17 Norm

The **(Euclidean)norm** of $x=(x_1,...x_n)^\mathsf{T}\in \mathbb{R}^n$ is
$$
\left \|x\right \|=\sqrt{\langle x,x \rangle}=\sqrt{x_1^2+...+x_n^2}
$$

#### Proporties of norm

For any $x,y\in \mathbb{R}^n$ and $a \in \mathbb{R}$
- $\left \|x\right \| \Longleftrightarrow x=0$,  
- $\left \|ax\right \| =  abs(a) \left \|x\right \|$ 
- $\left \|x+y\right \| \leq \left \|x\right \| + \left \|y\right \|$(Trangle Inequality)

### Def 0.18 Cauchy Schwarz Inequality

Fix $x,y \in \mathbb{R}^n$, it holds that
$$
|\langle x,y \rangle| \leq \left \|x\right \| \left \|y\right \|
$$

### Def 0.19 Orthogonal

Two vectors $x,y \in \mathbb{R}^n$ are **orthogonal** if 
$$
\langle x,y \rangle=0\ for\ x,y \neq 0
$$   

Notation: if $\langle v,w \rangle=0$, we write $x \perp y$

### Def 0.20 Orthogonal Basis
Let $$B=\{v_1,...v_n\}$$ be a **basis** of $\mathbb{R}^n$, s.t.$\left \|v_i\right \|=1$ for all $i$ and $v_i \perp v_j$ for all $i \neq j$. We call $B$ an **orthogonal basis**.


<!-- # 1. Mathmatical Basis

## 1.1 Coordinate Transformations and Orthogonal Matrices

### Def1.1 Coordinate Transformation
For any vector $x=(x_1,...x_n)^\mathsf{T}\in \mathbb{R}^n$, let $y_1,...,y_n$ be real numbers with $x=y_1f_1+...,+y_nf_n$.
We call $y_1,...,y_n$ the coordinate of $x\ w.r.t.$ the **basis** $$\{f_1,...,f_n\}$$    

The **coordinate vector** $y=(y_1,...y_n)^\mathsf{T}$ is given by 
$$
y=O^\mathsf{T}x=\left(
  \begin{array}{c}
          f_1^\mathsf{T}\\
          \vdots\\
          f_n^\mathsf{T}
  \end{array}
  \right)x=\left(
  \begin{array}{c}
          f_1^\mathsf{T}x\\
          \vdots\\
          f_n^\mathsf{T}x
  \end{array}
  \right)
$$    -->

