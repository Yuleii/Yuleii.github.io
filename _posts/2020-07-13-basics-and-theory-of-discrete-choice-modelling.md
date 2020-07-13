---
layout: article
title: Discrete Choice Modelling
key: 2020713
tags: Economics incomplete
pageview: false
modify_date: 2020-07-13
aside:
  toc: true
---

Basic and theory of discrete choice modelling

<!--more-->

## Mode Choice: Disaggregate Modelling

- Individuals = decision makers
- Choice process
    - first, an **individual** determines the **available alternatives**
    - next, evaluates the **attributes of each alternative**
    - then, use a **decision rule** to select an alternative.

- Four elements in a choice process:
    - Decision maker
    - Alternatives
    - Attributes of alternative
    - Decision rule

### The Decision Maker

- Different decision makers face different choice situations and can have **different tastes**(that is, they value attributes differently).
- For example, two individuals with different income levels and different residential locations are likely to have different sets of modes to choose from and may place different importance weights on travel time, travel cost and other attributes.

### The Alternatives

- individuals make a choice from a set of alternatives available to them.
- Set of available alternatives may be constrained by the infrastructure/supply.

###  Attributes of Alternative

- The alternatives in a choice process are characterized by a set of attribute values.
- Attractiveness of an alternative is determined by the value of its attributes.
- The attributes of alternatives may be genetic(that is ,they apply to all alternatives equally) or alternative-specific(they apply to one or a subset of alternatives).
- For example, in-vehicle-time is usually a generic attribute for all motorized alternatives. While wait time in relevant to transit modes only.

###  The Decision Rule

- An individual invokes a decision rule to select an alternative.
- The decision rule may include random choice, variety seeking, or other processes which refer to as being irrational.
- A number of possible rules fall under the *"rational decision"* processes.
- Here we focus on **"utility maximization"** as one such decision rule

###  Utility Maximization

- Utility maximization rule is based on two fundamental concepts:
    - The attribute vector chartering each alternative can be reduced to a scalar utility value for that alternative. Presuming that individuals make "trade-offs" among the attributes.
    - An individual selects the alternative with highest utility value. 

###  Utility-Based Choice Theory

- Utility is an indicator of value to an individual.
- The utility maximization rule states that an individual will select the alternative from his/her set of available alternatives that maximize his or her utility.
- The **utility function(U)** contains attributes of alternatives and characteristics of individuals that describes an individual's utility valuation for each alternative.

$$U(X_i,S_t)\ge U(X_j,S_t) \forall j \ \Rightarrow \ i  \succ  j \ \forall j \in C$$   
where    
**$U( )$** is the mathematical utility function,   
**$X_i,X_j$** are vectors of attributes describing alternatives $i$ and $j$, respectively(e.g., travel time, travel cost, and other relevant attributes of available mode),   
**$S_t$** is a vector of characteristics describing individual $t$, that influence his/her preferences among alternatives(e.g., household income and number of automobiles owned for travel mode choice),
{:.info}

### Errors in Deterministic Utility Functions

- The individual may incomplete or incorrect information or misperception about the attributes of some or all of the alternatives.
- The analyst("you") has different or incomplete information about the same attributes relative to the individuals.
- The analyst is unlikely to know, or account for, specific circumstances of the individual's travel decision.

Thus, taking a **probabilistic** approach is recommended.

### probabilistic Utility Function

$$U_{it}=V_{it}+\epsilon_{it}$$   
where   
**$U_{it}$** is the true utility of the alternative i to the decision maker $t$,($U_{it}$ is equivalent to $U(X_i,S_t))$ but provides a simpler notation),   
**$V_{it}$** is the deterministic or observable portion of the utility estimated by the analyst,   
**$\epsilon_{it}$** is the error or the portion of the utility unknown to the analyst. 
{:.info}

### Components of the Deterministic Portion of the Utility Function

- Related to the attributes of alternatives
- Related to the characteristics of the decision maker
- Representing the interactions between the attributes of alternatives and the characteristics of the decision maker.

$$V_{it}=V(S_t)+V(X_i)+V(S_t,X_i)$$   
where   
**$V_{it}$** is the systematic portion of utility of alternative $i$ for individual $t$,   
**$V(S_t)$** is the portion of utility associated with characteristics of individual $t$,   
**$V(X_i)$** is the portion of utility of alternative i associated with the attributes of alternative $i$,   
**$V(S_t,X_i)$** is the portion of the utility which results from in between the attributes of alternative $i$ and the characteristics of individual $t$.
{:.info}

### Utility Associated with the Attributes of Alternatives

The utility function usually includes
- Total travel time
- In-vehicle travel time
- Out-of vehicle travel time
- Travel cost
- Number of transfers(transit modes only)
- Walk distance
- Travel time reliability

Measures may differ across alternatives for the same individual and also among individuals due to  differences in the origin and the decision locations of each person's travel.   

$$V(X_{i})=\gamma_1 \times X_{i1} + \gamma_2 \times X_{i2}+ \cdots + \gamma_k \times X_{ik}$$   
where   
**$\gamma_k$** is the parameter which defined the direction and importance of he effect of attribute $k$ on the utility of an alternative,   
**$X_{ik}$** is the value of attribute $k$ for individual $i$.
{:.info}

**Example**   
A specific example for Drive Alone(DA), Share Ride(SR), and Transit(TR) alternatives is:
$$V(X_{DA})=\gamma_1 \times TT_{DA} + \gamma_2 \times TC_{DA}$$  
$$V(X_{SR})=\gamma_1 \times TT_{SR} + \gamma_2 \times TC_{SR}$$  
$$V(X_{TR})=\gamma_1 \times TT_{TR} + \gamma_2 \times TC_{TR} + \gamma_3 \times FREQ_{TR}$$ 
where   
$TT_i$ is the travel time for mode $i(i=DA,SR,TR)$ and  
$TC_i$ is the travel cost for mode $i$, and   
$FREQ_{TR}$ is the frequency for transit service.
{:.success}

### Utility Function to the Characteristics of the Decision Maker

The utility function could also include
- Income of the individual/household
- Gender
- Age
- Number of vehicles in traveler's household
- Number of workers in traveler's household
- Number of adults in traveler's household

$$\beta_{i0} \times ASC_i +\beta_{i1} \times S_{1t} + \beta_{i2} \times S_{2t} + \cdot + \beta_{iM} \times S_{Mt}$$   
where   
**$\beta$** is the parameter which defines the direction and magnitude of the incremental bias due to an increase in the $m^{th}$ characteristic of the decision maker($m=0$ represents the parameter associated with the alternative specific constant) and    
**$S_{mt}$** is the value of the $m^{th}$ characteristics for individual $t$.
{:.info}

**Example**   
For the case of three alternatives(DA, SR, and TR), the decision maker components of the utility functions are:
$$V(S_{DA})=\beta_{DA,0} \times 1 + \beta_{DA,1} \times Inc_t + \beta_{DA,2} \times NCar_t$$   
$$V(S_{SR})=\beta_{SR,0} \times 1 + \beta_{SR,1} \times Inc_t + \beta_{SR,2} \times NCar_t$$ 
$$V(S_{TR})=\beta_{TR,0} \times 1 + \beta_{TR,1} \times Inc_t + \beta_{TR,2} \times NCar_t$$ 
where   
**$\beta_{i,0}$** is the modal bias constant for mode $i(i=DA,SR,TR)$,   
**$Inc_t$** is the household income of the traveler,    
**$NCar_t$** is the number of cars in the traveler's household, and    
**$\beta_{i,1}, \beta_{i,2}$** are mode specific parameters on income and cars, respectively, for mode $i(i=DA,SR,TR)$.   
{:.success}

### Specification of the additive Error Term

In the alternative examples used above, the utility of each alternative can be represented by:

$$V_{DA}=V(S_t)+V(X_{DA})+V(S_t,X_DA) + \epsilon_{DA}$$   
$$V_{SR}=V(S_t)+V(X_{SR})+V(S_t,X_SR) + \epsilon_{SR}$$   
$$V_{TR}=V(S_t)+V(X_{TR})+V(S_t,X_TR) + \epsilon_{TR}$$   
where   
$V()$ represents the deterministic components of the utility for the alternatives, and     
$\epsilon_i$ represents the random components of the utility, also called the error term.
{:.success}