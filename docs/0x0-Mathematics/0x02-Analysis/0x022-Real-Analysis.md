# 0x022 Real Analysis

- [1. Measures](#1-measures)
    - [1.1. Outer Measure](#11-outer-measure)
    - [1.2. Measurable Spaces and Functions](#12-measurable-spaces-and-functions)
    - [1.3. Measures and Their Properties](#13-measures-and-their-properties)
    - [1.4. Convergence of Measurable Functions](#14-convergence-of-measurable-functions)
- [2. Integration](#2-integration)
    - [2.1. Integration with respect to a Measure](#21-integration-with-respect-to-a-measure)
    - [2.2. Limits of Integrals](#22-limits-of-integrals)
- [3. Differentiation](#3-differentiation)
    - [3.1. Product Measures](#31-product-measures)
    - [3.2. Products of Measure Spaces](#32-products-of-measure-spaces)
- [4. Banach Space](#4-banach-space)
- [5. LP Space](#5-lp-space)
- [6. Hilbert Space](#6-hilbert-space)
- [7. Reference](#7-reference)

Riemann Integral is not good enough. It has several deficiencies as follows:

- Riemann integration does not handle functions with many discontinuities
- Riemann integration does not handle unbounded functions
- Riemann integration does not work well with limits

## 1. Measures
### 1.1. Outer Measure
**Definition (length of open interval)** The length $l(I)$ of an open interval $I$ is defined by

$$ l(I) = 
\begin{cases}
b-a & \text{for } I = (a,b) \\
0 & \text{if } I = \emptyset \\ \infty & \text{if } I = (-\infty, a) \text{ or } I = (a, \infty) \\ \infty & \text{if } I = (-\infty, \infty) \end{cases}$$

**Definition (outer measure, $|A|$)** The outer measure $|A|$ of a set $A \subset R$ is defined by 

$$ |A| = \inf \{  \sum_{k=1}^{\infty} l(I_k): I_1, I_2, ... \text{ are open intervals and covers } A \}$$

!!! example "countable set has measure 0"

    Every countable subset of $R$ has outer measure 0. Each item can be covered by a open interval

    $$I_k = (a_k - \epsilon/2^k, a_k+ \epsilon/2^k)$$

    where

    $$\sum l(I_k) = 2 \epsilon$$

**Lemma (outer measure preserves order)**
$$A \subset B \implies |A| \leq |B|$$

**Lemma (outer measure is translation invariant)** Suppose $t \in R, A \subset R$

$$|t+A| = |A|$$

**Theorem (countable subadditivity)** Suppose $A_1, A_2, ...$ is a sequence of subsets of $R$. Then

$$ |\bigcup_{k=1}^{\infty} A_k | \leq \sum_{k=1}^{\infty} |A_k|$$

**Theorem (outer measure of a closed interval)** Suppose $a, b \in R, a < b$, then

$$|[ a, b ] | = b-a$$

note that this can be proved with Heine-Borel

**Theorem (nonadditivity of outer measure)** There exists disjoint subsets $A, B \subset R$ such that

$$|A \cup B| \neq |A| + |B|$$

note that this can be proved using AoC

### 1.2. Measurable Spaces and Functions
**Definition ($\sigma$-algebra)** $X$ is a set and $S$ is a set of subsets of $S$, $S$ is called $\sigma$-algebra when the following conditions are satisfied:

- $\emptyset \in S$
- $E \in S \implies X \setminus E \in S$
- $E_1, E_2, ... \in S \implies \bigcup_{k=1}^{\infty} E_i \in S$
  
**Definition (measurable space; measurable set)** A measurable space is an ordered pair $(X, S)$, where $X$ is a set and $S$ is a $\sigma$-algebra on $X$. An element of $S$ is called an $S$-measurable set.

**Definition (Borel set)** The smallest $\sigma$-algebra on $R$ containing all open subsets of $R$ is called the collection of Borel subsets of $R$. An element of this $\sigma$-algebra is called a Borel set.

!!! example "example of Borel sets"

    every open, half, closed subset is a Borel set. 

    every countable subset $\{ x_1, x_2, ... \}$ of $R$ is a Borel set because it can be written as

    $$B = \cup^{\infty}_i \{ x_i \}$$

**Definition (inverse image)** If $f: X \to Y$ is a function and $A \subset Y$, then the set $f^{-1}(A)$ is defined by

$$f^{-1}(A) = \{ x \in X: f(x) \in A \}$$

**Definition (measurable function)** Suppose $(X,S)$ is a measurable space. A function $f: X \to R$ is called S-measurable function if for every Borel set $B \subset R$

$$f^{-1}(B) \in S$$

**Criterion** Suppose $(X,S)$ is a measurable space and $f: X \to R$ is a measurable function iff 

$$f^{-1}((a, \infty)) \in S$$

**Definition (Borel measurable function)** Suppose $X \subset R$. A function $X \to R$ is called Borel measurable if $f^{-1}(B)$ is a Borel set for every Borel set $B \subset R$

Example Every continuous real-valued function defined on a Borel subset is a Borel measurable function

Example Every increasing function defined on a Borel subset is a Borel measurable function

**Criterion (operations preserving measurable functions)** Measurable functions are closed under composition, algebraic operations and pointwise functional limit

### 1.3. Measures and Their Properties
**Definition (measure)** Suppose $X$ is a set and $S$ is a $\sigma$-algebra on $X$. A measure  on $(X,S)$ is a function $\mu: S \to [0, \infty]$ such that $\mu(\emptyset) = 0$ and

$$\mu(\bigcup_{k=1}^{\infty} E_k) = \sum_{k=1}^{\infty} \mu(E_k)$$

**Definition (measure space)** A measure space is an ordered triple $(X, S, \mu)$, where $X$ is a set, $S$ is a $\sigma$-algebra, and $\mu$ is a measure on $(X,S)$

**Property (measure preserves order)** Suppose $(X, S, \mu)$ is a measure space, $D, E \in S$ and $D \subset E$, then
$$\mu(D) \leq \mu(E)$$

**Property (acountable subadditivity)** Suppose $(X, S, \mu)$ is a measure space and $E_1, E_2, ... \in S$, then

$$\mu(\cup_{k=1}^{\infty} E_i) \leq \sum_{k=1}^{\infty} \mu(E_i)$$

**Property (measure of a union)** Suppose $(X, S, \mu)$ is a measure space and $D,E \in S, \mu(D \cap E) < \infty $, then

$$\mu (D \cup E) = \mu(D) + \mu(E) - \mu(D \cap E)$$

**Property (outer measure is a measure on Borel sets)** Outer measure is a measure on $(R,B)$ where $B$ is the $\sigma$-algebra of Borel subsets of $R$

**Definition (Lebesgue measure wrt Borel subsets)** Lebesgue measure is the measure on $(R,B)$ where $B$ is the $\sigma$ algebra of Borel subsets of $R$, that assigns to each Borel set its outer measure

**Definition (Lebesgue Measurable set)** A set $A \subset R$ is called Lebesgue Measurable if there exists a Borel set $B \subset A$ such that $| A \ B|=0$

**Definition (Lebesgue Measure wrt Lebesgue Measurable set)** Lebesgue Measure is the measure on $(R, L)$ where $L$ is the $\sigma$-algebra of Lebesgue measurable subsets of $R$, that assigns to each Lebesgue measurable set its outer measure. $L$ is defined as

$$ L = \{ D \subset R | \forall{\epsilon > 0} \exists{F \subset D} |D \ F | < \epsilon \}$$

### 1.4. Convergence of Measurable Functions
**Theorem (Egorov)** Suppose $(X,S,\mu)$ is a measurable space and $\mu(X) < \infty$. Suppose $f_1, f_2, ...$ is a sequence of $S$-measurable function from $X$ to $R$ that converges pointwise on $X$ to a function $f$. Then for every $\epsilon > 0$, there exists a set $E \in S$ such that $\mu(X \ E ) < \epsilon$ and $f_1, f_2...$ converges uniformly to $f$ on $E$

**Theorem (Luzin)** Suppose $g: R \to R$ is a Borel measurable function. Then for every $\epsilon > 0$ there exists a closed set $F \subset R$ such that $| R \ F| < \epsilon$ and $g|_{F}$ is continuous function on $F$

## 2. Integration
For a measure space $(X, S, \mu)$, we aims at defining $\int_{A} f(x) d\mu$ for suitable measurable function $f: X \to R$ and for any $A \in S$ in a systematic manner.

### 2.1. Integration with respect to a Measure
**Definition (S-partition)** Suppose $S$ is a $\sigma$-algebra on a set $X$. An $S$-partition of $X$ is a finite collection $A_1, ..., A_m$ of disjoint sets in $S$ such that $A_i \cup .... \cup A_m = X$ 

**Definition (lower Lebesgue sum)** Suppose $(X, S, \mu)$ is a measure space, $f: X \to [0, \infty]$ is a S-measurable function and $P$ is a partition $A_1, ..., A_m$ of $X$. The lower Lebesgue sum $\mathcal{L}(f,P)$ is defined by 

$$\mathcal{L}(f, P) = \sum_{j=1}^{m} \mu(A_j) \inf_{A_j} f$$

We first think about reducing integration to the simple case of integrating non-negative function $f^{+}$, later it can be extended to a general function $f$ by expressing it using two non-negative function $f = f^{+} - f^{-}$

**Definition (Integral of a nonnegative function)** Suppose $(X, S, \mu)$ is a measure space and $f: X \to [0, \infty]$ is an $S$-measurable function. The integral of $f$ with respect to $\mu$ is defined by

$$ \int f d\mu = \sup \{ \mathcal{L}(f, P) | P \text{ is an S-partition of }X \}$$

Next, we think about reducing it to the case of integrating simple functions.

**Lemma (Integral of a characteristic function)** Suppose $(X, S, \mu)$ is a measure space and $E \in S$, Then

$$\int \chi_{E} d\mu = \mu(E)$$

**Theorem (monotone convergence)** Suppose $(X, S, \mu)$ is a measure space and $0 \leq f_1 \leq f_2 \leq ...$ is an increasing sequence of $S$-measurable functions. Define $f: X \to [0, \infty]$ by

$$f(x) = \lim_{k \to \infty} f_k(x)$$

Then

$$\lim_{k \to \infty} \int f_k(x) d\mu = \int f(x) d\mu$$

**Theorem (addivity of integration)** Suppose $(X, S, \mu)$ is a measure space and $f, g: X \to R$ are S-measurable functions such that $\int |f| < \infty, \int |g| < \infty$. Then

$$\int (f+g) d\mu = \int f d\mu + \int g d\mu$$

**Theorem (integration is homogeneous)** Suppose $(X, S, \mu)$ is a measure space and $f: X \to [-\infty, \infty]$ is a function such that $\int f d\mu$ is defined. If $c \in R$, then

$$\int c f d\mu = c \int f d\mu$$

### 2.2. Limits of Integrals
**Definition (integration on a subset)** Suppose $(X, S, \mu)$ is a measure space and $E \in S$. If $f: X \to [-\infty, \infty]$ is an $S$-measurable function, then $\int_{E} f d\mu$ is defined by

$$\int_{E} f d\mu = \int \chi_{E} f d\mu$$

**Definition (almost every)** Suppose $(X, S, \mu)$ is a measure space. A set $E \in S$ is said to contain $\mu$-almost every element of $X$ if $\mu( X \ E)=0$.

**Theorem (Dominated Convergence Theorem)** Suppose $(X, S, \mu)$ is a measure space, $f: X \to [-\infty, \infty]$ is $S$-measurable, and $f_1, f_2, ...$ are $S$-measurable functions from $X$ to $[-\infty, \infty]$ such that 

$$\lim_{k \to \infty} f_k (x) = f(x)$$

for almost every $x \in X$. If there exists an $S$-measurable function $g: X \to [0, \infty]$ such that

$$\int g d\mu < \infty \land | f_k (x) | \leq g(x) $$

for every $k \in Z^+$ and almost every $x \in X$, then

$$lim_{k \to \infty} \int f_k(x) d\mu = \int f d\mu$$

**Definition ($||f||_1, \mathcal{L}^1(\mu)$)** Suppose $(X, S, \mu)$ is a measure space. If $f: X \to [-\infty, \infty]$ is $S$-measurable. then the $\mathcal{L}^1$-norm of $f$ is defined by

$$||f||_1 = \int |f| d\mu$$

The Lebesgue space $\mathcal{L}^1(\mu)$ is defined by

$$\mathcal{L}^1(\mu) = \{ f: f \text{ is an S-measurable function from X to R such that } ||f||_1 < \infty$$

## 3. Differentiation
### 3.1. Product Measures
### 3.2. Products of Measure Spaces
**Definition (product of $\sigma$-algebra, $S \otimes T$)** Suppose $(X, S), (Y, T)$ are measurable spaces. Then the product $S \otimes T$ is defined to be the smallest $\sigma$-algebra on $X \times Y$ contains

$$\{ A \times B | A \in S, B \in T \}$$

**Definition (cross sections of sets)** Suppose $X, Y$ are sets and $E \subset X \times Y$. Then for $a \in X, b \in Y$, the cross sections $[E]_a, [E]^b$ are defined by

$$[E]_a = \{ y \in Y | (a, y) \in E \}$$

$$[E]^b = \{ x \in X | (x, b) \in E \}$$

## 4. Banach Space
**Theorem (Baire)** A complete metric space is not the countable union of closed subsets with empty interior 

## 5. LP Space
**Definition ($||f||_p$)** Suppose that $(X, S, \mu)$ is a measure space, $0 < p < \infty$ and $f: X \to F$ is $S$-measurable. Then the p-norm of $f$ is defined by

$$||f||_{p} = \Big( \int |f|^p d\mu \Big)^{1/p}$$

Note that the exponent is to make sure $||af||_p = |a| || f||_p$

**Definition (essential supremum)** The essential supremum of $f$ is 

$$||f||_{\infty} = \inf \{ t > 0 | \mu(\{ x \in X | |f(x)| > t \} ) = 0 \}$$

## 6. Hilbert Space

## 7. Reference
[1] Axler, Sheldon. "Measure, Integration & Real Analysis." (2020): 411.

