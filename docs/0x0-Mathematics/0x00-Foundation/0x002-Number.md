# Number

- [1. N](#1-n)
- [2. Z](#2-z)
- [3. Q](#3-q)
- [4. R](#4-r)
    - [4.1. Statements of Completeness](#41-statements-of-completeness)
- [5. Reference](#5-reference)

## 1. N ##
Peano Axioms

## 2. Z ##
**Theorem (Division theorem)** For any integer $a$ and any positive integer $n$, there exist unique integers $q, r$ such that $0 \leq r < n$ and

$$a = qn + r$$

**Theorem (Unique factorization)** There is exactly one way to write any composite integer $a$ as a product of the form

$$a = p_1^{e_1} p_2^{e_2} ... p_r^{e_r}$$

where $p_i$ are prime, $p_1 < p_2 ... < p_r$ and $e_i$ are positive integers.

## 3. Q ##

**Proposition (cardinality)** Q is countable

!!! info "proof"

    Set $A_1 = \{ 0 \}$ and $A_n$ where $n \geq 2$ be the set

    $$A_{n} = \{ \pm \frac{p}{q} \text{ where } $p,q \in N$ \text{ are in lowest terms with } p+q=n \}$$

    Then all Q can be enumerated



## 4. R ##

The reason to move from rational numbers to real numbers is when we encounter a sequence that looks as if it is converging to something, say $\sqrt{2}$, then we can be assured that there is indeed a number there we can call the limit.

Technically, $\mathbf{R}$ can be obtained by completing $\mathbf{Q}$ with an additional axiom as follows.

**Axiom (completeness)** Every nonempty set of real numbers that is bounded above has a least upper bound.

The definition of upper bound and least upper bound is given by

**Definition (upper bound)** A set $A \subseteq \mathbf{R}$ is bounded above if there exists a number $b \in \mathbf{R}$ such that $\forall{a \in A} a \leq b$. The number $b$ is called an upper bound of $A$.

**Definition (least upper bound)** A real number $s$ is the least upper bound for a set $A \subseteq \mathbf{R}$, denoted by $s = \sup(A)$, if it meets the following two criteria:

- $s$ is an upper bound for $A$ (upper bound condition)
- if $b$ is any upper bound for $A$, then $s \leq b$ (least condition)

$\sup$ is a more general concept of $\max$, while $\max(A)$ might not exist, $\sup(A)$ should always exists for bounded nonempty set $A$ because of the axiom of compeleteness. An important difference between sup and max is that $\sup(A)$ may or may not be an element of $A$, but $\max(A)$ is an element of $A$ if exists.

**Lemma (N and R, Archimedian property)** Given any number $x \in \mathbb{R}$, there exists an $n \in \mathbb{N}$ satisfying $n > x$. Given any real number $y > 0$, there exists an $n \in \mathbb{N}$ satisfying $1/n < y$

**Lemma (N and Q, density)** For every two real numbers $a,b$, there exists a rational number $r$ satisfying $a < r < b$.

**Proposition (cardinality)** R is uncountable

!!! info "proof R is uncountable"

    Suppose $R$ is countable, then $R$ can be enumerated by

    $$\{ x_1, x_2, ..., \}$$

    We prepare a list of intervals $I_n$ such that $I_{n+1} \subseteq I_n$ and $x_{n+1} \notin I_n$

    Then we know 

    $$\cap_n I_n$ contains such real number (by the Nested Interval Theorem), which is against the previous assumption.


### 4.1. Statements of Completeness
There are several equivalent statements about completeness. One of them can derive all the others.

**Theorem (Nested Interval Theorem)** Let $I_n = [a_n, b_n]$ be a sequence of closed intervals, and suppose that these intervals are nested in the sense that $I_1 \supset I_2 \supset I_3... $
and $b_n-a_n \to 0$ when $n \to \infty$, then the result interval has a nonempty intersection.

$$\cap_{n=1}^{\infty} I_n \neq \emptyset$$

**Theorem (Bolzano Weierstrass)** Every bounded sequence contains a convergent subsequence

**Theorem (Cauchy completeness)** Every Cauchy sequnece of real numbers converges

**Theorem (monotone convergence)** every nondecreasing, bounded sequence of real numbers converges

## 5. Reference
[1] Hofstadter, Douglas R. Gödel, escher, bach: ein endloses geflochtenes band. Klett-Cotta, 2006.
[2] Tao, Terence. Analysis. Vol. 1. Hindustan Book Agency, 2006.
