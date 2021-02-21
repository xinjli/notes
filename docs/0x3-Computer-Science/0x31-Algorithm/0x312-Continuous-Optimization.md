# 0x312 Mathematical-Optimization

- [1. Foundation](#1-foundation)
- [2. Linear Programming](#2-linear-programming)
- [3. Convex Optimization](#3-convex-optimization)
    - [3.1. Convex Optimization Problems](#31-convex-optimization-problems)
- [4. Nonlinear Optimization](#4-nonlinear-optimization)

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

## 2. Linear Programming

## 3. Convex Optimization

### 3.1. Convex Optimization Problems
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



## 4. Nonlinear Optimization
