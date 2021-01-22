---
layout: article
title: Algorithmic Thinking
key: 20201016
tags: Python
pageview: false
modify_date: 2020-10-16
aside:
  toc: true
---


<!--more-->

# Module 1 - Core Materials

## Five Steps of Algorithmic Thinking

- Understanding the problem. 
    - What are the input/output?
    - Do a few examples by hand.
    - Think about special cases.
- Formulating the problem. 
    - Think about the data and the best way to represent them (graphs, strings, etc.)
    - What mathematical criterion corresponds to the desired output?
- Developing an algorithm. 
    - Is the formulated problem amenable to a certain algorithm design
technique (greedy, divide-and-conquer, etc.)?
    - What data structures make sense to use? 
    - Is the algorithm correct? 
    - Is the algorithm efficient?
    - If the problem is “too hard,” do we want an approximation algorithm,
a randomized algorithm, a heuristic, ...? 
- Implementing the algorithm. 
    - Most algorithms are destined to be ultimately implemented as computer
programs.
    - The peril lies in the possibility of making the transition from an algorithm to a
program either incorrectly or very inefficiently. 
    - The opportunity lies in the possibility to better understand the
algorithm and even to improve it. 
- running it on the data and answering the original question.
    - Sometimes, it is discovered after this entire process is followed, that
the solution is not satisfactory. This might require going back to step
(1) and repeating the entire process. 

## Pseudo-code

[Pseudo-code syntax](https://storage.googleapis.com/codeskulptor-alg/pdf/PseudoCodeLibrary.pdf)

Pseudo-code is a high-level, abstract description of an algorithm that is intended to be read by humans and subsequently turned into a program in a programming language of choice. As such, pseudo-code provides the details needed to understand the algorithm, but omits many details that are left to the programmer to implement, since those may vary depending on the programming language and the choice of implementation.

## The small-world problem

![png]({{"/pictures/20201016/small-world_problem.png"}})

## Graphs and representation
[Graphs](https://storage.googleapis.com/codeskulptor-alg/pdf/GraphBasics.pdf)

## Brute force

[Brute Force Algorithms](https://storage.googleapis.com/codeskulptor-alg/pdf/BruteForceAlgorithms.pdf)

## Measuring efficiency

[Algorithm Efficiency](https://storage.googleapis.com/codeskulptor-alg/pdf/AlgorithmEfficiency.pdf)


### All Correct Algorithms Are Not Created Equal

Efficiency:
- Time: how fast an algorithm runs
- Space: how much extra space the algorithm requires
- There’s often a trade-off between the two. 

### It’s All a Function of the Input’s Size

- We often investigate the algorithm’s complexity (or, efficiency) in
terms of some parameter $n$ that indicates the algorithm’s input size
- For example, for an algorithm that sorts a list of numbers, the input’s size is the number of elements in the list.
- For some algorithms, more than one parameter may be needed to indicates the size of their inputs.
    - For the algorithm IsBipartite, the input size is given by the number
of nodes if the graph is represented as an adjacency matrix,
whereas the input size is given by the number of nodes and
number of edges if the graph is represented by an adjacency list. 

- Sometimes, more than one choice of a parameter indicating the input
size may be possible

- For an algorithm that multiplies two square matrices, one choice is n,
the order of the matrix, and another is N, the total number of entries
in the matrix.

- Notice that the relation between n and N is easy to establish, so
switching between them is straightforward (yet results in different
qualitative statements about the efficiency of the algorithm).

- When the matrices being multiplied are not square, N would be more
appropriate. 