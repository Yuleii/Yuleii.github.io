---
layout: article
title: Quantile Based Global Sensitivity Measure
key: 2020717
tags: Econometrics InProgress
pageview: false
modify_date: 2020-08-17
mathjax_autoNumber: false
aside:
  toc: true
---

Notes for my master thesis.

<!--more-->

## Sobol' sensitivity indices

### Deterministic approach

#### ANOVA (Analysis of Variance) Decomposition

$f: \mathbb{R}^p \rightarrow \mathbb{R}$ may be decomposed as 

$$
\begin{eqnarray*}
f(x)&=&f_0+\sum_{i=1}^{p}f_i(x_i)+\sum_{1 \le i < j \le p}f_{i,j}(x_i,x_j)+ \dots +f_{1,2,\dots ,p}(x_1,x_2,\dots,x_p)\\
&=& f_0 +  \sum_{k=1}^{p} \sum_{|u|=k} f_u(x_u)
\end{eqnarray*}
$$   

where   
$f_0=\mathbb{E}[f(x)]$   
$f_i(x_i)=\mathbb{E}[f(x)|x_i]-f_0$   
$f_{i,j}(x_i,x_j)=\mathbb{E}[f(x)|x_i,x_j]-f_i(x_i)-f_j(x_j)-f_0$   

- this hierarchical decomposition exists $\forall f$ such that $f (x) \in L^2$   
- if $x_1,x_2,\dots,x_p$ are statistically independent then    
$$\mathbb{E}[f_u(x_u)f_v(x_v)]=0 \quad u \ne v$$
$$\Longrightarrow Var(f(x))=\sum_{k=1}^{p} \sum_{|u|=k} Var(f_u(x_u))$$

#### Sobol' indices   

$$S_u=\frac{Var(f_u(x_u))}{Var(f(x))}$$

- $S_u$ measures the relative contribution of $x_u$ to $Var(f_u(x_u))$
- there are $2^p-1$ Sobol's indices

#### Total Sobol' indices  

$$T_u=\sum_{v \cap u \ne \emptyset} S_v$$

#### First Order and Total Sobol’ Indices

$$\{S_k, T_k \}_{k=1}^p$$

- $S_k, T_k \in [0,1]$ measures the importance of $x_k$
- $S_k$ only measures the contribution of $x_k$
- $T_k$ measures the contribution of all interactions involving $x_k$
- $S_k \le T_k\ \forall k \in {1,2,...,p}$
- $T_u \le \sum_{K \in u} T_k\ \forall u \in {1,2,...,p}$

#### Sensitivity indices for subsets of variable

- model function: $Y=f(x_1, \dots x_d)$
- input vector: $x=(x_1, \dots x_d)$
- PDF: $\rho(x_1, \dots x_d)$
- subset of variables: $y=(x_{i_1}, \dots x_{i_s})=(x_i), 1 \le s< d, 1 \le i \le d$
- complementary subset $z=(x_{i_1}, \dots x_{i_{d-s}})=x_{\sim i}$, so that $x=(y,z)$
- total variance: $V= \sum_{s=1}^d \sum_{i_i < \dots < i_s} V_{i_i \dots i_s}$
- partial variance: $V_{i_{1} \ldots i_{s}}=\int_{0}^{1} f_{i_{1} \ldots i_{s}}^{2}\left(x_{i_{1}}, \ldots, x_{i_{s}}\right) d x_{i_{1}}, \ldots, x_{i_{s}}$

##### The variance corresponding to $y$

$$V_y= \sum_{m=1}^s \sum_{(i_1 < \dots < i_m) \in K} V_{i_1, \dots ,i_m}$$

##### Total variance

$$
V_y^{tot}=V-V_z
$$

##### Global sensitivity indices 

$$
S_y=\frac{V_y}{V}
$$   

$$
S_y^{tot}=\frac{V_y^{tot}}{V}
$$

### Probabilistic approach

#### Total variance of $f(x_1, \dots x_d)$   

$$
V=V_{X_i}(E_{X_{\sim i}}(Y|X_i))+E_{X_i}(V_{X_{\sim i}}(Y|X_i)) 
$$

$$
1=\frac{V_{X_i}(E_{X_{\sim i}}(Y|X_i))}{V}+\frac{E_{X_i}(V_{X_{\sim i}}(Y|X_i))}{V}
$$

#### First order sensitivity index

$$S_i=\frac{V_{X_i}(E_{X_{\sim i}}(Y|X_i))}{V}$$

$$S_i^{tot}=\frac{E_{X_{\sim i}}(V_{X_i}(Y|X_{\sim i}))}{V}$$

## Sensitivity measures based on quantiles of output and related to them measures

### The αth quantile of the output CDF $q_Y(\alpha)$   

$$
\begin{eqnarray*}
\alpha&=&\int_{-\infty}^{q_{Y}(\alpha)} \rho_{Y}(y) d y=P\left\{Y \leq q_{Y}(\alpha)\right\} \\
&=&\int_{Y \leq q_{Y}(\alpha)} \rho_{X}(\mathbf{x}) d \mathbf{x}=\int_{R^{d}} I_{Y \leq q_{Y}(\alpha)}[Y(\mathbf{x})] \rho_{X}(\mathbf{x}) d \mathbf{x}
\end{eqnarray*}
$$

More formally,   

$$q_Y(\alpha)=F_Y^{-1}(\alpha)=inf{y|F(Y \le y) \le \alpha}$$

- $\rho_{Y}(y)$ and $F_Y(y)$ are PDF and CDF of the output Y, respectively 
- $I(x)$ is an indicator function

### The moment independent measure based on quantiles

$$
\begin{eqnarray*}
CHT_{i}&=&\left[\int\left(q_{Y \mid X_{i}}(\alpha)-q_{Y}(\alpha)\right)^{2} d \alpha\right]^{1 / 2} / E[Y] \\
&=&\left[E_{\alpha}\left(q_{Y \mid X_{i}}(\alpha)-q_{Y}(\alpha)\right)^{2} d \alpha\right]^{1 / 2} / E[Y]
\end{eqnarray*}
$$

- $q_{Y \mid X_i}$ is $\alpha$th quantile of CDF of the output conditional on the input variable $x_i$ being fixed at $x_i=X_i$

### new quantile-based sensitivity measures

$$
\begin{eqnarray*}
\bar{q}_i^{(1)}(\alpha)&=&E_{x_i}(|q_Y(\alpha)-q_{Y \mid X_{i}}(\alpha)|) \\
&=&\int |q_Y(\alpha)-q_{Y \mid X_{i}}(\alpha)|dF_{x_i}
\end{eqnarray*}
$$

$$
\begin{eqnarray*}
\bar{q}_i^{(2)}(\alpha)&=&E_{x_i}[(q_Y(\alpha)-q_{Y \mid X_{i}}(\alpha))^2] \\
&=& \int (q_Y(\alpha)-q_{Y \mid X_{i}}(\alpha))^2 dF_{x_i}
\end{eqnarray*}
$$

Normalized versions of quantile-based sensitivity measures

$$Q_i^{(1)}(\alpha)=\frac{\bar{q}_i^{(1)}(\alpha)}{\sum_{j=1}^d \bar{q}_j^{(1)}(\alpha)}$$   

$$Q_i^{(2)}(\alpha)=\frac{\bar{q}_i^{(2)}(\alpha)}{\sum_{j=1}^d \bar{q}_j^{(2)}(\alpha)}$$
