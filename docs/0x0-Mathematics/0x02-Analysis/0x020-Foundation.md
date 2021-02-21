# 0x020 Mathematical Analysis

- [1. Continuity](#1-continuity)
  - [1.1. Limits of Functions](#11-limits-of-functions)
    - [1.1.1. Criterions](#111-criterions)
  - [1.2. Continuity](#12-continuity)
    - [1.2.1. Criterions](#121-criterions)
    - [1.2.2. Continuity and Compactness](#122-continuity-and-compactness)
    - [1.2.3. Continuity and Connectedness](#123-continuity-and-connectedness)
  - [1.3. Uniform Continuity](#13-uniform-continuity)
  - [1.4. Lipschitz continuity](#14-lipschitz-continuity)
- [2. Differentiation](#2-differentiation)
  - [2.1. Real-value derivatives](#21-real-value-derivatives)
  - [2.2. Multivariate Differentiability](#22-multivariate-differentiability)
  - [2.3. Smoothness](#23-smoothness)
    - [2.3.1. Differentiability and Continuity](#231-differentiability-and-continuity)
    - [2.3.2. Differentiability and Continuously Differentiability](#232-differentiability-and-continuously-differentiability)
  - [2.4. Mean Value Theorem](#24-mean-value-theorem)
  - [2.5. Extrema of functions](#25-extrema-of-functions)
    - [2.5.1. Unconstrained Local Optimization](#251-unconstrained-local-optimization)
    - [2.5.2. Constrained Local Optimization](#252-constrained-local-optimization)
    - [2.5.3. Global Optimization](#253-global-optimization)
- [3. Riemann Integral](#3-riemann-integral)
  - [3.1. Partitions](#31-partitions)
  - [3.2. Integrability](#32-integrability)
  - [3.3. Properties of the Integral](#33-properties-of-the-integral)
  - [3.4. Fundamental Theorem of Calculus](#34-fundamental-theorem-of-calculus)
- [4. Reference](#4-reference)

Analysis is the art of taking limits.

## 1. Continuity
continuously differentiable < Lipschitz continuous < uniform continuous < continuous

### 1.1. Limits of Functions
Generally speaking, we want the value of $\lim_{x \to c} f(x)$ to be independent of how we approach $c$

**Definition (functional limit)** Suppose $x_0$ is a limit point of $E$, 
$$\lim_{x \to x_0; x \in E} f(x) = L$$
iff 
$$(\forall \epsilon > 0)(\exists \delta > 0)(\forall{x}:  0 < |x - x_0 | < \delta \land x \in E) |f(x) - L| \leq \epsilon$$

It looks there are two version of functional limit definitions, the definition here is called the deleted limit version where the $x = x_0$ is excluded from the requirements, the other version is called the non-deleted limit version where $x = x_0$ can be included

$$ (\forall x: |x-x_0 | < \delta \land x \in E) |f(x) - L| \leq \epsilon$$

These two definitions are have slightly different conclusions sometimes. This note will follow the deleted version.

It is important to remember that limit points of $E$ do not necessarily belong to $E$ unless it is closed. In fact, $x_0$ need not to be in the domain of $f$. 

!!! note "Example" 
    In the function $f(x) = x \sin(1/x)$ with $x>0$, $x=0$ is not included in the domain but $x=0$ is a limit point, so the limit on $0$ can exist

    $$\lim_{x \to 0} x \sin(\frac{1}{x}) = 0$$

#### 1.1.1. Criterions

As mentioned above, the functional limit should be independent how we approach the limit point, therefore all sequence limit should converges to the same point.
**Criterion (sequence criterion)** the following statements are equivalent

- $ \lim_{x \to x_0; x \in E} f(x) =  L$
- $(a_n) \to x_0 \implies f(a_n) \to L$ where $a_n \in E$

This also gives us an approach to decide the divergence
**Criterion (divergence)** functional limit $\lim_{x \to c} f(x)$ does not exist if
$$\lim_{x_n} = \lim_{y_n}.= c \land \lim f(x_n) \neq \lim f(y_n)$$

**Criterion (Algebraic Limit Theorem)** limit laws for functions

$$\lim_{x \to x_0} (f  \pm g)(x) = \lim_{x \to x_0} f(x) \pm \lim_{x \to x_0} g(x)$$

$$\lim_{x \to x_0} \min(f, g)(x) = \min (\lim_{x \to x_0} f(x),  \lim_{x \to x_0} g(x))$$

$$\lim_{x \to x_0} \max(f, g)(x) = \max(\lim_{x \to x_0} f(x), \lim_{x \to x_0} g(x))$$

$$\lim_{x \to x_0} (f g)(x) = \lim_{x \to x_0} f(x) \lim_{x \to x_0} g(x)$$

$$\lim_{x \to x_0} (f / g)(x) = \frac{\lim_{x \to x_0} f(x)}{\lim_{x \to x_0} g(x)}$$

In the case of multivariable input and single output function, it is a bit tricky. Even limits along all lines exists and have the same value, the continuity still might not exist

**Counter example (line limits does not guarantee limit)** Define the function $f$

$$f = \frac{||x||}{\theta(x)}$$
where $\theta(x)$ is the angle measured from the positive part. All line limits is 0, but when taking curve limit $||x||=\theta(x)$, then the curve limit is 1.

Again to make sure functional limit exist, ALL sequence limit should exist and equal not only line limits.


**Proposition (limits are local)** the following statements are equivalent

$\lim_{x \to x_0; x \in E} f(x) = L$
$(\forall \delta \in R) \lim_{x \to x_0; x \in E \cup (x - \delta, x+\delta)} f(x) = L$

**Proposition (multivariable convergence)** Suppose $U \subset \mathbf{R}^n$, $f=(f_1, ..., f_m): U \to \mathbf{R}^m$ and $x_0 \in \bar{U}$, then

$$\lim_{x \to x_0} f(x) = (a_1, ..., a_m)$$

is equivalent to
$$(\forall{i: 1 \leq i \leq m}) \lim_{x \to x_0} f_i(x) = a_i$$


### 1.2. Continuity
The continuity class can be organized as follows:

$$\text{ Continuously Differentiable } \subset \text{ Lipschitz Continuous } \subset \text{ Uniformly Continuous } \subset \text{ Continuous } \subset \text{ Well-Defined } $$

**Definition (Continuity)** $f: X \to R$ is continuous at $x_0 \in X$ iff

$$ \lim_{x \to x_0; x \in X} f(x) = f(x_0)$$

Continuous function preserves the convergence (i.e. : $x_n \to x_o \implies f(x_n) \to f(x_o)$)

The most important point here is that the point $x_0$ has to be in the domain of $f$


**Definition (Discontinuity)** There are three types of discontinuity
- If $\lim_{x \to c} f(x)$ exists but has a value different from $f(c)$, the discontinuity is called *removable*
- If $\lim_{x \to c+} f(x) \neq \lim_{x \to c-} f(x)$, then $f$ has a *jump discontinuity* at c
- If $\lim_{x \to c}$ does not exist for other reasons, the discontinuity is called *essential*

!!! note "nowhere continuous function"
    Dirichlet's function is an example of nowhere continuous function

    $$f(x) = \begin{cases} 1 & \text{ if } x \in Q \\ 0 & \text{ if } x \not\in Q \end{cases}$$


#### 1.2.1. Criterions

**Criterion (Arithmetic operations and composition)** if $f, g$ are continuous at $x_0$, then $f+g, f-g, f/g, fg, \min(f,g), \max(f,g), g \circ f$ are also continuous at $x_0$

In the case of single variable, we can define the left, right limits and use them to determine continuity.
**Definition (left, right limits)** 
$$(\forall x_0 \in \overline{X \cap (x_0, \infty)}) f(x_0 +) := \lim_{x \to x_0; x \in X  \cap (x_0, \infty)} f(x)$$

$$(x_0 \in \overline{X \cap (-\infty, x_0)}) f(x_0 -) := \lim_{x \to x_0; x \in X  \cap (-\infty, x_0)} f(x)$$

**Criterion (left right limits and continuity)** If $f(x_0+), f(x_0-)$ both exist and equal to $f(x_0)$, then $f$ is continuous at $x_0$


Continuity has multiple good properties, for example, it preserves compactness and connectedness, which guarantees the continuous function has extreme value and intermediate value under certain conditions.

#### 1.2.2. Continuity and Compactness
**Theorem (preservation of compact sets)** Let $f: A \to R$ be continuous on $A$. If $K \subseteq A$ is compact, then $f(K)$ is compact as well

**Proposition (extreme value theorem)** If $f: A \to R$ is continuous on a compact set $K\ subset R$, then $f$ attains a maximum and mimum value.

#### 1.2.3. Continuity and Connectedness
**Theorem (preservation of connected sets)** Let $f: G \to R$ be continuous. If $E \subseteq G$ is connected, then $f(E)$ is connected as well

**Theorem (Intermediate value theorem)** Let $f: [a,b] \to R$ be a continuous function on $[a,b]$. Let $y$ be a real number between $f(a), f(b)$. Then there exists $c \in [a,b]$ such that $f(c)=y$

Conversely, a function having the intermediate value property does not necessariy need to be continuous.

### 1.3. Uniform Continuity
continuity is a local property, but uniform continuity is a global property

**Definition (uniform continuity)** Let $X \subset R$ and let $f: X \to R$. We say that $f$ is uniformly continuous if

$$(\forall \epsilon > 0) (\exists \delta > 0) (\forall |x-x_0| < \epsilon) |f(x)-f(x_0)|<\delta$$

**Definition (equivalent sequences)** Let $m$ be an integer . Let $(a_n)_{n=m}^{\infty}, (b_n)_{n=m}^{\infty}, $ be two sequences of real numbers, and let $\epsilon > 0$ be given. 

($\epsilon$-close) We say that $(a_n)_{n=m}^{\infty}$ is $\epsilon$-close to $(b_n)_{n=m}^{\infty}$ iff $a_n$ is $\epsilon$-close to $b_n$ for each $n \geq m$.
(eventually $\epsilon$-close) We say that $(a_n)_{n=m}^{\infty}$ is eventually $\epsilon$-close to $(b_n)_{n=m}^{\infty}$ iff there exists an $N \geq m$ such that the sequences $(a_n)_{n=N}^{\infty}$ and $(b_n)_{n=N}^{\infty}$ are $\epsilon$-close.
(equivalent sequences) Two sequences $(a_n)_{n=m}^{\infty}, (b_n)_{n=m}^{\infty}$ are equivalenet iff for each $\epsilon > 0$, the sequences are eventually $\epsilon$-close.
Lemma Real sequences of $(a_n)_{n=1}^{\infty}, (b_n)_{n=1}^{\infty}$ are said to be equivalent iff $\lim_{n \to \infty} (a_n - b_n) = 0$

**Proposition (uniformly continuity and sequences)** following are logically equivalent

$f: X \to R$ is uniformly continuous on $X \subset R$
Whenever $(x_n)_{n=1}^{\infty}, (y_n)_{n=1}^{\infty}$ are two equivalent sequences consisting of elements of $X$, the sequences $(f(x_n))_{n=1}^{\infty}, (f(y_n))_{n=1}^{\infty}$ are also equivalent

**Proposition (uniform continuity preserves Cauchy sequences)** if $f$ is a uniformly continuous function. Let $(x_n)_{n=1}^{\infty}$ be a Cauchy sequence. Then $(f(x_n))_{n=1}^{\infty}$ is also Cauchy

**Theorem (compact continuous function is uniformly continuous)** If $f: A \to R$ is continous on a compact set $A$. Then $f$ is also uniformly continuous

### 1.4. Lipschitz continuity
**Definition (Lipschitz continuity)** A function $f: A \to R$ is called Lipschitz if there exists a bount $M > 0$ such that for all $x, y \in A, x \neq y$

$$|\frac{f(x)-f(y)}{x-y} | \leq M$$

Lemma Lipschitz continuous implies uniform continuous

**Example (contraction mapping)** A contractive function is a function

$$|f(x) - f(y)| \leq c |x-y|$$

where $0 < c < 1$. It is a Lipschitz continuous function

## 2. Differentiation
### 2.1. Real-value derivatives
**Definition (differentiability at a point)** Let $X$ be a subset of $\mathbb{R}$, $x_0 \in X$ which is a limit point of $X$, $f: X \to \mathbb{R}$. If the limit

$$\lim_{x \to x_0; x \in X \setminus \{ x_0 \}} \frac{f(x)-f(x_0)}{x - x_0}$$

converges to some real number $L$, we say that $f$ is differentiable at $x_0$ on $X$ with derivative $L$ and write $f'(x_0) := L$. Otherwise $f'(x_0)$ is undefined and $f$ is not differentiable at $x_0$. 

Differentiability is a local property with respect to a point

**Definition (differentiability on domain)** Let $X$ be a subset of $R$ and let $f: X \to R$ be a function. $f$ is differentiable on $X$ iff $f$ is differentiable at every limit point $x_0 \in X$

**Proposition (Newton's approximation)** Let $X$ be a subset of $\mathbb{R}$, let $x_0 \in X$ be a limit point of $X$, let $f: X \to \mathbb{R}$ a function and $L$ be a real number. Following statements are logically equivalent:

$f$ is differentiable at $x_0$ on $X$ with derivative $L$

for every $\epsilon > 0$ there exists a $\delta > 0$ such that $f(x)$ is $\epsilon |x-x_0|$-close to $f(x_0) + L(x-x_0)$ whenever $x \in X$ is $\delta$-close to $x_0$

$$(\forall x |x-x_0| \leq \delta) |f(x) - (f(x_0) + L(x-x_0))| \leq \epsilon |x-x_0|$$


### 2.2. Multivariate Differentiability
**Definition (directional derivative)** Let $E$ be a subset of $\mathbb{R}^n$, $f: E \to \mathbb{R}^m$ be a function, let $x_0$ be an interior point of $E$, and let $v$ be a vector in $R^n$. If the limit

$$\lim_{t \to 0; t>0; x_0+tv \in E} \frac{f(x_0+tv) - f(x_0)}{t}$$

exists, we say $f$ is differentiable in the direction $v$ at $x_0$, and we denote the above limit by $D_v f(x_0) \in \mathbb{R}^m$

$$(D_v) f (x_0) = \lim_{t \to 0; t>0}\frac{f(x_0+tv)-f(x_0)}{t}$$

**Lemma** Suppose $f(x)=(f_1(x), f_2(x), ..., f_n(x))$, then $f$ is directional differentiable with $e$ is equivalent to the statement that for all $i$, $f_i$ is directional differentiable with $e$.

Directional Derivative is scalar multiplicative, the derivative of $ku$ direction is $k$ times the derivative of $u$ direction.
$$D_{ku} f(a) = kD_u f(a)$$

**Definition (directional linear)** A function is called directional linear, iff there exists a linear transformation that can be used to compute all directional derivatives at that point

$$D_v f(a) = L(v)$$

**Definition (partial derivative)** Let $E$ be a subset of $\mathbb{R}^n$, $f: E \to \mathbb{R}^m$ and $x_0$ is an interior point of $E$, $1\leq j \leq n$. Then the partial derivative of $f$ with respect to $x_j$ variable at $x_0$, denoted $\frac{\partial f}{\partial x_j}(x_0)$ is defined by

$$\frac{\partial f}{\partial x_j}(x_0) = \lim_{t \to 0; t \neq 0; x_0 + te_j \in E} \frac{f(x_0+te_j)-f(x_0)}{t}$$

Next, we think about the differentiability for the multivariable function, the definition of differentiability for one variable cannot be directly to multivariable function $f: R^n \to R^m$ because the denominator and nominator are vectors of different dimension.

$$\lim_{x \to x_0} \frac{f(x)-f(x_0)}{x-x_0}$$

Instead of this definition, we interpret that $f$ is approximately linear near $x_0$, which $f(x) \approx f(x_0) + L(x-x_0)$, then the previous definition can be defined as

$$\lim \frac{|f(x) - (f(x_0)+L(x-x_0))|}{|x-x_0|} = 0$$

where the denominator and nominator are both scalar, this definition can be applied in the multivariable function as follows.

**Definition ((total) differentiability)** Let $E$ be a subset of $R^n$, $f: E \to R^m$ be a function. $x_0 \in E$ be a point, let $L: R^n \to R^m$ be a linear transformation. We say $f$ is differentiable at $x_0$ with derivative $L$ if we have 

$$\lim_{x \to x_0; x \in E - x_0} \frac{|| f(x) - (f(x_0)+L(x-x_0))|| }{|| x-x_0||} = 0$$

where $L$ is called the total derivative or Jacobian matrix.

For a differentiable function, 

$$L(v) = D_v f(a)$$

Not differentiability implies directional linear, but directional linear does not imply differentiability.

Note the total differentiability is corresponding to the standard differentiability in one variable.

**Definition (Jacobian matrix)** The Jacobian matrix is defined as 
$$\mathbf J = \begin{bmatrix}
    \dfrac{\partial \mathbf{f}}{\partial x_1} & \cdots & \dfrac{\partial \mathbf{f}}{\partial x_n} \end{bmatrix}
= \begin{bmatrix}
    \dfrac{\partial f_1}{\partial x_1} & \cdots & \dfrac{\partial f_1}{\partial x_n}\\
    \vdots & \ddots & \vdots\\
    \dfrac{\partial f_m}{\partial x_1} & \cdots & \dfrac{\partial f_m}{\partial x_n} \end{bmatrix}$$

**Definition (Jacobian)** Jacobian matrix is a square matrix when $m=n$, Its determinant is called the Jacobian determinant, or simply the Jacobian.

The Jacobian at a given point gives important information about the behavior of $f$ near the point. For example, the continuously differentiable function $f$ is invertible near $p$ when the Jacobian determinant at $p$ is non-zero, which is known as the inverse function theorem


### 2.3. Smoothness
In general, the differentiability class can be organized as follows:

$$ \text{continuously differentiable function }C^1 \subset \text{differentiable function} \subset \text{ directional defferentiable } \subset \text{ partial differentiable } $$

**Definition (class $C^k, C^{\infty}$)** The class $C^k$ is a set of function $f$ where its derivatives $f', f'', ..., f^{(k)}$ exist and are continous. It is said to be in the class $C^{\infty}$ or **smooth**, if The function has deriavtives of all orders.

A related concept is analytic function. For any $C^{\infty}$ function, a Taylor seris is defined at arbitrary points, but its neighbor is not guaranteed to converge. To gaurantee convergence, it needs to be an analytic function.

**Definition (analytic function, $C^{\omega}$)** An analytic function is a function that is locally given by a convergent power series.

Note Analytic function is a strictly subset of smooth function, there are smooth functions that are not analytic function. Details will be given in the seris section.
$$\text{ Analytic function } C^{\omega} \subset \text{ smooth function } C^{\infty}$$

#### 2.3.1. Differentiability and Continuity

**Counter Example (continuous but not differentiable)** The easy example is the absolute value function where 0 is not differentiable. Weierstrass has a even function where continuous but nowhere differentiable

$$f(x) = \sum_{n=0}^{\infty} a^n \cos(b^nx)$$

where $a,b$ are carefully chosen.

Derivative functions might not be continuous, but it will satisfy the intermediate value properties as follows

**Theorem (Darboux)** If $f$ is differentiable on an interval $[a,b]$, and if $\alpha$ satisfies $f'(a) < \alpha < f'(b)$, then there exists a point $c \in (a,b)$ where $f'(c) = \alpha$


#### 2.3.2. Differentiability and Continuously Differentiability

Being differentiable does not guarantee its derivative is continuous, showing 

$$ \text{ differentiable } \not\!\!\!\!\implies \text{ continuous differentiable }$$

Here is the famous example

!!! example "differentiable everywhere but has discontinuity"

    Consider the following function

    $$f(x) = \begin{cases} x^2 \sin(1/x) \text{ if } x > 0 \\ 0 \text{ if } x =0 \\ \end{cases}$$

    It is differentiable everywhere, the derivative is given by

    $$ f'(x) = \begin{cases} -\cos(1/x) + 2x \sin(1/x) \text{ if } x > 0 \\ 0 \text{ if } x=0 \\ \end{cases}$$ 
    
    However, it has the discontinuity at 0 which is an *essential* discontinuity

On the other hand, continuous derivatives implies the continuous differentiability and of course differentiability.

$$ \text{ continuous differentiable } \implies \text{ differentiable }$$

**Proposition (continuous partial implies continuous total differentiability)** If all the partial derivatives $\frac{\partial f}{\partial x_j}$ exists and continuous on $x_0$, then $f$ is differentiable at $x_0$ and the linear transformation $f'(x_0)$ is defined by

$$f'(x_0)(v_j)_{1\leq j \leq n} = \sum_j v_j \frac{\partial f}{\partial x_j}(x_0)$$

However, simple existence of partial derivatives does NOT imply total differentiability.
**Counter Example (existence of all partial does NOT imply even continuity)** Consider the following case
$$f(x, y) = \begin{cases} \frac{xy}{x^2+y^2} \text { if } (x,y) \neq (0,0) \\ 0 \text{ if } (x,y) = (0,0) \end{cases}$$

In this case, partial derivative exists for $x,y$, but it is not even continuous. of course not differentiable nor continuously differentiable.

**Theorem (mixed partial derivative are equal in $C^2$ )** For a twice continuously differentiable function $f$, the mixed second partial derivatives are equal:

$$f_{xy} = f_{yx}$$


### 2.4. Mean Value Theorem
**Theorem (Rolle)** Let $a<b$ be real numbers, and let $g: [a,b] \to R$ be a continuous function which is differentiable on $(a,b)$. Suppose also that $g(a)=g(b)$. Then there exists an $x \in (a,b)$ such that $g'(x) = 0$

**Theorem (mean value theorem)** If $f: [a,b] \to R$ is continuous on $[a,b]$ and differentiable on $(a,b)$, then there exists a point $c \in (a,b)$ where

$$f'(c) = \frac{f(b)-f(a)}{b-a}$$

**Theorem (generalized mean value theorem)** If $f, g$ are continuously on the closed interval $[a,b]$ and differentiable on the open interval $(a,b)$, then there exists a point $c \in (a,b)$ where

$$[f(b) - f(a)]g'(c) = [g(b) - g(a)]f'(c)$$


### 2.5. Extrema of functions
**Definition (local minimum)** Let $f: D \subset \mathbb{R}^n \to \mathbb{R}$. We say $f$ has a *local minimum* of $f(a)$ at point $a$ in D if there exists an open ball with radius $\epsilon$ such that

$$\forall(x \in B_{\epsilon}(a) \cap D)f(x) \geq f(a)$$

#### 2.5.1. Unconstrained Local Optimization
First derivate test can be used to find all interior candidates for local extremum.
**Theorem (first derivative test, Fermat)** Let $f$ be a differentiable function from $D \subset \mathbb{R}^n \to \mathbb{R}$, suppose $f$ has a local extremum $f(a)$ at the interior point $a$, then the first partial derivatives of $f$ are zero at $A$

$$\nabla f(a) = 0$$

To decide the actual extremum within the candidates, the second derivative test is required.
**Theorem (Second derivative test)** Let $f \in C^{3}$  in an open set of $\mathbb{R}^n$ containing $a$. If $\nabla f(a)=0$ and Hessian is positive definite at $a$, then $f$ has a local minimum at $a$.

#### 2.5.2. Constrained Local Optimization
**Theorem (Lagrange Multiplier)** Any constrained critical point of the function $f$ on the domain $D=\{ g = 0 \}$ must be a point $a$ satifying either of

- $f$ is not differentiable at $a \in D$
- $\nabla g(a) = 0$
- $\nabla f(a) = \lambda \nabla g(a)$

The second condition is called the degeneracy condition, and the last condition is the Lagrange condition

#### 2.5.3. Global Optimization
To find the global extrema, devide the domain into subdomain and gather their critical points to find the actual global extrema. The existence of global extrema can be guaranteed by the continuous function and compact domain as mentioned in the previous section.

## 3. Riemann Integral
Historically, the concept of integration was defined as the inverse process of differentiation. This approach, however, is unsatisfying because it results in a very limited number of functions that can be limited. For example, any function with a jump discontinuity cannot be integrated (because of Darboux's Theorem). Around 1850 in the work of Cauchy and Riemann, integration start to use the notion of area under the curve as a starting point for building rigorous definition of the integral.

The major function classes related to Riemann integral can be classified as follows. Note that integrable family is boarder than continous, but differentiable function is more narrow than continuous function.

$$ \text{Continuous }\subset \text{ Piecewise continuous }\subset\text{ Continuous almost everywhere }\subseteq\text{ Riemann Integrable }$$

!!! example "counter example (integrable vs antidifferentiable)"
    Note that integrable function and function can be taken antiderivative are not equivalent. For example, the following example is integrable but not antidifferentiable.

    $$ f(x) =
    \begin{cases}
    0 & \text{ for } x < 0 \\
    1 & \text{ for } x \geq 0 \\
    \end{cases}
    $$

The class of functions whose Antiderivative exists falls somewhere between the previous hierarchy, because every continuous function has antiderivative (guaranteed by the fundamental theorem), and function with antiderivative can be integrable, but not every integrable function has antiderivative. Note there are also some examples where functions are not continuous but has antiderivative.

### 3.1. Partitions
**Definition (length of intervals)** If $I$ is a bounded interval, we define the length of $I$, denoted $|I|$. If $I$ is one of tthe intervals $[a,b], (a,b), [a,b), (a,b]$ for some real numbers $a<b$, then we define $|I| := b-a$. Otherwise if $I$ is a point or the empty set, we define $|I|=0$

**Definition (Partitions)** Let $I$ be a bounded interval. A partition of $I$ is a finite set $P$ of bounded intervals contained in $I$, such that every $x \in I$ lies in exactly one of the bounded intervals $J \in P$

**Theorem (length is finitely additive)** Let $I$ be a bounded interval, n be a natural number, and let $P$ be a partition of $I$ of cardinality $n$ Then 

$$|I| = \sum_{J \in P} |J|$$

**Definition (finer and coarser partitions)** Let $I$ be a bounded interval, $P, P'$ be two partitions of $I$. We say that $P'$ is finer than $P$ if for every $J \in P'$, there exists a $K \in P$ such that $J \subseteq K$

**Definition (common refinement)** Let $I$ be a bounded interval, $P, P'$ be two partitions of $I$. We define the common refinement $P \# P'$ to be the set

$$P \# P' := \{ K \cap J : K \in P \land J \in P' \}$$

**Definition (lower sum, upper sum)** The lower sum, upper sum of a bounded function $f$ with respect to partition $P$ is given by

$$L(f,P) := \sum_{k=1}^{n} m_k (x_k - x_{k-1})$$

$$U(f,P) := \sum_{k=1}^{n} m_k (x_k - x_{k-1})$$

where $m_k := \inf\{ f(x): x\in [x_{k-1}, x_k] \}$, $M_k := \sup\{ f(x): x\in [x_{k-1}, x_k] \}$

### 3.2. Integrability
**Definition (upper integral, lower integral)** Let $\mathcal{P}$ be the collection of all possible partitions of the interval $[a,b]$. The upper integral, lower integral of $f$ is defined to be

$$U(f) := \inf \{ U(f,P) : P \in \mathcal{P} \}$$

$$L(f) := \sup \{ L(f,P) : P \in \mathcal{P} \}$$

**Definition (Riemann Integrability)** A bounded function $f$ defined on the interval $[a,b]$ is Riemann-integrable if $U(f) = L(f)$. In this case

$$\int_{a}^b f = U(f) = L(f)$$

**Criterion (Integrability)** A bounded function $f$ is integrable on $[a,b]$ iff for every $\epsilon > 0$ there exists a partition $P_{\epsilon}$ of $[a,b]$ such that

$$U(f, P_{\epsilon}) - L(f, P_{\epsilon}) < \epsilon$$

By applying this criterion, we know several classes of functions are integrable
**Criterion (continuous function is integrable)** If $f$ is continuous on $[a,b]$, then it is integrable

Proof: This can be shown by controlling the difference between max and min within each range by exploiting uniform continuity, (which is guaranteed by the domain compactness)

**Criterion (monotone function is integrable)** If $f: [a,b] \to \mathbb{R}$ is monotone on the set $[a,b]$, then it is integrable.

**Criterion (function with a single discontinuity at an endpoint is integrable)** If $f: [a,b] \to R$ is bounded and $f$ is integrable on $[c,b]$ for all $c \in (a,b)$, then $f$ is integrable on $[a,b]$

!!! example "A function with single discontinuity is still integrable"

    Consider the function with the domain $[0,1]$

    $$f(x) = \begin{cases} 1 & \text{ for } x \neq 1 \\ 0 & \text{ for } x =1 \end{cases}$$

    The upper sum $U(f,P)$ is always 2, the lower sum is less than 2, but can be controlled by embedding the discontinuity into a small subinterval.

Any function with a finite number of discontinuity is integrable, some function with infinite discontinuities still might be integrable, depending on its measure of discontinuity.

!!! example "Function with $N$ discontinuity is integrable"

    Consider the function

    $$f(x) = \begin{cases} 1 & \text{ if } x=1/n \text{ for some } n \in N \\ 0 & \text{ otherwise} \end{cases}

    This function has discontinuity of $N$ and is integrable (by considering partition sequence with length of $1/n^2$)


!!! example "Function with $Q$ discontinuity is integrable (Thomae's function)"

    Thomae's function has discontiuities at every rational number

    $$f(x) = \begin{cases} 1/n & \text{ if } x=m/n \\ 0 & \text{ if } x \notin Q \end{cases}$$

    Its discontinuity has measure 0 and is integrable.


**Criterion (Lebesgue)** Let $f: [a,b] \to R$ be a bounded function. $f$ is Riemann-integrable iff the set of noncontinous point has measure zero

!!! example "Function with uncountable discontinuity might be integrable (Cantor)"

    Consider the indicator function over the Cantor set

    $$f(x) = \begin{cases} 1 & \text{ if } x \in C \\ 0 & \text{ if } x \not\in C \end{cases}$$

    where $C$ is the cantor set. This function has uncountable discontinuity but with measure 0, therefore it is Riemann Integrable


!!! example "Dirichlet's function is not Riemann Integrable"

    The Dirichlet's function is not Riemann Integrable because the noncontinuous point has measure 1.

    $$f(x) = \begin{cases} 1 & \text{ for x rational} \\ 0 & \text{ for x irrational} \end{cases}$$


### 3.3. Properties of the Integral
**Theorem** Assume $f: [a,b] \to R $ is bounded and $c \in (a,b)$. Then $f$ is integrable on $[a,b]$ iff $f$ is integrable on $[a,c]$ and $[c,b]$, in which case

$$\int_a^b f = \int_a^c f + \int_c^b f$$

**Theorem** Assume $f$ and $g$ are integrable functions on the interval $[a,b]$

The function $f+g$ is integrable on $[a,b]$

$$\int_a^b f+g = \int_a^b f + \int_a^b g$$

For $k \in R$, the function $kf$ is integrable

$$\int_a^b kf = k \int_a^b f$$

If $f(x) < g(x)$ on $[a,b]$

$$\int_a^b f \leq \int_a^b g$$

The function $|f|$ is integrable and 
$$|\int_a^b f | \leq \int_a^b |f| $$

**Theorem (Integral Limit Theorem)** Assume that $f_n \to f$ uniformly on $[a,b]$ and each $f_n$ is integrable. Then $f$ is integrable and 

$$\lim_{n \to \infty} \int_{a}^{b} f_n = \int_{a}^{b} f $$

### 3.4. Fundamental Theorem of Calculus

Note that Stoke theorem can be thought as generalization of those fundamental theorems.

Integration of Differentiation
**Theorem (fundamental theorem of calculus 1)** if  $f: [a,b] \to R$ is integrable and $f$ is antidifferentiable such that $F: [a,b] \to R$ is antiderivative of $f$ then

$$\int_{a}^{b} f = F(b) - F(a)$$

Differentiation of Integration.
**Theorem (fundamental theorem of calculus 2)** Let $g: [a,b] \to R$ be integrable and for $x \in [a,b]$ define

$$G(x) = \int_{a}^{x} g$$

then $G$ is continuous on $[a,b]$ If $g$ is continuous at some point $c \in [a,b]$, then $G$ is differentiable at $c$ and $G'(c) = g(c)$

!!! example "continuity is required in the 2nd statement"

    Consider the function

    $$f(x) = \begin{cases} 0 & \text{ if } x < 0 // 1 & \text{ if } x \geq 0 \end{cases}$$

    It has 1 discontinuity at 0 and its integration is

    $$F(x) = \begin{cases} 0 & \text{ if } x < 0 // x & \text{ if } x \geq 0 \end{cases}$$

    $F(x)$ is not differentiable at this point! 

Note the other side is not true: $G$ being able to differentiate at $c$ does not imply that $g(c)$ is continuous.

**Lemma (Integration by parts)** Assume $f(x), g(x)$ are continuously differentiable, then

$$\int_{a}^b f(x)'g(x) dx = f(b)g(b) - f(a)g(a) - \int_a^b f'(x)g(x) dx$$

Note the requirement is a bit stronger than necessary.

**Lemma (Integration by substitution)** Assume $f(x)$ is continuous, and $g(x)$ is continuously differentiable, then

$$\int_a^b f(g(x))g'(x) dx = \int_{g(a)}^{g(b)} f(x) dx$$

Leibnitz's rule is an application of the Fundamental Theorem and chain rules. It characterizes the interchanging the differnetiation and integral.
**Theorem (Leibnitz's Rule)** If $f(x, \theta), a(\theta), b(\theta)$ are differentiable with respect to $\theta$, then

$$\frac{d}{d\theta} \int_{a(\theta)}^{b(\theta)} f(x, \theta) dx = f(b(\theta), \theta) \frac{d}{d\theta}b(\theta) - f(a(\theta), \theta) \frac{d}{d\theta}a(\theta) + \int_{a(\theta)}^{b(\theta)} \frac{\partial}{\partial \theta} f(x, \theta)$$

If both $a(\theta), b(\theta)$ are constant, we have a special case of Leibnitz's Rule
$$\frac{d}{d\theta} \int_{a}^{b} f(x, \theta) dx = \int_{a}^{b} \frac{\partial}{\partial \theta} f(x, \theta) dx$$


## 4. Reference
[1] Tao, Terence. Analysis. Vol. 1. Hindustan Book Agency, 2006.

[2]  Tao, Terence. Analysis. Vol. 2. Hindustan Book Agency, 2006.

[3] Abbott, Stephen. Understanding analysis. Vol. 2. New York: Springer, 2001.

[4] Lax, Peter D., and Maria Shea Terrell. Multivariable Calculus with Applications. Springer, 2017.

[5] 杉浦光夫. "解析入門 I." 東京大学出版会
[6] 杉浦光夫. "解析入門 II." 東京大学出版会
