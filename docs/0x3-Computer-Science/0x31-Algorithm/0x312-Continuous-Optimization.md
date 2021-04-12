# 0x312 Continuous-Optimization

- [1. Linear Programming](#1-linear-programming)
- [2. Convex Optimization](#2-convex-optimization)
- [3. Unconstrained Minimization](#3-unconstrained-minimization)
- [4. Equality Constrained Minimization](#4-equality-constrained-minimization)
- [5. Inequality Constrained Minimization](#5-inequality-constrained-minimization)
- [6. Nonlinear Optimization](#6-nonlinear-optimization)
- [7. Reference](#7-reference)

## 1. Linear Programming

## 2. Convex Optimization
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

## 3. Unconstrained Minimization

## 4. Equality Constrained Minimization

## 5. Inequality Constrained Minimization

## 6. Nonlinear Optimization

## 7. Reference

[1] Boyd, Stephen, Stephen P. Boyd, and Lieven Vandenberghe. Convex optimization. Cambridge university press, 2004.

