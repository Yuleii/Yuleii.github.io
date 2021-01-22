---
layout: article
title: Notes on Discrete Choice Modelling
key: 2020713
tags: DiscreteChoice
pageview: false
modify_date: 2020-07-14
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

##  Utility Maximization

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

### Probabilistic Utility Function

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

$$V_{DA}=V(S_t)+V(X_{DA})+V(S_t,X_{DA}) + \epsilon_{DA}$$   
$$V_{SR}=V(S_t)+V(X_{SR})+V(S_t,X_{SR}) + \epsilon_{SR}$$   
$$V_{TR}=V(S_t)+V(X_{TR})+V(S_t,X_{TR}) + \epsilon_{TR}$$   
where   
$V()$ represents the deterministic components of the utility for the alternatives, and     
$\epsilon_i$ represents the random components of the utility, also called the error term.
{:.success}

### Distribution of The Error Term

- If we assume the error is **normally distributed**, this leads to the formulation of the **Multinomial Probit choice model**.   
- If we assume the error term has a **Gumbel**(or Extreme-Value) distribution, theis leads to the formulation of the **Multinomial Logit Model(MNL)**

## Multinomial Logit Model

The specific assumption that lead to the Multinomial Logit Model(NML) are:   
- The error components follow a Gumbel distribution.
- The error components are identical and independently distributed(IID) across alternatives.
- The error components are identically and independently distributed(IID) across observations/individuals.

Te MNL give the choice probabilities of each alternative as a function of the deterministic portion of the utility of all the alternatives.   
$$Pr(i)=\frac{\exp(V_i)}{\sum_{j=1}^{J} \exp(V_j)}$$   
where   
$Pr(i)$ is the probability of the decision-maker choosing alternative $i$ and   
$V_j$ is the systematic component of the utility of alternative $j$.
{:.info}

**Example**   
Going back to the DA, SR and TR example, the probabilities of each alternative are then:   
$$Pr(DA)=\frac{\exp(V_{DA})}{\exp(V_{DA})+\exp(V_{SR})+\exp(V_{TR})}$$   
$$Pr(SR)=\frac{\exp(V_{SR})}{\exp(V_{DA})+\exp(V_{SR}+\exp(V_{TR}))}$$   
$$Pr(TR)=\frac{\exp(V_{TA})}{\exp(V_{DA})+\exp(V_{SR}+\exp(V_{TR}))}$$
{:.success}   

### Application 1: Travel Demand Modelling

This application focus on the problem of peak period travel between an outer suburb and the CBD. Residents of the selected outer suburb have the opinion of driving to the CBD or taking a bus or train. A total of 15,000 people make the trip from the selected suburb to the CBD each day, You have been hired by the bus operator to forecast the effects of some new operating policies. A logit mode choice model, previously estimated using data collected in another part of the city is available for the analysis.The utility function for the model is as follows.   

$V_m=0.5(CD)-0.05(IVTT_m)-0.1(OVTT_m)-0.22(OPTC_m)$ 

where   
$V_m$ = utility of the mode $m$   
$CD$ = car mode dummy variable(1 for car and 0 for other modes)   
$IVTT_m$ = in-vehicle travel time for mode $m$   
$OVTT_m$ = out-of-vehicle travel time for mode $m$   
$OPTC_m$ = out-of-pocket total cost for mode $m$($)    

**Table 1: Current characteristics of the modes.**

|---
|  | Car| Bus |Train
|:-:|:-:|:-:|:-:
| In-vehicle time(mins) | 40 | 50 | 45 
| Out-of-vehicle time(mins) | 7 | 12 |17 
| Out-of-pocket cost($) | 4.75 | 1.10 |2.50
|---

(a) Examine the coefficients in the utility function. Are the signs logical?  What effects would be captured by the car mode dummy variable? Are the relative magnitudes of the in- and out-of vehicle travel times consistent with expectations?   

> The dummy variable associated with car mode has a positive sign, that means if all the other components are 0, the utility value of car would be higher than the utility value of all the other modes. Because cars are generally preferred by people.   
> The sign of in-vehicle travel time is negative means that if in-vehicle travel increases, the utility value of an alternatives would go down. So you less likely to choose the alternative because it takes much longer time to get to CBD. Same logic with OVTT and OPTC.

(b) Use the mode choice model to predict the current bus ridership(# of traveller) and revenue for the morning service to the CBD.   


```py
import numpy as np
import pandas as pd

# Create dataframe.
dict = {"IVTT": [40, 50, 45], "OVTT": [7, 12 ,17], "OPTC": [4.75, 1.1, 2.5]}
df = pd.DataFrame(dict, index=["Car", "Bus", "Train"])
print(df)
>      IVTT  OVTT  OPTC
Car      40     7  4.75
Bus      50    12  1.10
Train    45    17  2.50

# Calculate utility values of three modes. Given utility functor and characteristics table.
# CD=1 only for car alternative.
V_car = 0.5 *1 - 0.05*df["IVTT"]['Car'] - 0.1 * df["OVTT"]['Car'] -0.22 * df["OPTC"]['Car']
V_bus = 0.5 *0 - 0.05*df["IVTT"]['Bus'] - 0.1 * df["OVTT"]['Bus'] -0.22 * df["OPTC"]['Bus']
V_train = 0.5 *0 - 0.05*df["IVTT"]['Train'] - 0.1 * df["OVTT"]['Train'] -0.22 * df["OPTC"]['Train']

# Create new columns
df['Utility'] = [V_car, V_bus, V_train]
# Exponential value of each utility.
df['Exp_V'] = np.exp(df['Utility'])
# Summation of exponential values.  
sum_exp_V_j = df["Exp_V"].sum()
# probability of three modes being selected.
df['Pr_i'] = df['Exp_V'] / sum_exp_V_j
# The sum of these probabilities should be equal to 1.
print(df['Pr_i'].sum())
> 1.0
# Number of Travellers(ridership).
df['n_traveller'] = df['Pr_i'] * 15000
# Revenue for bus and train company.
df['revenue'] = df['n_traveller'] * df["OPTC"]

print(df)
>      IVTT  OVTT  OPTC  Utility     Exp_V      Pr_i  n_traveller  \
Car      40     7  4.75   -3.245  0.038969  0.560804  8412.064911   
Bus      50    12  1.10   -3.942  0.019409  0.279324  4189.858549   
Train    45    17  2.50   -4.500  0.011109  0.159872  2398.076540   

            revenue  
Car    39957.308326  
Bus     4608.844404  
Train   5995.191349  
```

(c) One option involves increasing the service in the peak hour from 6 buses to 8 pre hour. This will reduce the out-of vehicle time for the bus to 10.75 mins, and cut travel time from 50 mins to 47 mins. Predict the effects of these changes on ridership and revenue for the morning service to the CBD.

```py
# Change the value
# For bus, IVTT decrease from 50 to 47, OVTT drop from 12 to 10.75.
dict = {"IVTT": [40, 47, 45], "OVTT": [7, 10.75 ,17], "OPTC": [4.75, 1.1, 2.5]}

# Others remain the same.
print(df)
>      IVTT   OVTT  OPTC  Utility     Exp_V      Pr_i  n_traveller  \
Car      40   7.00  4.75   -3.245  0.038969  0.515249  7728.732266   
Bus      47  10.75  1.10   -3.667  0.025553  0.337866  5067.992828   
Train    45  17.00  2.50   -4.500  0.011109  0.146885  2203.274906   

            revenue  
Car    36711.478262  
Bus     5574.792111  
Train   5508.187266  
```

> For bus, ridership increases from 4189 to 5067 users, as a result the revenue increase(from 4608 to 5574).


### The Equivalent Differences Property

A fundamental property of the multinomial logit and other choice models is that the choice probabilities of the alternatives depend only on the differences in the deterministic utilities of different alternatives and not their actual values.

**Example**     
$$Pr(i)=\frac{\exp(V_{i})}{\exp(V_{DA})+\exp(V_{SR})+\exp(V_{TR})}$$   
rewrite by adding $\Delta$ to each utility value of each alternatives, the probability value remains the same:
$$Pr(i)=\frac{\exp(V_{i} + \Delta V)}{\exp(V_{DA}+ \Delta V)+\exp(V_{SR})+\exp(V_{TR}+ \Delta V)}$$
{:.success}   

### Independence of Irrelevant Alternatives: IIA Property

- One of the most widely discussed properties of the NML model is its independence of irrelevant alternatives(IIA) property.
- For any individual, the ratio of the probabilities of choosing two alternatives is independent of the presence or attributes of any other alternative.
- Example: "Red bus, blue bus".


### Application 2: Red bus, blue bus

Consider a city where 50% of travellers choose car(C) and 50% choose bus(B). In terms of model(6.8), which is an N-way structure, this means that $C_C = C_B$. Let us now assume that the manager os the bus company, in a stroke of marketing genius, decides to paint half the buses res(RB) and half of them blue(BB), but manages to remain the same level of service as before. This means that $C_{RB}=C_{BB}$, and as the car mode has not changed this values is still equal to $C_C$. It is interesting to note that model(6.8) now predicts:   

$$P_C=\frac{\exp(-\beta C_C)}{\exp(-\beta C_C)+\exp(-\beta C_{RB})+\exp(-\beta C_{RB})}=0.33$$    

when one would expect $P_C$ to remain 0.5, and the buses to share the other half of the market equally between red and blue buses. The example is, of course, exaggerated but serves well to show the problems of the N-way structure in the presence of correlated options(in this case completely correlated). 

> This shows that the effect of IIA property that if your alternatives are not totally independent and irrelevant to each other, what you end up in probabilities would be biased.

## Model Development

Logit model development consists of   
- formulating model specifications
- estimating numerical values of the parameters for the various attributes specified in each utility function by fitting the models to the observed choice data

### Maximum Likelihood Estimation Theory

- Finding model parameters which maximize the likelihood of the observed choices cnditional on the model.
    - Develop a joint probability density function of the observed sample, called the likelihood function.
    - Estimating parameter values which maximize the likelihood function. 


$$L(\beta)=\prod_{\forall t\in T} \prod_{\forall j\in J}(P_{jt}(\beta))^{\delta_{jt}}$$   
where   
$\delta_{jt}=1$ is chosen indicator(=1 if $j$ is chosen by individual $t$ and 0, otherwise) and   
$P_{jt}$ is the probability that individual $t$ chooses alternative $j$.   
The values of the parameters which maximize the likelihood function are obtained by finding the first derivative of the likelihood function and equating it to zero.
{:.info}

- The log of function yields the same maximum as the function and is mre convenient to differentiate.
- Therefore, we maximize the log-likelihood function instead of the likelihood function itself.

$$LL(\beta)=\log(L(\beta))=\sum_{\forall t\in T} \sum_{\forall j\in J}\delta_{jt} \times \ln(P_{jt}(\beta))$$  
$$\frac{\partial(LL)}{\partial \beta_k}=\sum_{\forall t\in T} \sum_{\forall j\in J}\delta_{jt} \times \frac{1}{P_{jt}} \times \frac{P_{jt}(\beta)}{\partial \beta} \qquad \forall k$$ 
{:.info}

### Application 3: Maximum Likelihood Estimator

Suppose a logit model of binary choice between cars and bus is to be estimated. For simplicity, let us assume the utility specification includes only the travel time variable that the deterministic portion of the utility function for the two modes is defined as follows:   
      
$$V_{Auto}=\beta_1 \times Travel Time_{Auto}$$   
$$V_{Bus}=\beta_1 \times Travel Time_{Bus}$$     
    
Suppose that the estimation sample consists of observation of modes choice of only three individuals. The modal travel times and observed choice foe each os the three individuals in the sample is as follows:  

|---
| Individual # | Auto Travel Time| Bus Travel Time |Chosen Mode
|:-:|:-:|:-:|:-:
| 1 | 30 mins | 50 mins | Car(mode 1) 
| 2 | 20 mins | 10 mins | Car(mode 1) 
| 3 | 40 mins | 30 mins | Bus(mode 2) 
|---

According to the logit model, the probabilities for the observes mode for each individual are:   
$$Individual \ 1 \ (P_{11})=\frac{\exp(30\beta)}{\exp(50\beta)+\exp(30\beta)}=\frac{1}{1+\exp(20\beta)}$$   
$$Individual \ 2 \ (P_{12})=\frac{\exp(20\beta)}{\exp(10\beta)+\exp(20\beta)}=\frac{1}{1+\exp(-10\beta)}$$   
$$Individual \ 3 \ (P_{23})=\frac{\exp(30\beta)}{\exp(30\beta)+\exp(40\beta)}=\frac{1}{1+\exp(10\beta)}$$     

The log-likelihood expression for this sample will be as follows:  

$$
\begin{eqnarray*}
LL(\beta) &=& \sum_{j=1,2} \sum_{t=1,2,3}\delta_{jt} \times \ln(P_{jt}(\beta)) \\
&=& 1\times \ln(P_{11}+0\times \ln(P_{21})) \\
&+& 1\times \ln(P_{12}+0\times \ln(P_{22})) \\
&+& 0\times \ln(P_{13}+0\times \ln(P_{23})) \\
&=& \ln(P_{11}) + \ln(P_{12}) + \ln(P_{23})
\end{eqnarray*} 
$$

A maximum likelihood estimator finds the value of the parameter $\beta$ which maximizes the *log-likelihood* value. This solution is obtained by setting the first derivative of the log-likelihood function equal to zero, and solving for $\hat{\beta}$. However, for this illustrative example, we can plot the graph for log-likelihood(or likelihood) as a function of $\beta$ to find the point where yhe maximum occurs. Figure 1 shows the graph of likelihood and log-likelihood as a function of $\beta$. It can be seen that the point where the maximum occurs is identical for the likelihood and the log-likelihood estimate of $\beta$.   

Practical applications of logit models include multiple parameters and many observations. Consequently, the maximum likelihood estimated for the parameters cannot be found graphically. Specialized soft ware packages are available for this purpose.



![likelihood](https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/2020713/likelihood.png)
![log_likelihood](https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/2020713/log_likelihood.png)   
<center>
Figure 1 Likelihood and Log-likelihood as a Function of a parameter Value.
</center>

* * *

## Course Link
- [CIV5305/6305: Basics and theory of discrete choice modelling 6.0](https://www.youtube.com/watch?v=aPdedMTiFzo&t=1365s)