---
layout: article
title: Discrete Choice Methods with Simulation 
key: 2020715
tags: DiscreteChoice InProgress
pageview: false
modify_date: 2020-07-15
aside:
  toc: true
---

Notes on [Discrete Choice Methods with Simulation (Kenneth Train, 2009)](https://eml.berkeley.edu/books/choice2.html)

<!--more-->

# Introduction

## Choice Probabilities and Integration 

- Behavioral process: $y=h(x,\epsilon)$
    - $x$: observed factors
    - $\epsilon$: unobserved factors  
  
- Probability:
  $$P(y|x)=Prob(\epsilon \ s.t.\ h(x,\epsilon)=y)$$   

> The probability that the agent chooses a particular outcome from the set of all possible outcomes is simply the probability that the unobserved factors are such that the behavioral process results in that outcome   

- Probability in an indicator function form(1.1):   
  $$
  \begin{eqnarray*}
  P(y|x)&=&Prob(I \left[ h(x, \epsilon)=y \right] =1) \\
        &=& \int I \left[ h(x, \epsilon)=y \right] f(\epsilon)d \epsilon
  \end{eqnarray*}
  $$ 
    - $f(x)$: Density of unobserved random term $\epsilon$.
    - $I [h(x, \epsilon)=y ]$: Indicator function. $I [\cdot] = 1$ if the value of $\epsilon$, combined with $x$, induces the agent to choose outcome $y$, and $I [\cdot] = 0$ otherwise.   
  
> Stated in this form, the probability is an integral–specifically an integral of an indicator for the outcome of the behavioral process over all possible values of the unobserved factors.

## Integral Forms

### Complete Closed-Form Expression 

- Utility: $U=\beta' x+\epsilon$
    - The person takes the action only if the utility is positive($U>0$).
- Assume that $\epsilon$ is distributed logistically:
    - $f(\epsilon)=\frac{e^{-\epsilon}}{(1+ e^{-\epsilon})^2}$
    - $F(\epsilon)=\frac{1}{(1+ e^{-\epsilon})}$
- The probability of a person taking action:   
  $$
  \begin{eqnarray*}
  P&=&\int I \left[ \beta' x+\epsilon >0 \right] \ f(\epsilon)d\epsilon \\
        &=&\int I \left[ \epsilon >-\beta' x \right] \ f(\epsilon)d\epsilon \\
        &=&\int_{-\beta' x}^{\infty} \ f(\epsilon)d\epsilon \\
        &=&1-F(-\beta' x) \\
        &=&1-\frac{1}{1+ e^{-\epsilon}} \\
        &=&\frac{e^{\epsilon}}{1+ e^{\epsilon}}=\frac{\exp(\beta' x)}{1+\exp(\beta' x)}
  \end{eqnarray*}
  $$    

- Example:
  - Multinomial logit (in Chapter 3)
  - Nested logit (Chapter 4)
  - Ordered logit (Chapter 7)

- Notes: The integral for probabilities cannot be expressed in closed form.
   

### Complete Simulation

- $\bar{t} = \int t(\epsilon)f(\epsilon)d\epsilon$
    - $t(\epsilon)$ is a statistic based on $\epsilon$ which has density $f(\epsilon)$
> Simulation relies on the fact that integration over a density is a form of averaging Approximate true average with simulated average.   

- Simulation process:
    1. Take a draw of $\epsilon$ from $f(\epsilon)$. Label this draw $\epsilon^1$, where the superscript denotes that it is the first draw.
    2. Determine whether $h(x,\epsilon^1) = y$ with this value of $\epsilon$. If so, create $I^1 = 1$; otherwise set $I^1 = 0$.
    3. Repeat steps 1 and 2 many times, for a total of R draws. The indicator for each draw is labeled $I^r$ for $r = 1,...,R$.
    4. Calculate the average of the $I^r$'s. This average is the simulated probability: that the draws of the unobserved factors, when combined with
    the observed variables $x$, result in outcome $y$.   

- Example:
    - Probit (in Chapter 5)   
  
- Notes: Choice probabilities can often be expressed as averages of other statistics, rather than the average of an indicator function. The simulators based on these other statistics are calculated analogously, by taking draws from the density, calculating the statistic, and averaging the results. 

### Partial Simulation, Partial Closed Form 

- Random terms: $\epsilon=(\epsilon_1, \epsilon_2)$
    - joint density:    
      $f(\epsilon)=f(\epsilon_1, \epsilon_2)=f(\epsilon_2|\epsilon_1) \cdot f(\epsilon_1)$   

- Probability in equation(1.1):   
  $$
  \begin{eqnarray*}
  P(y|x)&=& \int I \left[ h(x, \epsilon)=y \right] f(\epsilon)d \epsilon \\
  &=& \int_{\epsilon_1} \left[ \int_{\epsilon_2} I \left[h(x, \epsilon_1, \epsilon_2)=y \right] f(\epsilon_2|\epsilon_1)d \epsilon_2 \right]f(\epsilon_1)d \epsilon_1 \\
  &=& \int_{\epsilon_1} g(\epsilon_1) f(\epsilon_1)d \epsilon_1
  \end{eqnarray*}
  $$    
  with   
  $$g(\epsilon_1) \equiv \int_{\epsilon_2} I \left[h(x, \epsilon_1, \epsilon_2)=y \right] f(\epsilon_2|\epsilon_1)d \epsilon_2$$
  
> Note that it is simply the average of g over the marginal density of $\epsilon_1$. The probability is simulated by taking draws from $f(\epsilon_1)$, calculating $g(\epsilon_1)$ for each draw, and averaging the results.   
   
- Example:
    - Mixed logit (in Chapter 6)




# Part I: Behavioral Models

# Part II: Estimation


