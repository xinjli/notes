# 0x023 Convex-Analysis

- [1. Convex Sets](#1-convex-sets)
    - [1.1. Affine Set](#11-affine-set)
    - [1.2. Convex Set](#12-convex-set)
        - [1.2.1. Operations that preserve convexity](#121-operations-that-preserve-convexity)
    - [1.3. Cone Set](#13-cone-set)
    - [1.4. Generalized Inequalities](#14-generalized-inequalities)
    - [1.5. Seperating and Supporting Hyperplanes](#15-seperating-and-supporting-hyperplanes)
    - [1.6. Dual Cones and Generalized Inequalities](#16-dual-cones-and-generalized-inequalities)
- [2. Convex Functions](#2-convex-functions)
    - [2.1. Basic Properties and Examples](#21-basic-properties-and-examples)
    - [2.2. Closedness and Semicontinuity](#22-closedness-and-semicontinuity)
    - [2.3. Operations that preserve convexity](#23-operations-that-preserve-convexity)
    - [2.4. The conjugate function](#24-the-conjugate-function)
- [3. Duality](#3-duality)
    - [3.1. Lagrange Dual Problem](#31-lagrange-dual-problem)
- [4. Reference](#4-reference)

## 1. Convex Sets
### 1.1. Affine Set
**Definition (affine set)** A set $C \subseteq R^n$ is affine if for any $x_1, x_2 \in C$, then $\theta x_1 + (1-\theta)x_2 \in C$ where $\theta \in R$

note: Affine set is a subspace plus an offset

**Definition (affine hull)** The affine hull of $C$ is the affine combination of all points in $C$. The affine dimension of $C$ is the dimension of its affine hull, which is the dimension of the underlying subspace

!!! example "solution set of linear equations"

    The solution set of a system of linear equations is an affine set

    $$\{ x | Ax=b \}$$


!!! example "hyperplane"

    A hyperplane is also a solution set of linear equation, therefore affine set

    $$\{ x | a^Tx =b \}$$

### 1.2. Convex Set

**Definition (convex set)** A set $C$ is convex if for any $x1,x2 \in C$, and any $0 \leq \theta \leq 1 $, then 

$$\theta x_1 + (1-\theta)x_2 \in C$$

**Definition (convex hull)** The convex hull of $C$ is the convex combination of all points in $C$

!!! example "halfspace"

    A halfspace is a convex set

    $$\{ x | a^T x \leq b\}$$

!!! example "ball and ellipsoid"

    A norm ball is a convex set

    $$\{ x | ||x-x_c|| \leq r \}$$

    A lreated family are ellipsoids, they are also convex

    $$\{ x | (x-x_c)^TP^{-1}(x-x_c) \leq 1 \}$$

!!! example "polyhedra and simplex"

    A polyhedron is defined as the solution set of a finite number of halfspaces and hyperplanes, therefore convex

    $$\{ x | Ax \preceq b, Cx=d \}$$

    Simplexes are an important family of polyhedra, it is defined with $k+1$ affinely independent points $v_0, ..., v_k$ (i.e. : $v_1-v_0, v_2-v_0, ...$ are independent), the simplex is given by their convex hull

    $$\{ \theta_0 v_0 + ... + \theta_k v_k | \theta \succeq 0, 1^T \theta = 1 \}$$


#### 1.2.1. Operations that preserve convexity
**Proposition (Intersection preserves convexity)** The intersection of any number of convex sets is a convex set

For example, polyhedron is the intersection of halfspaces and hyperplanes


!!! example "positive semidefinite cone"

    positive semidefinite cone can be expressed 

    $$\bigcap_{z \neq 0} \{ X \in S^n | z^T X z \geq 0 \} $$

    which is the intersection of infinite number of halfspaces $ \{ X \in S^n | z^T X z \geq 0 \}$, and so is convex

**Proposition (convex set and halfspaces)** a closed convex set $S$ is the intersection of all halfspaces that contain it

$$ S = \bigcap \{ H | H, S \subseteq H \} $$

**Proposition (Affine function preserves convexity)**  $y = Ax + b$ and its reverse preserves convexity, which means suppose $S \subset R^n$ is convex and $f: R^n \to R^m$ is an affine function, then the image and reverse image

$$f(S) = \{ f(x) | x \in S \}$$

$$f^{-1}(S) = \{ x | f(x) \in S \}$$

are both convex

!!! example "limear matrix inequality"

    Solution set of linear matrix inequality (LMI)

    $$A(x) = x_1 A_1 + ... + x_n A_n \preceq B$$

    is convex because it is the inverse image of the positive semidefinite cone under the affine function $f(x) = B - A(x)$

**Definition (perspective function)** The perspective function $P: R^{n+1} \to R^n$ with the domain $R^{n} \times R_{++}$ is 

$$P(z, t)=\frac{z}{t}$$

**Proposition (perspective function preserves convexity)** If $C \subset \text{dom}(P)$ is convex, then its image is convex

$$P(C) = \{ P(x) | x \in C \}$$

If $C \subset R^n$ is convex, then the inverse image is also convex

$$P^{-1}(C) = \{ (x, t) \in R^{n+1} | x/t \in C, t > 0 \}$$


**Definition (linear-fractional function)** The linear fractional function is the composition of perspective function with an affine function

$$f(x) = \frac{Ax + b}{c^Tx + d}$$
where $\text{dom }f = \{x | c^T x + d > 0 \}$

Affine function and linear function can be thought as the special cases of linear-fraction by setting $c=0$

**Proposition (Linear-fractional and perspective function preserve convexity)** The perspective functions, linear-fractional functions preserve convexity

### 1.3. Cone Set
**Definition (cone)** A set is cone if for every $x \in C, \theta \geq 0$ then $\theta x \in C$. A set is called convex cone if it is convex and cone

!!! example "norm cones"

    The norm cone is convex cone

    $$\{ (x,t) | ||x|| \leq t \}$$

**Definition (conic hull)** The conic hull of $C$ is the conic combination of all points in $C$

**Definition (proper cone)** A cone $K \subset R^n$ is called a proper cone if it satisfies the following:

-  convex
-  closed
-  solid (has noempty interiors)
-  pointed (contains no line)

!!! example "positive semidefinite cone"

    The set of symmetric positive semidefinite matrices is a proper cone

    $$S^n_{+} = \{ X | X = X^T, X \succeq 0 \}$$


### 1.4. Generalized Inequalities
**Definition (generalized inequality)** A generalized inequality defined with respect to a proper cone $K$ is a partial order

$$x \preceq_{K} y \iff y-x \in K$$

$$x \prec_{K} y \iff y-x \in K^{\circ}$$

The following two generalized inequalities are commonly used

!!! example "nonnegative orthant and componentwise inequality"

    The nonnegative orthant $K=R^n_{+}$ is a proper cone. The associated generalized inequality $\preceq_K$ is the componentwise inequality $(\forall{i})x_i \leq y_i$ 

!!! example "positive semidefinite cone and matrix inequality"

    The positive semidefinite cone is a proper cone. The associated inequality $\preceq_K$ means

    $$X \preceq_K Y \implies Y-X \in S^n_{+}$$

**Definition (minimum, maximum)** $x \in S$ is the minimum element of $S$ with respect to $\preceq_{K}$ if for all $y \in S$, $x \preceq_{K} y$

**Definition (minimal, maximal)** $x \in S$ is the minimal element of $S$ with respect to $\preceq_{K}$ if $y \preceq_{K} x $, then $y = x$

### 1.5. Seperating and Supporting Hyperplanes
**Theorem (separating hyperplane theorem)** Let $A,B$ be two disjoint convex set in $R^n$, there exists a nonzero vector $v$ 

and scalar $c$, such that for all $x \in A, y \in B$,

$$\langle x, v \rangle \geq c, \langle y, v \rangle \leq c$$

The converse, however, is not necessarily true: the existence of a separating hyperplane implies $A,B$ are disjoint.

We need additional constraints to make it true, for example, any two convex sets $A,B$, at least one of which is open, are disjoint iff there exists a separating hyperplane.

**Theorem (supporting hyperplane theorem)** For a non-empty convex set $C$ and its boundary point $x_0$, there exists a supporting hyperplane to $C$ at $x_0$

### 1.6. Dual Cones and Generalized Inequalities
**Definition (dual cone)** The following set $K^{*}$ is called the dual cone with respect to cone $K$

$$K^{*} = \{ y |(\forall{ x \in  K}) x^T y \geq 0 \}$$

Note that the dual cone of a subspace is the orthogonal complement of the subspace

**Properties (dual generalized inequalities)**
$x \preceq_K y \iff (\forall \lambda \preceq_{K^{*}} 0) \lambda^T x \leq \lambda^T y$
$x \prec_K y \iff (\forall \lambda \prec_{K^{*}} 0) \lambda^T x \leq \lambda^T y$
Criterion (dual characterization of minimum) $x$ is the minimum element of $S$ with respect to $K$ iff for every $\lambda \prec_{K^*} 0$, $x$ is the unique minimizer of $\lambda^T z$ over $z \in S$

**Criterion (dual characterization of minimal)** $x$ is the minimal element of $S$ with respect to $K$ iff $x$ minimizes a $\lambda^T x$ for a particular $\lambda \prec_{K^{*}} 0$

## 2. Convex Functions
### 2.1. Basic Properties and Examples
**Definition (Convex function)** A function $f: R^n \to R$ is convex if its domain is a convex set and for all $x, y \in dom(f), \theta \in [0, 1]$ we have

$$f(\theta x + (1-\theta) y) \leq \theta f(x) + (1-\theta)f(y)$$

Note that, convexity of the domain is a prerequisite for convexity of a function. When we call a function convex, we imply that its domain is convex

A function is strictly convex if strict inequality holds whenever $x \neq y \land \theta \in (0, 1) $

Similarly, a function $f$ is (strictly) **concave** iff $-f$ is (strictly) convex

!!! example "affine function"
    An affine function is a convex function whose form is

    $$f(x)=ax+b$$

!!! example "norm"
    A norm $|| \cdot ||$ is also an convex function become accoring to the triangle inequality, we have

    $$||\alpha x + (1-\alpha) y|| \leq \alpha ||x|| (1-\alpha) ||y||$$

!!! example "max function"

    The max function is convex on $R^n$
    $$f(x)= max \{ x_1, ..., x_n \}$$

!!! example "log-sum-exp"

    The log-sum-exp is convex on $R^n$

    $$f(x) = \log \sum_i e^{x_i}$$

!!! example "log-determinant"

    The log-det function is concave on $S^n_{++}$

    $$f(x) = \log\det X$$


**Corollary (convex $\land$ concave = affine)** all affine (and also linear) functions are both convex and concave, and vice versa

Under the assumption of differentiability, we have two equivalent statements of convexity.

**Criterion (1st order condition)** Suppose $f$ is differentiable. Then $f$ is convex iff $dom(f)$ is convex and

$$(\forall x, y \in dom(f)) f(y) \geq f(x) + f(x) + \nabla f(x)^T (y-x)$$

It states that the first taylor approximation is a global underestimator for convex function. Conversely , if the first Taylor approximation is aways a global underestimator, then the function is convex.

**Criterion (2nd order condition)** Suppose $f$ is twice differentiable, then $f$ is convex iff $dom(f)$ is convex and its Hessian is positive semidefinite

$$(\forall x \in dom(f)) \nabla^2 f(x) \succeq 0$$

**Definition (sublevel set, superlevel set)** The $\alpha$-sublevel set of $f: R^n \to R$ is defined as

$$C_\alpha = \{ x \in dom(f) | f(x) \leq \alpha  \}$$

**Corollary (sublevel set and convex)** Sublevel sets of a convex function are convex. Note that the converse is not true: a function can have all its sublevel sets convex, but not be a convex function. (e.g: $f(x) = e^{-x}$)

**Definition (epigraph)** The epigraph of a function $f: R^n \to R$ is defined as

$$\text{epi } f = \{ (x,t) | x \in dom(f), f(x) \leq t \}$$

$dom(f)$ can be seen as a projection of $epi(f)$.

**Theorem (epigraph and convexity)** A function is convex iff its epigraph is a convex set

Many results for convex functions can be proved geometrically by using epigraphs and apply results for convex sets.

''' info "convex set and indicator function"
    A convex set $X$ can also be mapped to a indicator function $\delta(x|X)$. 
    A set if convex iff its indicator function is convex

    $$\delta(x|X) = \begin{cases}0 & \text{ if }x \in X \\ \infty & \text{ otherwise} \end{cases}$$

### 2.2. Closedness and Semicontinuity
**Definition (closed function)** A function $f$ is a *closed* function if its epigraph is a closed set.

**Definition (semicontinuous)** A function $f$ is called lower semicontinuous at $x \in \mathcal{X}$ if

$$f(x) \leq \liminf_{k \to \infty} f(x_k) $$

for every sequence ${x_k} \subset \mathcal{X}$ with $x_k \to x$. We say that $f$ is lower semicontinuous at each point $x$ in its domain $\mathcal{X}$. Upper semicontinuous is defined that $-f$ is lower semicontinuous.



### 2.3. Operations that preserve convexity
**Proposition (nonnegative weighted sum)** Nonnegative weight sum of convex function is convex function

$$f = w_1 f_1 + ... + w_n f_m$$

**Proposition (affine mapping)** Affine mapping preserves convexity

$$g(x) = f(Ax + b)$$

Note this is the proof that least square problem is a convex problem

$$|| Ax - b ||^2_2$$


**Proposition (supremum)** If for each $y$, $f(x,y)$ is convex in $x$, then its supreme over $y$ is also convex

$$g(x) = \sup_{y} f(x,y)$$

**Proposition (composition)** Suppose $f(x) = h(g_1(x), ..., g_k(x))$ where $h: R^k \to R, g_i: R^n \to R$. $f$ is convex if $h$ is convex and nondecreasing in each argument, $g$ is convex

**Proposition (infimum)** If $f$ is convex in $(x,y) $ and $C$ is a convex nonempty set, then the function $g$ is convex  if some $g(x) > -\infty$

$$g(x) = \inf_{y \in C} f(x,y) $$

Notice the difference between previous sup and inf: the inf requires $y$ to be minimized over a convex set where sup does not require anything.

!!! example "distance to a set"

    The distance of a point $x$ to a set $S$ is defined as

    $$dist(x, S) = \inf_{y \in S} ||x - y||$$

    This function is convex

**Proposition (perspective of a function)** If $f: R^n \to R$, then the perspective function of $f$ is the function $g: R^{n+1} \to R$ defined by

$$g(x, t) = t(fx/t)$$

with domain

$$\{ (x,t) | x/t \in dom(f), t  > 0 \}$$

!!! example "euclid norm squared"

    The perspective function on $f(x)=x^Tx$ is convex

    $$g(x, t) = x^Tx/t$$

### 2.4. The conjugate function
**Definition (conjugate function)** Let $f: R^n \to R$. The function $f*: R^n \to R$, defined as

$$f^*(y) = \sup_{x \in \text{dom} f }  (y^T x - f(x))$$

The domain of conjugate function consists of $y \in R^n$ for which the sup is bounded.

Conjugate function $f*$ is a convex function because it is taking sup over a affine function of $y$. This is true regardless of $f$'s convexity.

!!! example "conjugate of convex quadratic function"

    The conjugate of $f(x) = \frac{1}{2}x^TQx$ with $Q$ positive definite, then

    $$f^*(y) = \frac{1}{2}y^*Q^{-1}y$$


!!! example "conjugate of indicator function"

    The conjugate of indicator function f a set $S$, i.e $I(x) = 0$ with $dom(I)=S$ is the support function of $S$

    $$I^*(y) = \sup_{x \in S} y^Tx$$


!!! example "conjugate of log-sum-exp"

    The conjugate of log-sum-exp $f(x) = \log (\sum_i e^{x_i})$ is the negative entropy function

    $$f^*(y) = \sum_i y_i \log(y_i)$$

    with the domain restricted to the probability simplex.

**Corollary (Fenchel's inequality)** from the conjugate definition, it is obvious that

$$(\forall(x, y)) f(x) + f^*(y) \geq x^Ty$$

**Lemma (conjugate's conjugate)** If $f$ is convex and closed, then

$$f^{**} = f$$



## 3. Duality
### 3.1. Lagrange Dual Problem
**Definition (Lagrangian)** The Lagrangian $L: R^n \times R^m \times R^p \to R$ associated with the standard form optimization problem is

$$L(x, \lambda, \nu) = f_0(x) + \sum_{i=1}^m \lambda_i f_i(x) + \sum_{i=1}^{p} \nu_i h_i(x)$$

$\lambda$ is called the Lagrange multiplier and $\nu$ is called dual variables. Domain $\mathcal{D} = \mathrm{dom} f_i \cap \mathrm{dom} h_i$

**Definition (dual function)** The Lagrange dual function is the minimum value over $x$

$$g(\lambda, \nu) = \inf_{x \in \mathcal{D}} L(x, \lambda, \nu)$$

Dual function over $(\lambda, \nu)$ is concave even the original problem is not convex. 

One of the motivations of Lagrangian is to gives the lower bound on the optimal value of the original problem.

$$g(\lambda, \nu) \leq p*$$

**Definition (dual problem)** The Lagrange dual problem associated with the primal problem is a convex optimization problem even the primal problem is not

$$\text{maximize } g(\lambda, \nu) $$

$$\text{subject to } \lambda \succeq 0 $$

Dual feasible means there exists a pair $(\lambda, \nu)$ such that $\lambda \succeq 0, g(\lambda, \nu) > -\infty$. We refer to $(\lambda^*, \nu^*)$ as dual optimal if they are optimal for the dual problem

The dual problem is always a convex optimization problem even the primal problem is not convex

**Proposition (weak duality)** The optimal value of the dual problem, denoted $d^*$ is by definition, the best lower bound on the optimal value of the primal problem $p^*$, therefore

$$d^* \leq p^*$$

This property is called the weak duality

**Proposition (strong duality and Slater's condition)** The strong duality holds when the optimal duality gap is zero

$$d^* = p^*$$

The strong duality does not always hold, one of condition to make it hold is the Slater's condition such that there exists a strictly feasible point

$$f_i(x) < 0$$

**Definition (proof, certificate)** If we can find a dual feasible $(\lambda, \nu)$, we establish a lower bound on the optimal value of the primal problem: $p^* \geq g(\lambda, \nu)$. Then the point provides proof or certificate that  $p^* \geq g(\lambda, \nu)$

**Criterion (Karush-Kuhn-Tucker, KKT)** Let $x^*, (\lambda^*, \nu^*)$ be any primal and dual optimal points with zero duality gap. Then

$$ f_i(x^*) \leq 0 $$

$$h_i(x^*) = 0$$

$$\lambda^* \geq 0$$

$$\lambda^* f_i(x^*) = 0$$

$$ \nabla f_0 (x^*) + \sum_{i=1}^m \lambda^* \nabla f_i(x^*) + \sum_{i=1}^p \nu_i^* \nabla h_i (x^*) = 0 $$

If a convex optimization problem with differentiable objective and constraint functions satisfies Slater's condition, then the KKT conditions provide necessary and sufficient conditions for optimality

## 4. Reference
[1] Boyd, Stephen, and Lieven Vandenberghe. Convex optimization. Cambridge university press, 2004.

[2] Bertsekas, Dimitri P. Convex optimization theory. Belmont: Athena Scientific, 2009.