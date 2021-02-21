# 0x001 Topology

- [1. Topological Space](#1-topological-space)
- [2. Metric Space](#2-metric-space)
- [3. Connectedness](#3-connectedness)
- [4. Compactness](#4-compactness)
- [5. Reference](#5-reference)

## 1. Topological Space
**Definition (topology)** Let $X$ be a non-empty set. A set $\mathcal{T}$ of subsets of $X$ is said to be topology on $X$ iff

- $X \in \mathcal{T}, \emptyset \in \mathcal{T}$
- union of any number of sets of $\mathcal{T}$ belongs to $\mathcal{T}$
- interaction of any two sets of $\mathcal{T}$ belongs to $\mathcal{T}$
- The pair $(X, \mathcal{T})$ are called topological space

!!! example "discrete, indiscrete topology"

    There are two trivial topological space for any $X$, $2^X$ is the *discrete topology* of $X$, $\{  \emptyset, X \}$ is the *indiscrete topology* of $X$.

**Definition (finer, coarser)** Suppose $\mathcal{T}, \mathcal{T'}$ are two different topologies on a given set $X$, if $\mathcal{T} \subset \mathcal{T'}$, then $\mathcal{T}$ is a coarser and $\mathcal{T'}$ is a finer topology

**Definition (open set)** $U \subset X$ is an open set iff $U \in \mathcal{T}$

## 2. Metric Space
**Definition (Metric spaces)** A metric space $(X,d)$ is a space $X$ of objects, together with a distance function or metric $d: X \times X \to [ 0, \infty ]$, which associates to each pair $x,y$ of points in $X$ a non-negative real number $d(x,y) \geq 0$. Furthermore, the metric must satisfy the following four axioms:

- $(\forall{x \in X}) d(x,x) =0$
- $(\forall{x, y \in X, x \neq y}) d(x,y) > 0$
- $(\forall{x, y \in X}) d(x,y) = d(y,x)$
- $(\forall{x,y,z \in X}) d(x,z) \leq d(x,y)+d(y,z)$

**Definition (Ball)** The ball $B_{(X,d)} (x_0, r)$ in a metric space where $x_0 \in X, r >0$ is defined to be the set

$$B_{(X,d)} (x_0, r) := \{ x \in X: d(x, x_0) \in r \}$$

**Definition (Convergence)** Let $(X,d)$ be a metric space and let $(x^n)_{n=m}^{\infty}$ be a sequence of points in $X$, let $x \in X$. We say that $(x^n)_{n=m}^{\infty}$ converges to $x$ with respect to the metric $d$ iff $\lim_{n \to \infty} d(x^n, x)$ exists and is equal to 0

!!! example "$l^{\infty}$ metric"

    $$d_{l^{\infty}}((x_1, x_2, ..., x_n), (y_1, y_2, ..., y_n)) := sup\{ |x_i - y_i|: 1 \leq i \leq n \}$$

!!! example "discrete metric"

    Let $X$ be an arbitrary set, the discrete metric is defined by $d_{disc}(x,y) := 0$ if $x=y$ otherwise $d_{disc}(x,y) = 1$

**Proposition (equivalence of $l^1, l^2, l^{\infty}$)** Let $R^n$ be a Euclidean space, $(x^{(k)})_{k=m}^{\infty}$ be a sequence of points in $R^n$. We write $(x^{(k)}=(x_1^{(k)}, x_2^{(k)}, ..., x_n^{(k)})$. Let $x=(x_1, x_2, ..., x_n)$ be a point in $R^n$. Then the following four statements are equivalenet

- $(x^{(k)})_{k=m}^{\infty}$ converges to $x$ with respect to $l^1$
- $(x^{(k)})_{k=m}^{\infty}$ converges to $x$ with respect to $l^2$
- $(x^{(k)})_{k=m}^{\infty}$ converges to $x$ with respect to $l^{\infty}$
for all $1 \leq j \leq n$, the sequence $(x_j^{(k)})_{k=m}^{\infty}$ converges to $x_j$

Note the following limit point is a limit point over a set, the limit point over a sequence is another concept.

**Definition (limit point over a set)** A point $x$ is a limit point of a set $A$ if every $\epsilon$ neighborhood of $x$ intersects the set $A$ at some point other than $x$

This essentially means that $x$ can be a limit of sequence on $A$. A point $x$ is a limit point of a set $A$ iff $x = \lim a_n$ for some sequence $(a_n)$ contained in $A$ satisfying $a_n \neq x$ for all $n \in \mathbf{N}$

One important fact is limit point $x$ might not belong to $A$

**Definition (interior, boundary, exterior)** 
$x_0 \in X$ is an interior iff $(\exists r >0) B(x_0, r) \subseteq E$
$x_0 \in X$ is an exterior iff $(\exists r >0) B(x_0, r) \cap E = \emptyset$
$x_0$ is a boundary point if it is neither an interior or exterior

**Definition (adherent point)** $x_0$ is an adherent point of $E \subseteq X$ iff

$$(\forall r > 0) B(x_0, r) \cap E \neq \emptyset$$

Note: adherent point does not equal to limit point as it allows isolated point, but limit point need a sequence (different from itself) to approach it

**Definition (closure)** The set of all adherent point of $E$ is called the closure of $E$ and is denoted $\bar{E}$

**Definition (open, closed)** 
- $E$ is closed if it contains all of its boundary points (it contains its limit points.)
- $E$ is open if it contains none of its boundary points


**Definition (isolated point)** A point $x \in A$ is an isolated point of $A$ if it is not a limit point of $A$

Note that an isolated point must belong to $A$. Isolation means that there is a neighborhood where the point can be detached from the remaining of the other points.

Closed set essentially means the set is closed under limit operations

**Lemma (properties of closed set)**
- finite union of closed set is closed
- any intersection of closed set is closed (up to uncountable intersection)
- Infinite union of closed set might not be closed (e.g: $\cup_{n} [1/n, 1]$ is not closed as 0 does not belong to it)

**Examples (closed set)**
- cantor set

**Definition (adherent point, closure point)** $x$ is called an adherent point of $A$ if every neighborhood of $x$ contains at least one point of $A$.

Adherent point is either limit point or isolated point

**Definition (closure)** A closure of $A$ is a set $\bar{A}$ combining all limit points $L$ with $A$

$$\bar{A} = A \cup L$$

Closure is a closed set and is the smallest closed set containing $A$

Theorem $O$ is open $\iff$ $O^c$ is closed

**Definition (perfect)** A set $P \subset R$ is perfect if it is closed and contains no isolated points

A nonempty perfect set is uncountable

## 3. Connectedness
**Definition (connected space)** Let $X$ be a topological space, A separation of $X$ is a pair $U,V$ of disjoint open subsets of $X$ whose union is $X$. The space is said to be connected if there is no separation of $X$.

**Definition (separated)**  Two nonempty sets $A,B \subset R$ are separated if $\bar{A} \cap B$ and $A \cap \bar{B}$ are both empty

**Definition (disconnected)** A set $E \subset R$ is disconnected if it can be written as $E = A \cup B$ where $A,B$ are separated. If it is not disconnected, it is called connected

**Lemma (connected)** A set is connected if and only if for all disjoint sets $A,B$ where $E = A \cap B$,  there is always a convergent sequence from one side can limit into the other one. 

Lemma A set $E \subset R$ is connected iff whenever $a < c < b$ with $a,b\in E$ it follows that $c \in E$

**Definition (connectedness in metric space)** Let $(X, d)$ be a metric space. We say that $X$ is disconnected iff there exist disjoint non-empty open sets $V, W$ such that $X=V \cup W$

## 4. Compactness
compactness is a concept generalizing a bounded closed set.

**Definition (open cover)** Suppose $A \subset R$, a collection $\mathcal{C}$ of open subsets of $R$ is called an open cover of $A$ if $A$ is contained in the union of all the sets in $\mathcal{C}$

**Definition (finite subcover)** An open cover $\mathcal{C}$  of $A$ is said to have a finite subcover if $A$ is contained in the union of some finite list of sets in $\mathcal{C}$

**Definition (sequential compactness)** A set $K \subset R$ is sequential-compact if every sequence in $K$ has a subsequence that converges to some limit in $K$.

**Definition (compactness)** A set $K \subset R$  is compact if every open cover for $K$ has a finite subcover

**Theorem (Heine-Borel)** Following statements are equivalent

- $K$ is sequential compact
- $K$ is compact
- $K$ is closed and bounded


## 5. Reference
[1] Abbott, Stephen. Understanding analysis. Vol. 2. New York: Springer, 2001.

[2] Tao, Terrence. "Analysis (Volume 1)." Hindustan Book Agency (2006).

