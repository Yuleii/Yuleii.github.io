---
layout: article
title: Method Of Moments
key: 2020716
tags: Statistics InProgress
pageview: false
modify_date: 2020-07-16
aside:
  toc: true
---


Introduction to method of moments, generalized method of moments(GMM) and method of simulated moments (MSM)
<!--more-->

## Basic

Maximum likelihood is one way to get a point estimate, another way to get point estimate is to use the method of moments.

- Moment
  - $E(X)$: the first moment
  - $E(X^2)$: the second moment
  - $E(X^k)$: the $k^{th}$ moment of a random variable

- Estimate some mean using the method of moment:
  - Estimate for the first moment $E(X)$: $\frac{\sum X_i}{n}$
  - Estimate of $k^{th}$ moment $E(X^k)$: take a random sample of size $n$, then $\frac{\sum_{i=1}^n X_i^k}{n}$

## Example

- A random sample $X_1 \cdots, X_n$   
  - $\mu=E(X)$   
  - $\sigma^2=E(X-E[x])^2$ or $E(X^2)-\mu^2$   

- Method of moments estimator of $\mu$:  $\hat{\mu}=\frac{\sum_{i=1}^n X_i}{n}$   

- Method of moments estimator of $E(X^2)$:  $\frac{\sum_{i=1}^n X_i^2}{n}$ 

- Method of moments estimator of $\sigma^2$: $\hat{\sigma^2}=\frac{\sum_{i=1}^n X_i^2}{n}- \left[\frac{\sum_{i=1}^n X_i}{n} \right]^2$

## Course Link

[Method Of Moments](https://www.youtube.com/playlist?list=PLdxWrq0zBgPViBm1aBlYc5rvL2w5YIMot)

## To do
- [ ] [Moment Generating Functions](https://www.youtube.com/playlist?list=PLdxWrq0zBgPU0DUvONdlNpgndFr0e6qt3)
- [ ] [Method of Simulated Moments (MSM)](https://www.youtube.com/watch?v=pPqI5LbC96Y)
- [ ] [Simulated Method of Moments (SMM) Estimation](https://notes.quantecon.org/submission/5b3db2ceb9eab00015b89f93)
