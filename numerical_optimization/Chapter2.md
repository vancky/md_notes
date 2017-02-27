---
title: Numerical Optimization -Chapter 2
date: 2017-02-23 12:25:27
tags: numerical, optimization
---
# Fundmentals of Unconstrained Optimization

Unconstrained optimization: 
$$\min_x f(x),x\in R^n , f:R^n -> R, n\ge 1$$
## 2.1 What is a solution?

Global minimizer : A point $x^* $ that satisfied $f(x^*)\le f(x)$ for all $x$. 
Local minimizer :
- weak : $\exists N , \forall x \in N,f(x^*)\le f(x)$,N is a neighborhood of $x^*$.
- strict : $\exists N , \forall x \in N,x\ne x^*f(x^*)< f(x)$
- isolated: $x^*$is the only local minimizer in $N$
### Local minimun with smooth function

- Taylor's Theorem $f(x+p)=f(x)+\nabla f(x+tp)^T p$
- First-Order Necessary Conditions  $\nabla f(x^*)=0$
- Second-Order Necessary Conditions  $\nabla f(x^*)=0$and $\nabla ^2 f(x^*)$is positive semidefinite
- Second-Order Sufficient Conditions $\nabla f(x^*)=0$and $\nabla ^2 f(x^*)$is positive definite
- When$ f$ is convex,any local minimizer $x^*$is a global minimizer . If in addition$ f$ is differentiable ,then any stationary point $x^*$is a global minimizer of $f$ .

## 2.2 Overview of algorithms

- All algorithms for unconstrained problem require a starting point $x_0$, by the user or the algorithm randomly.

- Beginning at $x_0$,algorithms generate a sequence of iterates $\{x_k\}^\infty _{k=0}$ .

- How to move from one $x_k$ to the next ? The algorithms uses information $f$ at $x_k$ or sometimes information from eariler iterates $x_0,x_1,...,x_{k-1}$ . Goal is $f(x_k)>f(x_{k+1})$(nonmonotone algorithms change 1 to constant m).

### Two strategies : line search and trust region

- line search strategy :
  choose a direction $p_k$ ,searches along this direction from $x_k$ for $x_{k+1}$ with lower function value. Solve a subproblem : 
  $$\min _{\alpha>0}f(x_k+\alpha p_k)$$

- trust region strategy:
  Construct a model funciton $m_k$ approximate $f$ at point $x_k$ within trust region . The goal is to find step $p$ by solving the subproblem:

  $$\min_p m_k(x_k+p), \text{where}  x_k+p \text{ belongs trust region}$$

  Usually ,the trust region is a ball defined by $||p| |_2\le \Delta$,the scalar $\Delta >0$ is called the trust-region radius. Sometimes ,elliptical and box-shaped trust regions may also be used. The model $m_k$ is defined to be a quadratic function  :

  $$m_k(x_k+p)=f_k+p^T\nabla f_k+\frac12p^T B_k p$$


  where$f_k,\nabla f_k$,and$B_k$are a scalar,vector,and matrix,respectively . The matrix $B_k$ is either the Hessian $\nabla ^2 f_k$or some approximation to it. 

### Search directions for line search methods

- Steepest descent direction :  $p_k=- \nabla f_k$ , this direction is orthogonal to the contours of the function .
  In general ,any direction makes an angle of strictly less than $\frac \pi 2$ with $-\nabla f_k$ is guaranteed to produce a decrese in $f$.

  Do not require second derivatives but sometimes can be excruciatingly slow on difficult problems. 


- Newton direction :  
   $$f(x_k+p) \approx f_k+p^T \nabla f_k +\frac 12 p^T \nabla^2 f_k p \equiv m_k(p)$$
  Assuming $\nabla ^2 f_k $ is positive definite, solving the subproblem $\min_p m_k(p)$ by setting the derivative of $m_k(p)$  to zero. we get 

  $$p_k^N=-(\nabla^2 f_k)^{-1}\nabla f_k$$

  Fast rate of local convergence , unsuitable when Hessian  is not positive definite and computation of Hessian can be cumbersome,error-prone and expensive .

- Quasi-Newton direction:
  Use $B_k$ approximates $\nabla^2f_k$ with the information from $g$ changes.From Taylor's theorem, we have (with adding $\nabla^2f(x)p$and subtracting it):
  $$\nabla f(x+p)=\nabla f(x)+\nabla^2f(x)p+\int_0^1[\nabla^2f(x+tp)-\nabla^2f(x)]p\mathrm{d}t$$

  By setting $x=x_k$ and $p=x_{k+1}-x_k$ ,we obtain

  $$\nabla f_{k+1}=\nabla f_k+\nabla^2f_k(x_{k+1}-x_k)+o(||x_{k+1}-x_k||) $$

  so we can write 

  $$\nabla^2f_k(x_{k+1}-x_k)\approx \nabla f_{k+1}-\nabla f_k$$

  we choose new Hessian approximation $B_{{k+1}}$ so that it satisfy the property of the true Hessian ,that is ,we require the secant equation:

  $$B_{k+1}s_k=y_k$$

  where 

  $$s_k=x_{k+1}-x_k, y_k=\nabla f_{k+1}-\nabla f_k$$

  Symmetirc-rank-one(SRI) formula:

  $$B_{k+1}=B_k+\frac{(y_k-B_ss_k)(y_k-B_ks_k)^T}{(y_k-B_ks_k)^Ts_k}$$

  BFGS formula:

  $$B_{k+1}=B_k+ \frac{B_k s_k s_k^T B_k}{s_k^TB_ks_k} +\frac{y_ky_k^T}{y_k^Ts_k}$$

  The quasi-Newton search direction is :

  $$p_k=-B_k^{-1}\nabla f_k$$

- Conjugation gradient direction :

  $$p_k=-\nabla f(x_k)+\beta_k p_{k-1}$$

  where $\beta_k$is a scalar that ensures the $p_k$ and $p_{k-1}$ are conjugate .

### Models for trust-region methods

  In trust-region subproblem , we set $B_k=0$  ,and define the trust region with Euclidean norm,then it becomes:

  $$\min_pf_k+p^T\nabla f_k , \text{subject to } ||p||_2\le\Delta_k$$

The solution is :

  $$p_k=-\frac{\Delta_k\nabla f_k}{||\nabla f_k||}$$

which is steepest descent direction is line search method.