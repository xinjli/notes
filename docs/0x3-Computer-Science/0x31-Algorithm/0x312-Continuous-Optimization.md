# 0x312 Mathematical-Optimization

- [1. Foundation](#1-foundation)
    - [1.1. Multivariable Optimization](#11-multivariable-optimization)
        - [1.1.1. Unconstrained Local Optimization](#111-unconstrained-local-optimization)
        - [1.1.2. Constrained Local Optimization](#112-constrained-local-optimization)
        - [1.1.3. Global Optimization](#113-global-optimization)
    - [1.2. Linear Programming](#12-linear-programming)
    - [1.3. Convex Optimization](#13-convex-optimization)
- [2. Unconstrained Minimization](#2-unconstrained-minimization)
- [3. Equality Constrained Minimization](#3-equality-constrained-minimization)
- [4. Inequality Constrained Minimization](#4-inequality-constrained-minimization)
- [5. Nonlinear Optimization](#5-nonlinear-optimization)
- [6. Reference](#6-reference)

## 1. Foundation
**Definition (optimization problems)** The optimization problems is formulated as follows:

$$ \text{minimize } f_0(x) \\
\text{subject to } f_i(x) \leq 0, h_j(x) = 0$$

where $f_0$ is the objective function, the inequality $f_i(x) \leq 0$ is inequality constraints, the equation $h_i(x)$ is called the equalit constraints. 

**Definition (optimal value, optimal point)** The *optimal value* $p^*$ is defined as

$$p^* = \inf \{ f_0(x) | f_i(x) \leq 0, h_j(x) = 0 \}$$

We say $x^*$ is an *optimal point* if $x^*$ is feasible and

$$f_0(x^*) = p^*$$

The set of optimal points is the *optimal set*, denoted

$$X_{opt} = \{ x| f_i(x) \leq 0, h_j(x)=0, f_0(x) = p^* \}$$

If there exists an optimal point for the porblem, the problem is said to be *solvable*.

### 1.1. Multivariable Optimization
**Definition (local minimum)** Let $f: D \subset \mathbb{R}^n \to \mathbb{R}$. We say $f$ has a *local minimum* of $f(a)$ at point $a$ in D if there exists an open ball with radius $\epsilon$ such that

$$\forall(x \in B_{\epsilon}(a) \cap D)f(x) \geq f(a)$$

#### 1.1.1. Unconstrained Local Optimization
First derivate test can be used to find all interior candidates for local extremum.
**Theorem (first derivative test, Fermat)** Let $f$ be a differentiable function from $D \subset \mathbb{R}^n \to \mathbb{R}$, suppose $f$ has a local extremum $f(a)$ at the interior point $a$, then the first partial derivatives of $f$ are zero at $A$

$$\nabla f(a) = 0$$

To decide the actual extremum within the candidates, the second derivative test is required.
**Theorem (Second derivative test)** Let $f \in C^{3}$  in an open set of $\mathbb{R}^n$ containing $a$. If $\nabla f(a)=0$ and Hessian is positive definite at $a$, then $f$ has a local minimum at $a$.

#### 1.1.2. Constrained Local Optimization
**Theorem (Lagrange Multiplier)** Any constrained critical point of the function $f$ on the domain $D=\{ g = 0 \}$ must be a point $a$ satifying either of

- $f$ is not differentiable at $a \in D$
- $\nabla g(a) = 0$
- $\nabla f(a) = \lambda \nabla g(a)$

The second condition is called the degeneracy condition, and the last condition is the Lagrange condition

#### 1.1.3. Global Optimization
To find the global extrema, devide the domain into subdomain and gather their critical points to find the actual global extrema. The existence of global extrema can be guaranteed by the continuous function and compact domain as mentioned in the previous section.

### 1.2. Linear Programming

### 1.3. Convex Optimization
A fundamental property of convex optimization problems is that any local optimal point is also global optimal

**Definition (convex optimization)** A convex optimization problem is of the form

$$\text{minimize } f_0(x)$$

$$\text{s.t. } f_i(x) \leq 0, a_i ^T = b_i$$

where $f_i$ are convex functions

**Criterion (optimality)** In the constrained problem. Suppose the objective $f_0$ is differentiable, then $x$ is optimal if $x \in X$ where $X$ is the feasible set

$$\forall(y \in X) \nabla f_0(x)^T (y-x) \geq 0$$

For an unconstrained problem, the condition reduces to the well known condition

$$\nabla f_0(x) = 0$$

**Definition (quadratic optimization, QP)** The convex optimization is called quadratic program (QP) if it can be expressed in the form

$$\text{minimize } \frac{1}{2} x^T P x + q^T x + r$$

$$\text{s.t. } Gx \preceq h, Ax = 0$$

where $P \in S^n_{+}$

**Definition (second-order cone programming, SOCP)** A second-order cone program (SOCP) has the following form

$$\text{minimize } f^T x$$

$$\text{s.t. } || A_i x + b_i ||_{2} \leq c_i^T x + d_i $$

**Definition (semidefinite programming, SDP)** When $K \in S^k_{+}$, the cone of positive semidefinite matrics, the associated conic form problem is called a semidefnite program (SDP)

$$\text{minimize }c^T x$$

$$\text{s.t. } x_1 F_1 + ... + x_n F_n + G \preceq 0, Ax = b$$

where $G, F_i \in S^k$

## 2. Unconstrained Minimization

## 3. Equality Constrained Minimization

## 4. Inequality Constrained Minimization

## 5. Nonlinear Optimization

## 6. Reference

[1] Boyd, Stephen, Stephen P. Boyd, and Lieven Vandenberghe. Convex optimization. Cambridge university press, 2004.

