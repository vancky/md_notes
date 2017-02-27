---
title: Numerical Optimization -Introduction
date: 2017-02-23 10:48:27
tags: numerical, optimization
---
### Basic 
- Optimization : objective (profit,time,potential energy,anything else) , variables . The goal is to find values of the variables that optimize the objective.

- Variables: constrained or not .

- Modeling: identifying objective ,variables ,constraints for a given problem.

### Mathematical formulation: 
- $x$ vector of variables, also named parameters.

- $f$ objetive function , a function that we want to maximize of minimize.

- $c_i$ constraint function , $x$ must satisfy

  $ \min _{x\in  R^n} f(x)$  subject to    ${c_i =0;c_j \ge 0; i \in E;j \in I}$

### Classify
- continuous versus discrete 
- constrained and unconstrained
- global and local 
### Convexity
   Convex set :
- straight line segement connecting any two points is $S$ lies entirely inside $S$.
- for any $x\in S ,y \in S$ we have $\alpha x+(1-\alpha)y \in S$ for all $\alpha \in [0,1]$.


   Convex funtion:
-   domain set $S$ is convex set
-   for any $x\in S ,y \in S$ , $f$ satisfied :
     $f(\alpha x+(1-\alpha)y) \le \alpha f(x) + (1-\alpha)f(y)$ for all $\alpha \in [0,1]$.


 Convex programming or convex optimization 
- objective function is convex
- equality constraint function $c_i(),i \in E$ are linear
- quality constraint function $c_j(),j\in I$are concave
    Any  local solution of the proble is in fact a global solution  

