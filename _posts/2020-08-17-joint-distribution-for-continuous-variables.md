---
layout: article
title: Joint Distributions for Continuous Variables
key: 20200817
tags: Statistics
pageview: false
modify_date: 2020-08-17
mathjax_autoNumber: false
aside:
  toc: true
---

An example for finding marginal PDF of two random variables given the joint probability density function

<!--more-->

## Example

- A certain factory produces two kinds of products on any given day; widgets and gizmos.
- Let these two kinds of products be represented by the random variables X and Y respectively.
- Given that the joint probability density function of these variables is given by   

$$
f(x,y)=
\begin{cases}
\frac{2}{3}(x+2y)& 0 \le x \le1,0 \le y \le 1 \\
0& \text{elsewhere}
\end{cases}
$$

## Questions

- Find the marginal PDF of X

$$
\begin{eqnarray*}
g(x)&=&\int_{-\infty}^\infty f(x,y)dy \\
&=&\int_0^1 \frac{2}{3}(x+2y)dy \\
&=&\frac{2}{3} \left[xy+y^2\right]_{y=0}^{y=1} \\
&=&\frac{2}{3}[x+1]-\frac{2}{3}[0+0] \\
&=&\frac{2}{3}(x+1) 
\end{eqnarray*}
$$

- Find the marginal PDF of Y

$$
\begin{eqnarray*}
h(y)&=&\int_{-\infty}^\infty f(x,y)dx \\
&=&\int_0^1 \frac{2}{3}(x+2y)dx \\
&=&\frac{2}{3} \left[\frac{x^2}{2}+2xy\right]_{x=0}^{x=1} \\
&=&\frac{2}{3}[\frac{1}{2}+2y]-\frac{2}{3}[0+0] \\
&=&\frac{2}{3}(\frac{1}{2}+2y)
\end{eqnarray*}
$$

- Find $P(X \le 1/2, Y \le 1/2)$

$$
P(X \le 1/2, Y \le 1/2)=
\int_0^{1/2} \int_0^{1/2} \frac{2}{3}(x+2y)dx\ dy
$$

$$
\begin{eqnarray*}
\int_0^{1/2} \frac{2}{3}(x+2y)dx 
&=& \frac{2}{3} \left[\frac{x^2}{2}+2xy\right]_{x=0}^{x=1/2} \\
&=& \frac{2}{3} [\frac{0.5^2}{2}+y]-[0+0] \\
&=& (\frac{1}{12}+\frac{2y}{23})
\end{eqnarray*}
$$

$$
\begin{eqnarray*}
\int_0^{1/2}(\frac{1}{12}+\frac{2y}{23})dy
&=&\left[\frac{y}{12}+\frac{2y^2}{6}\right]_{x=0}^{x=1/2} \\
&=&\frac{1}{24}+\frac{2}{24} \\
&=&\frac{1}{8} \\
\end{eqnarray*}
$$

## Source
[Joint Distributions for Continuous Variables - Worked Example](https://youtu.be/Om68Hkd7pfw)
