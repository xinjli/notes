# 0x000 Set Theory

- [1. History](#1-history)
- [2. Axiomatic Set Theory](#2-axiomatic-set-theory)
    - [2.1. Zermelo–Fraenkel](#21-zermelofraenkel)
        - [2.1.1. Function](#211-function)
        - [2.1.2. Images and Inverse Images](#212-images-and-inverse-images)
        - [2.1.3. Cartesian Products](#213-cartesian-products)
    - [2.2. Cardinality](#22-cardinality)
- [4. Reference](#4-reference)

This first note sets up the formal notations of sets, logic and number systems used in all notes.

## 1. History
The **naive set theory**, unlike the axiomatic set theories, is using informal logics based on natural languages. The naive set theory was first created by *Georg Cantor* at the end of 19th century and developed by *Gottlob Frege*.

However, *Bertrand Russel* found the following paradox during his work on *Principia Mathematica*

$$A = \{X | X \not\in X \}$$

from which contradictory conclusion can be drawn when deciding whether $A \in A$.

The paradox comes from the following axiom assumption.

**Axiom (Universal specification, Axiom of comprehension)**: Suppose for every object $x$, we have a property $P(x)$ pertaining to $x$. Then there exists a set $\{ x | P(X) \text{ is true } \}$

This is the one of examples of self-reference, which has many interesting applications in mathematics and computer science. For example, Gödel, Escher, Bach has many examples about this.

Frege respond to the letter from Russel as follows, sad..
> Hardly anything more unfortunate can befall a scientific writer than to have one of the foundations of his edifice shaken after the work is finished
> Gottlob Frege


## 2. Axiomatic Set Theory

### 2.1. Zermelo–Fraenkel
**Axiom (Sets are objects)**. If $A$ is a set, then $A$ is also an object. In particular, given two sets $A$ and $B$, it is meaningful to ask whether $A$ is also an element of $B$.

**Axiom (Axiom of extensionality, equality of set)**. Two sets $A$ and $B$ are equal, $A=B$, iff every element of $A$ is an element of $B$ and vice versa.

Comment: The "is an element of " relation $\in$ obeys the axiom of substitution ( equality axiom)

**Axiom (Empty set)**. There exists a set $\emptyset$, known as the empty set, which contains no elements. i.e. for every object $x$, we have $x \notin \emptyset$

**Lemma (Single Choice)** Let $A$ be a non-empty set. Then there exists an object $x$ such that $x \in A$

**Axiom (Singleton sets and pair sets)** If $a$ is an object, then there exists a set $\{ a \}$ (singleton). If $a$ and $b$ are objects, then there exists a set $\{ a, b \}$ (pair).

**Axiom (Pairwise union)**: Given any two sets $A, B$, there exists an union set $A \cup B$

**Lemma** Union operation is commutative and associative

**Definition (Subsets)** Let $A,B$ be sets. We say that $A$ is a subset of $B$, denoted $A \subseteq B$ iff every element of $A$ is also an element of $B$.

**Proposition (Sets are partially ordered by set inclusion)** Let $A,B,C$ be sets. If $A \subseteq B$ and $B \subseteq C$, then $A \subseteq C$. If $A \subseteq B$ and $B \subseteq A$ then $A=B$

**Axiom (Axiom of specification, axiom of separation)** Let $A$ be a set, and for each $x \in A$, let $P(x)$ be a property pertaining to $x$ (either true or false). Then there exists a set, called $\{ x \in A | P(X) \}$

**Definition (Intersections)**. The intersection $S_1 \cap S_2$ of two sets is defined to be the set

$$S_1 \cap S_2 = \{ x \in S_1 | x \in S_2 \}$$

**Definition (Difference sets)** Given two sets $A$ and $B$, we define the set $A-B$ or $A \setminus B$

$$A \setminus B := \{ x \in A | x \not\in B \}$$

**Proposition (Sets form a boolean algebra)** Let $A,B,C$ be sets, and let $X$ be a set containing $A,B,C$ as subsets

* (minimum element) $A \cup \emptyset = A$ and $\emptyset \cap A = \emptyset$
* (maximum element) $A \cup X = X$ and $A \cap X = A$
* (identity) $A \cap A = A, A \cup A = A$
* (commutativity) $A \cup B = B \cup A$ and $A \cap B = B \cap A$
* (associativity) $(A \cup B) \cup C = A \cup (B \cup C), (A \cap B) \cap C = A \cap (B \cap C)$
* (distributivity) $A \cap (B \cup C) = (A \cap B) \cup (A \cap C), A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$
* (Partition) $A \cup (X \setminus A) = X, A \cap (X \setminus A) = \emptyset$
* (De morgan laws) $X \setminus (A \cup B) = (X \setminus A) \cap (X \setminus B), X \setminus (A \cap B) = (X \setminus A) \cup (X \setminus B)$
  

**Axiom (Replacement)** Let $A$ be a set. For ay object $x \in A$, and any object y, suppose we have a statement $P(x,y)$ pertaining to $x$ and $y$, such that for each $x \in A$ there is at most one $y$ for which $P(x,y)$ is true. Then there exists a set $\{ y | P(x,y) \text{ is true for some } x \in A \}$

Remark: this can be used to apply function to element of a set to create another set

**Axiom (Infinity)** There exists a set $\mathcal{N}$, whose elements are called natural numbers such that Peano axioms hold

**Axiom (Axiom of regularity, axiom of foundation)** If $A$ is a non-empty set, then there is at least one element $x$ of $A$ which is either not a set, or is disjoint from $A$.


#### 2.1.1. Function
There are two ways to formally define the function, the common way is to simply define the domain, range, and how one generates the output $f(x)$ from each input, this is known as an explicit definition of a function, more or less the one proposed by Peter Lejeune Dirichlet in the 1830s when studying the convergence of Fourier Series.

The other case is to efine a function by specifying what property $P(x,y)$ links the input $x$ with the output $f(x)$; this is an implicit definition of a function.

**Definition (Functions)** Let $X,Y$ be sets, and let $P(x,y)$ be a property pertaining to an object $x \in X$ and an object $y \in Y$, such that for every $x \in X$ there is exactly one $y \in Y$ for which $P(x,y)$ is true. Then we define the function $f: X \rightarrow Y$ defined by $P$ to be the object which, given any input $x \in X$, assigns an output $f(x) \in Y$ for which $P(x, f(x))$ is true.

**Definition (Equality of functions)** Two functions $f: X \rightarrow Y, g: X \rightarrow Y$ with the same domain and range are said to be equal $f=g$ iff $f(x) = g(x)$ for all $x \in X$

**Definition (Composition)** Let $f: X \rightarrow Y$ and $g: Y \rightarrow Z$ be two functions, such that the range of $f$ is the same set as the domain of $g$. We then define the composition $g \circ f: X \rightarrow Z$ of the two functions $g$ and $f$ to be the function defined explicitly by the formula

$$(g \circ f)(x) := g(f(x))$$

**Lemma (Composition is associative)** Let $f: Z \rightarrow W, g: Y \rightarrow Z$ and $h: X \rightarrow Y$ be functions. Then $f \circ (g \circ h) = (f \circ g) \circ h$

**Definition (injective)** A function $f$ is one-to-one (or injective) if different elements map to different elements

$$x \neq x' \implies f(x) \neq f(x') $$

**Definition (surjective)** A function $f$ is onto (or surjective) if every element in $Y$ comes from applying $f$ to some element in $X$: for every $y \in Y$, there exists $x \in X$ such that $f(x) = y$

**Definition (bijective)** A function is called bijective or invertible if it is both injective and surjective

#### 2.1.2. Images and Inverse Images
**Definition (Images of Sets)** If $f: X \rightarrow Y$ is a function from $X$ to $Y$, and $S$ is a set in $X$, we define $f(S)$ to be the set

$$f(S) := \{  f(x) | x \in S \}$$

**Definition (Inverse images)** If $U$ is a subset of $Y$, we define the set $f^{-1}(U)$ to be the set

$$f^{-1}(U) := \{ x \in X | f(x) \in U \}$$

**Lemma (algebra of inverse images)** Suppose $f: X \to Y$ is a function, then

$$f^{-1}(Y \setminus A) = X \setminus f^{-1}(A)$$
$$f^{-1}(\cup_{A \in \mathcal{A}} A) = \cup_{A \in \mathcal{A}} f^{-1}(A)$$
$$f^{-1}(\cap_{A \in \mathcal{A}} A) = \cap_{A \in \mathcal{A}} f^{-1}(A)$$

**Axiom (Power set axiom)** Let $X,Y$ be sets. Then there exists a set, denoted $Y^{X}$, which consists of all the functions from $X$ to $Y$

Remark: this is to basically create larger set such as $\mathbf{R}$

**Lemma (existence of power set)** Let $X$ be a set, then following set exists

$$\{ Y | Y \subseteq X \}$$

**Axiom (Union)** Let $A$ be a set, all of whose elements are themselves sets. Then there exists a set $\cup A$ whose elements are precisely those objects which are elements of the elements of $A$.

#### 2.1.3. Cartesian Products
**Definition (Ordered Pair)** If $x$ and $y$ are any objects, we define the ordered pair $(x,y)$ to be a new object, consisting of $x$ as its first component and $y$ as its second component. Two ordered pairs $(x,y)$ and $(x', y')$ are considered equal iff both their components match

Remark: pair can be implemented with set as $(x,y) = \{ \{ x \}, \{ x, y \} \}$

**Definition (Cartesian Product)** If $X$ and $Y$ are sets, then we define the Cartesian product $X \times Y $ to be the collection of ordered pairs

$$X \times Y = \{ (x,y) | x \in X, y \in Y \}$$

**Definition (Ordered n-tuple and n-fold Cartesian product)** Let $n$ be a natural number. An ordered n-tuple $(x_i)_{1 \leq i \leq n}$ (also denoted $(x_1, ..., x_n)$ is a collection of objects $x_i$. If $(X_i)_{1 \leq i \leq n}$ is an ordered n-tuple of sets, we define their Cartesian product $\prod_{1 \leq i \leq n} X_i$ (also denoted $X_1 \times ... \times X_n$) by

$$\prod_{1 \leq i \leq n} := \{ (x_i)_{1 \leq i \leq n} | x_i \in X_i \text{ for all } 1 \leq i \leq n \}$$

**Definition (Finite choice)** Let $n \geq 1$ be a natural number and for each natural number $ 1 \leq i \leq n$, let $X_i$ be a non-empty set. Then there exists an n-tuple $(x_i)_{1 \leq i \leq n}$ such that $x_i \in X_i$ for all $1 \leq i \leq n$

Remark: infinite number of choices requires the axiom of choice

### 2.2. Cardinality

To compare the size of different sets, Cantor's idea was to attempt to put the sets into a 1-1 correspondence with each other.

**Definition (Equal cardinality)** $X$ and $Y$ have equal cardinality iff there exists a bijection $f: X \rightarrow Y$. In this case, we write

$$X \sim Y$$

The notion of having equal cardinality is an equivalence relation (i.e: reflective, symmetric, transitive)

**Definition (cardinality)** Let $n$ be a natural number. A set $X$ is said to have cardinality $n$ iff it has equal cardinality with $\{ i \in N | i < n \} $. We also say that $X$ has $n$ elements iff it has cardinality of $n$

**Proposition (Uniqueness of cardinality)** Let $X$ be a set of some cardinality $n$. Then $X$ cannot have any other cardinality.

**Lemma** Suppose that $n \geq 1$ and $X$ has cardinality $n$. Then $X$ is non-empty, and if $x$ is any element of $X$, then the set $X - \{ x \}$ has cardinality $n-1$.

**Definition (finite, infinite)** A set is infinite iff it has cardinality $n$ for some natural number $n$; otherwise, the set is called infinite. If $X$ is a finite set, we use $\#(X)$ to denote the cardinality of $X$

In the infinite sets, it has more than 1 level of cardinality.

**Definition (countable, uncountable)** A set $A$ is *countable* if $\mathbb{N} \sim A$, an infinite set that is not countable is called an *uncountable* set. (e.g: N, Z, Q are countable and R is uncountable)

!!! example "Cantor's Diagonalization"

    The open interval $(0,1)$ is uncountable. This can be shown by expanding each real number into a decimal representation.


## 4. Reference
[1] Hofstadter, Douglas R. Gödel, escher, bach: ein endloses geflochtenes band. Klett-Cotta, 2006.
[2] Tao, Terence. Analysis. Vol. 1. Hindustan Book Agency, 2006.
