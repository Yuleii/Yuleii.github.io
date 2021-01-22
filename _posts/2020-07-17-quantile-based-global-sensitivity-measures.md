---
layout: article
title: Quantile Based Global Sensitivity Measures
key: 2020717
tags: SensitivityAnalysis
pageview: false
modify_date: 2020-08-20
mathjax_autoNumber: false
aside:
  toc: true
---

Notes on the paper [Quantile Based Global Sensitivity Measures by S. Kucherenko, S. Song, L. Wang](https://www.sciencedirect.com/science/article/abs/pii/S0951832016304574)

<!--more-->

# Sensitivity Measures 

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

#### Sensitivity Indices for Subsets of Variable

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

## Quantile Based Sensitivity Measure

### The αth quantile of the output CDF $q_Y(\alpha)$   

$$
\begin{eqnarray*}
\alpha&=&\int_{-\infty}^{q_{Y}(\alpha)} \rho_{Y}(y) d y=P\left\{Y \leq q_{Y}(\alpha)\right\} \\
&=&\int_{Y \leq q_{Y}(\alpha)} \rho_{X}(\mathbf{x}) d \mathbf{x}=\int_{R^{d}} I_{Y \leq q_{Y}(\alpha)}[Y(\mathbf{x})] \rho_{X}(\mathbf{x}) d \mathbf{x}
\end{eqnarray*}
$$

More formally,   

$$q_Y(\alpha)=F_Y^{-1}(\alpha)=\inf \left\{y|F(Y \le y) \ge \alpha \right\}$$

- $\rho_{Y}(y)$ and $F_Y(y)$ are PDF and CDF of the output Y, respectively 
- $I(x)$ is an indicator function


### New quantile-based sensitivity measures

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

## Other Moment Independent Measures

### Chun et al.

[Chun M, Han S, Tak N. An uncertainty importance measure using a distance metric for the change in a cumulative distribution function. Reliab Eng Syst Saf 2000;70:313–21](https://www.sciencedirect.com/science/article/abs/pii/S0951832000000685)

$$
\begin{eqnarray*}
CHT_{i}&=&\left[\int\left(q_{Y \mid X_{i}}(\alpha)-q_{Y}(\alpha)\right)^{2} d \alpha\right]^{1 / 2} / E[Y] \\
&=&\left[E_{\alpha}\left(q_{Y \mid X_{i}}(\alpha)-q_{Y}(\alpha)\right)^{2} d \alpha\right]^{1 / 2} / E[Y]
\end{eqnarray*}
$$

- $q_{Y \mid X_i}$ is $\alpha$th quantile of CDF of the output conditional on the input variable $x_i$ being fixed at $x_i=X_i$

### Borgonovo
[Borgonovo E. A new uncertainty importance measure. Reliab Eng Syst Saf 2007;92:771–84.](https://www.sciencedirect.com/science/article/abs/pii/S0951832006000883)

$$
\delta_{i}=\frac{1}{2} E_{x_{i}}\left[s\left(x_{i}\right)\right]=\frac{1}{2} \int \left[ \int \rho_{Y}(y)-\rho_{Y \mid X_{i}}(y) \mid d y \right] d F_{x_i}
$$

where $\rho_{Y \mid X_{i}}(y)$ is the conditional on $x_i=X_i$ PDF of the output Y.

## Linear Model with Normally Distributed Variables

$$
Y=a_1x_1+a_2x_2+ \cdots +a_dx_d
$$

- $x_i \sim N(\mu_i,\sigma_i^2)$
- $Y \sim N(\sum_{i=1}^d a_i \mu_i, \sum_{i=1}^d a_i^2 \sigma_i^2 )$
- $Y \mid X_i \sim N(a_i x_i+\sum_{j=1,j \ne i}^d a_j \mu_j, \sum_{j=1,j \ne i}^d a_j^2 \sigma_j^2 )$

**Sobol's sensitivity indice**

$$
S_i=S_i^{tot}=\frac{a_i^2 \sigma_i^2}{\sum_{j=1}^d a_j^2 \sigma_j^2}
$$

**For this model**

$$
q_Y(\alpha)=\sum_{i=1}^d a_i \mu_i + \Phi^{-1}(\alpha) \sqrt{\sum_{i=1}^d a_i^2 \sigma_i^2}
$$

$$
q_{Y|X_i=x_i}(\alpha)=a_i x_i + \sum_{j=1,j \ne i}^d a_j \mu_j + \Phi^{-1}(\alpha) \sqrt{\sum_{j=1,j \ne i}^d a_j^2 \sigma_j^2}
$$

where $\Phi^{-1}(\alpha)$ is the inverse error function.

**Hence**

$$
q_Y(\alpha)-q_{Y|X_i=x_i}(\alpha)=a_i(\mu_i - x_i)+\Phi^{-1}(\alpha) \left(\sqrt{\sum_{i=1}^d a_i^2 \sigma_i^2}-\sqrt{\sum_{j=1,j \ne i}^d a_j^2 \sigma_j^2} \right)
$$

$$
\begin{eqnarray*}
q_i^{(2)}(\alpha)&=&E_{x_i}[(q_Y(\alpha)-q_{Y \mid X_{i}}(\alpha))^2] \\
&=&E_{x_i} \left[ \left(a_i(\mu_i - x_i)+\Phi^{-1}(\alpha) \left(\sqrt{\sum_{i=1}^d a_i^2 \sigma_i^2}-\sqrt{\sum_{j=1,j \ne i}^d a_j^2 \sigma_j^2} \right) \right)^2 \right] \\
&=&a_i^2 \sigma_i^2+[\Phi^{-1}(\alpha)]^2 \left(\sqrt{\sum_{i=1}^d a_i^2 \sigma_i^2}-\sqrt{\sum_{j=1,j \ne i}^d a_j^2 \sigma_j^2} \right)^2 
\end{eqnarray*}
$$

**Theorem 1.** For the linear additive model with normally distributed variables  
$$
\qquad \qquad \qquad \qquad \qquad \qquad Q_i^{(2)}(\alpha=0.5)=S_i
$$
{:.info}

Proof:   
$\Phi^{-1}(\alpha=0.5)=0$   
$q_i^{(2)}=a_i^2 \sigma_i^2$   
$$Q_i^{(2)}(\alpha)=\frac{\bar{q}_i^{(2)}(\alpha)}{\sum_{j=1}^d \bar{q}_j^{(2)}(\alpha)}=\frac{a_i^2 \sigma_i^2}{\sum_{j=1}^d a_j^2 \sigma_j^2}=S_i$$

# Monte Carlo estimators

## The brute force estimator

- Sampling N point $X^l=(x_1^l, \dots , x_d^l)$
- Using MC or QMC sampling methods and estimating CDF 

$$
F_Y^{(N)}(y)=\frac{1}{N} \sum_{l=1}^N I(Y(x_1^l, \dots , x_d^l)<y)
$$

$$
F_{Y \mid X_i}^{(N)}(y)=\frac{1}{N} \sum_{l=1}^N I(Y(x_1^l, \dots , x_i = X_i, \dots , x_d^l)<y)
$$

- Once CDFs are computed, MC/QMC estimates of quantiles can be
computed as

$$
q_Y^{(N)}(\alpha)=[F_Y^{(N)}]^{-1}(\alpha)=\inf 	\left\{ y \mid F_Y^{(N)}(Y \le y) \ge \alpha \right\}
$$

$$
q_{Y \mid X_i}^{(N)}(\alpha)=[F_{Y \mid X_i}^{(N)}]^{-1}(\alpha)=\inf 	\left\{ y \mid F_{Y \mid X_i}^{(N)}(Y \le y \mid x_i=X_i) \ge \alpha \right\}
$$

- The Monte Carlo (MC) or Quasi-Monte Carlo (QMC) estimators

$$
q_i^{(1)}(\alpha)=\frac{1}{N} \sum_{j=1}^N \mid q_Y^{(N)}(\alpha)-q_{Y \mid X_i^{j}}^{(N)}(\alpha) \mid
$$

$$
q_i^{(2)}(\alpha)=\frac{1}{N} \sum_{j=1}^N \left( q_Y^{(N)}(\alpha)-q_{Y \mid X_i^{j}}^{(N)}(\alpha) \right)^2
$$

- The total number of sampled points and function evaluations for a fixed $i$ is equal to $N_T^i=NN+N$. To compute all $d$ estimates $N_T=dNN+N=N(dN+1)$.

## Double loop reordering (DLR) approach

- $N$ points $x^{(j)},j=1,2, \dots, N$ are generated from the joint PDF

- Values of the output$$\left\{ Y^{(j)}\right\}$$ are found at this sampled set $$\left\{ x^{(j)}\right\}$$

- CDF $F_Y(y)$ of the out put Y is found as before using

$$
F_Y^{(N)}(y)=\frac{1}{N} \sum_{l=1}^N I(Y(x_1^l, \dots , x_d^l)<y)
$$

- For each random variable $x_i$, the sample set $$\left\{ x^{(j)}\right\},j=1,2, \dots, N$$ with corresponding values of $$\left\{ Y^{(j)}\right\}$$ is sorted in ascending order with respect to the values of $x_i$ and subdivided in $M$ equally populated partitions(bins) with $N_m=N/M$ points in each bin $(M < N)$. Within each bin the CDF $F_{Y \mid X_i}(y)$ of the output conditional on the input variable  $x_i$ being fixed at $x_i=X_i^l, l=1, \dots ,N_m$ is estimated as

$$
F_{Y \mid X_i}^{(N_m)}(y)=\frac{1}{N_m} \sum_{l=1}^{N_m} I(Y(x_1^l, \dots , x_i^l = X_i^l, \dots , x_d^l)<y)
$$

- Once CDFs are computed, MC/QMC estimates of quantiles can be computed as before 

$$
q_Y^{(N)}(\alpha)=[F_Y^{(N)}]^{-1}(\alpha)=\inf 	\left\{ y \mid F_Y^{(N)}(Y \le y) \ge \alpha \right\}
$$

$$
q_{Y \mid X_i}^{(N)}(\alpha)=[F_{Y \mid X_i}^{(N)}]^{-1}(\alpha)=\inf 	\left\{ y \mid F_{Y \mid X_i}^{(N)}(Y \le y \mid x_i=X_i) \ge \alpha \right\}
$$

- Finally, the MC/QMC estimators of integrals have the form:

$$
\tilde{q_i}^{(1)}(\alpha)=\frac{1}{M} \sum_{j=1}^M \mid q_Y^{(N_m)}(\alpha)-q_{Y \mid X_i^{j}}^{(N_m)}(\alpha) \mid
$$

$$
\tilde{q_i}^{(2)}(\alpha)=\frac{1}{M} \sum_{j=1}^M \left( q_Y^{(N_m)}(\alpha)-q_{Y \mid X_i^{j}}^{(N_m)}(\alpha) \right)^2
$$

- The total number of sampled points and function evaluations required for computing $\tilde{q_i}^{(1)}(\alpha)$ and $\tilde{q_i}^{(2)}(\alpha)$ for all $i=1,2, \dots ,d$ is $N_T=N$

# Application

## Value at Risk

- Consider tomorrow's price $P$ for a portfolio which depends on a set of $d$ random variables

- Tomorrow's values $$\left\{x_i\right\}, i=1, \dots, d$$ for a set of "risk factors"

- The portfolio contains $m$ contracts whose values tomorrow are $$\left\{C_k\right\}, k=1, \dots, m$$

- Portfolio price function

$$
P(x_1,x_2, \dots ,x_d)=\sum_{k=1}^m C_k(x_1,x_2, \dots ,x_d)
$$

- We are interested in the value of the α-quantile of the profit and loss (P&L) distribution function of the portfolio which we denote $f_Y(y)$, where $Y=\Delta P$ is a change in the portfolio value over a specific defined time period $T$.

- VaR is an α-quantile of model output as defined by 

$$
q_Y(\alpha)=F_Y^{-1}(\alpha)=\inf \left\{y|F(Y \le y) \ge \alpha \right\}
$$

- Quantile measures based on VaR for eisk management problems:

$$
Q_i^{Var}=\frac{E_{x_i}(d[VaR_Y(\alpha)-VaR_{Y \mid X_i}(\alpha)])}{\sum_{j=1}^d E_{x_i}(d[VaR_Y(\alpha)-VaR_{Y \mid X_j}(\alpha)])}
$$

- $d[]$: $C_1$ distance and $L_2$ distance




