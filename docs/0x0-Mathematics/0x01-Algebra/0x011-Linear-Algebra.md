# 0x011 Linear Algebra

- [1. Vector Spaces](#1-vector-spaces)
    - [1.1. Vector Space](#11-vector-space)
    - [1.2. Subspaces](#12-subspaces)
    - [1.3. Finite Dimension Vector Space](#13-finite-dimension-vector-space)
- [2. Inner Product Space](#2-inner-product-space)
    - [2.1. Inner Products and Norms](#21-inner-products-and-norms)
    - [2.2. Orthonormal Bases](#22-orthonormal-bases)
    - [2.3. Orthogonal Complements](#23-orthogonal-complements)
- [3. Linear Map](#3-linear-map)
    - [3.1. vector space of linear maps](#31-vector-space-of-linear-maps)
    - [3.2. Injectivity and Surjectivity](#32-injectivity-and-surjectivity)
    - [3.3. Invertibility (isomorphism)](#33-invertibility-isomorphism)
    - [3.4. Products](#34-products)
    - [3.5. Quotients](#35-quotients)
    - [3.6. Duality](#36-duality)
- [4. Eigenvalues and Eigenvectors](#4-eigenvalues-and-eigenvectors)
    - [4.1. Invariant Subspaces](#41-invariant-subspaces)
    - [4.2. Upper-Triangular Matrices](#42-upper-triangular-matrices)
    - [4.3. Diagonal Matrices](#43-diagonal-matrices)
- [5. Operators on Inner Product Spaces](#5-operators-on-inner-product-spaces)
    - [5.1. Normal Operator](#51-normal-operator)
    - [5.2. Hermitian Operator](#52-hermitian-operator)
    - [5.3. Positive Operator](#53-positive-operator)
    - [5.4. Unitary Operator](#54-unitary-operator)
- [6. Operators on Complex Vector Spaces](#6-operators-on-complex-vector-spaces)
    - [6.1. Generalized Eigenvectors](#61-generalized-eigenvectors)
    - [6.2. Operator Decomposition](#62-operator-decomposition)
    - [6.3. Characteristic and Minimal Polynomials](#63-characteristic-and-minimal-polynomials)
- [7. Operators on Real Vector Spaces](#7-operators-on-real-vector-spaces)
- [8. Reference](#8-reference)

The Hierarchical structure related to vector space is as follows:

![structure](../../img/Mathematical_Spaces.png)

With inner product structure, you can induce norm as

$$||a|| = \sqrt{\langle a, a \rangle}$$

With norm structure, you can induce metric as

$$d(a, b) = ||a-b||$$


## 1. Vector Spaces
closed under vector addition and scalar multiplication. It is a specicial case of module:  module over a field

### 1.1. Vector Space
**Definition (addition, scalar multiplication)**
An addition on a set $V$ is a function that assigns $u+v \in V$ to each pair of elements $u,v \in V$

A scalar multiplication on a set $V$ is a function that assigns an element $\lambda v \in V$ to each $\lambda \in F$ and each $v \in V$

**Definition (vector space)**
A vector space is a set $V$ along with an addition on $V$ and a scalar multiplication on V such that the following properties hold:

- commutativity: $u+v = v+u$ for all $u,v \in V$
- associativity: $(u+v)+w = u + (v+w)$ and $(ab)v = a(bv)$ for all $u,v,w \in V$ and $a,b \in F$
- additive identity: there exists an element $0 \in V$ such that $v+0 = v$ for all $v \in V$
- additive inverse: for every $v \in V$, there exists $w \in V$ such that $v+w=0$
- multiplicative identity: $1v = v$ for all $v \in V$
- distributive properties: $a(u+v) = au + av$ and $(a+b)v = av + bv$ for all $a,b \in F$ and all $u,v \in V$
- 
Note: $(V,+)$ is an abelian group

**Definition (vector)**: elements of a vector space are called vectors or points

### 1.2. Subspaces
**Definition (subspace)** A Subset $U$ of $V$ is called a subspace of $V$ if $U$ is also a vector space (using the same addition and scalar multiplication as on $V$)

**Criterion (subspace)** A subset $U$ of $V$ is a subspace iff $U$ satisfies the following three conditions
- additive identity: $ 0 \in U$
- closed under addition: $u,w \in \implies u+w \in U$
- closed under scalar multiplication: $a \in F, u \in U \implies au \in U$
  
Note: the union of subspaces is rarely a subspace, but a collection of subspaces are always subspace.

**Definition (sum of subspace)** Suppose $U_1, U_2, ... U_m$ are subsets of $V$, the sum of $U_1, ... U_m$, denoted by $U_1 + ... + U_m$ is the set of all possible sums of elements of $U_1, ... , U_m$. More precisely,

$$ U_1 + U_2 + ... + U_m = \{ u_1 + u_2 + ... + u_m | u_1 \in U_1, ..., u_m \in U_m \}$$

**Definition (direct sum)** Suppose $U_1, U_2, ... U_m$ are subspaces of $V$, the sum $U_1 + U_2 + ... + U_m$ is called a direct sum if each element of $U_1 + U_2 + ... + U_m$ can be written in only one way as a sum of $u_1 + u_2 + ... + u_m$, if it is a direct sum, then $U_1 \oplus U_2 \oplus ... \oplus U_m$ denotes $U_1 + U_2 + ... + U_m$

**Criterion (direct sum)** $U + W$ is a direct sum in either of the following case

there is only one way to write $u+w = 0$, where $u \in U, w \in W$
$U \cap W = \{ 0 \}$
note: direct sum means the linear independence between subspaces

### 1.3. Finite Dimension Vector Space
**Definition (linear combination)** A linear combination of a list $v_1, ..., v_m$ of vectors in $V$ is a vector of the form $a_1 v_1 + ... + a_m v_m$ where $a_1, ... , a_m \in F$

btw, Affine combination has a bias in addition

**Definition (span)** The set of all linear combinations of $v_1, ..., v_m$ in $V$ is called the span of $v_1, ... v_m$, denoted $span(v_1, ..., v_m)$.

**Definition (basis)** A basis of $V$ is a list of vectors in $V$ that is linearly independent and spans $V$

$$v = a_1 v_1 + ... + a_n v_n$$

Note that it has to satisfy two properties: 1) linear independence 2) span the whole space.

## 2. Inner Product Space
### 2.1. Inner Products and Norms
inner product is a generalization of the dot product

**Definition (inner product)** An inner product on $V$ is a function that takes each ordered pair $(u, v)$ of elements of $V$ to a number $\langle u, v \rangle \in F$ and has the following properties.

- (positivity) $\langle v, v \rangle \geq 0 $ for all $v \in V$
- (definiteness) $\langle v, v \rangle = 0 $ iff $v = 0$
- (additivity in first slot) $\langle u+v, w \rangle = \langle u, w \rangle + \langle v, w \rangle$ for all $u,v,w \in V$
- (homogeneity in first slot) $\langle \lambda u, v \rangle = \lambda \langle u, v \rangle$ for all $\lambda \in F$ and all $u,v \in V$
- (conjugate symmetry) $\langle u, v \rangle = \overline{\langle v, u \rangle}$ for all $u,v \in V$
  
**Definition  (inner product space)** An inner product space is a vector space $V$ along with an inner product on $V$

**Definition (norm)** For $v \in V$, the norm of $v$, denoted $||v||$ is defined by

$$||v|| = \sqrt{\langle v, v \rangle}$$

**Definition (orthogonal)** Two vectors $u, v \in V$ are called orthogonal if $\langle u, v \rangle = 0$

**Theorem (Pythagorean)** Suppose $u, v$ are orthogonal in $V$. Then

$$ || u+v ||^2 = ||u||^2 + ||v||^2$$

**Theorem (Cauchy-Schwarz)** Suppose $u,v \in V$. Then

$$ | \langle u, v \rangle | \leq ||u|| ||v|| $$

**Theorem (Triangle Inequality)** Suppose $u, v \in V$. Then

$$||u+v|| \leq || u|| + ||v||$$

### 2.2. Orthonormal Bases
**Definition (orthonormal)** A list of vectors is called orthonormal if each vector in the list has norm 1 and isorthogonal to all the other vectors in the list.

**Definition (orthonormal basis)** An orthonormal basis of $V$ is an orthonormal list of vectors in $V$ that is also a basis of $V$

**Theorem (Schur)** Suppose $V$ is a finite-dimensional complex vector space and $T \in \mathcal{L}(V)$ Then $T$ has an upper-triangular matrix with respect to some orthonormal basis of $V$

**Theorem (Riesz)** Suppose $V$ is finite-dimensional and $\varphi$ is a linear functional on $V$. Then there is a unique vector $u \in V$ such that

$$\varphi(v) = \langle v, u \rangle$$

### 2.3. Orthogonal Complements 
**Definition (orthogonal complement)** If $U \subset V$, then the orthogonal complement of $U$, denoted $U^\perp$ is

$$U^\perp = \{ v \in V : (\forall u \in U) \langle v, u \rangle = 0 \}$$

**Lemma (direct sum decomposition with orthogonal complement)** Suppose $U$ is a finite-dimensional subspace of $V$. Then

$$ V = U \oplus U^\perp $$

## 3. Linear Map
### 3.1. vector space of linear maps

**Definition (linear map)** A linear map from vector space $V$ to vector space $W$ obeys following properties

- T preserve addition (additivity) : $T(x+y)=T(x)+T(y)$
- T preserves scalar multiplication (homogeneity): $T(cx) = cT(x)$
  

Linear map is homomorphism of vector space

!!! note "linear map forms a vector space" 

    The set of all linear maps from $V$ to $W$ is denoted $\mathcal{L}(V, W)$. Suppose $S,T \in \mathcal{L}(V,W), \lambda \in F$ then sum and product are linear maps from $V \to W$

    $$(\forall v \in V) (S+T)(v) = Sv + Tv$$

    $$(\forall v \in V) (\lambda T)(v) = \lambda(Tv)$$

    With previous definitions, $\mathcal{L}(V,W)$ forms a vector space

**Definition (production of linear maps)** Suppose $T \in \mathcal{L}(U,V), S \in \mathcal{L}(V,W)$ then the product $S,T \in \mathcal{L}(U,W)$ is defined by

$$(\forall u \in U) (ST)(u) = S(T(u))$$

**Proposition (properties of products)**

- associativity $(T_1 T_2)T_3 = T_1 (T_2 T_3)$
- identity $TI = IT = T$
- distributive properties $(S_1 + S_2)T = S_1 T + S_2 T$


### 3.2. Injectivity and Surjectivity
Both injectivity and subjectivity are important concepts in linear algebra, they can be characterized by the null space and range space.

**Definition (injective)** A function $T: V \to W$ is called injective if $Tu = Tv \implies u=v$

**Defintiion (null space)** Null space (kernel) of linear map $T \in \mathcal{L}(V,W)$ is a subset of $V$ which was mapped to 0 vector : 

$$null(T) = \{ v \in V: T(V) = 0 \} $$

Note that null space is a subspace of $V$

Injectivity and null space are connected by the following proposition

**Condition (injectivity)** Let $T \in \mathcal{L}(V,W)$, then $T$ is injective iff $null(T)=\{ 0 \}$

Surjectivity is the property whether all elements in the target space can be reached with the map

**Definition (surjective)** A function $T: V \to W$ is called surjective if its range is $W$

**Definition (range)** The range of $T: V \to W$ is the subset of $W$ consisting of those vectors that are of the form $Tv$ for some $v \in V$

$$ range(T) = \{ Tv : v \in V \}$$

Note that range is a subspace of $W$

Surjectivity can be related to range space by the following condition.

**Condition (surjective)** A function $T: V \to W$ is called surjective if its range is $W$

Surjectivity/Injectivity or range/null can be related by the following fundamental theorem in Linear algebra.

**Theorem (fundamental theorem of linear maps)** Suppose $V$ is finite-dim and $T \in \mathcal{L}(V,W)$ .then range $T$ is finte-dim and 

$$\dim V = \dim null T + \dim range T$$

Proof concept: suppose $u_1, ..., u_m$ is a basis of $null(T)$, extending it to the basis of  $V$ by adding $v_1, ..., v_n$, then showing that $Tv_1, ..., Tv_n$ is a basis of $range(T)$

### 3.3. Invertibility (isomorphism)

**Definition (invertible)** A linear map $T \in \mathcal{L}(V,W)$ is called invertible if there exists a linear map $S \in \mathcal{L}(W,V)$ such that $ST$ and $TS$ are identity maps. $S$ and $T$ are called an inverse of the other respectively. 

The inverse of $T$ is denoted by $T^{-1}$, and it is unique.

**Proposition (invertibility == injectivity + surjectivity)** A linear map is invertible iff it is injective and surjective

**Definition (isomorphism, isomorphic)** An isomorphism is an invertible linear map, two vector spaces are called isomorphic if there is an isomorphism from one onto the other

**Proposition (dimension and isomorphism)** Two finite-dim vector spaces are isomorphic iff they have the same dim

**Definition (operator)** An operator $T \in \mathcal{L}(V)$ is Da linear transformation $T$ for a vector space $V$ to itself. (endomorphism)

**Criterion (invertibility)** Following statements are equivalent in operator $T$ in finite dimensional vector space

- $T$ is invertible
- $T$ is injective
- $T$ is surjective

Note that neither injectivity nor surjectivity implies invertibility in infinite-dim vector spaces

### 3.4. Products
**Definition (product of vector spaces)** The product of vector space is defined by

$$V_1 \times V_2 ... \times V_m = \{ (v_1, ..., v_m) : v_1 \in V_1, ..., v_m \in V_m  \}$$ 

**Definition (sum of vector and subspace)** suppose $v \in V$ and $U$ is a subspace of $V$. 

$$v + U := \{ v + u : u \in U \} $$

**Defintion (affine subset, parallel)** An affine subset of $V$ is a subset of $V$ of the form $v + U$ where $v \in V$ and $U$ is a subspace of $V$, and the affine subset $v+U$ is said to be parallel to $U$

### 3.5. Quotients
following binary relation on $V$ where $S \subset V$ is a subspace is an equivalence relation

$$ u \equiv v \iff u - v \in S$$

**Definition (quotient space)** Suppose $U$ is a subspace of $V$, then the quotient space $V/U$ is the set of all affine subsets of $V$ parallel to $U$

$$V/U := \{ v + U : v \in V \}$$

The set $v+U$ is called a coset of $U$ and $v$ is called a coset representative.

**Definition (addition, scalar multiplication on quotient space)** 
$$ (v+U) + (w+U) = (v+w) + U$$

$$ \lambda (v+U) = (\lambda v) + U$$

quotient space forms vector space with these definitions. However, not all structures in algebra has this property, for example subgroup. Only normal subgroup has this property where $G/N$ is a group. For rings, ideals have this property.

**Definition (quotient map, canonical projection)** quotient map (actually a linear map) $\pi: V \to V/U$ is defined

$$ \pi(v) = v + U $$

**Definition ($\widetilde{T}$)** Suppose $T \in \mathcal{L}(V,W)$. Define $\widetilde{T}: V/(null T) \to W$ by 

$$ \widetilde{T}(v + null T) = Tv$$

**Theorem (first isomorphism theorem)** $\widetilde{T}$ is injective

### 3.6. Duality
**Definition (linear functional)** A linear functional on $V$ is a linear map from $V$ to $F$. In other words, it is an element of $\mathcal{L}(V, F)$

**Definition (dual space)** The dual space of $V$, denoted $V'=\mathcal{L}(V, F)$, is the vector space of all linear functionals on $V$

**Definition (dual basis)** dual basis of $V$'s basis $v_1, ..., v_n$ is the list $\varphi_1, ... \varphi_n$ of element of $V'$ where $\varphi_j(v_k)=1$ iff $k==j$, otherwise 0. Dual basis is a basis of $V'$

**Definition (dual map)** dual map of $T \in \mathcal{L}(V,W)$ is the linear map $T' \in \mathcal{L}(W', V')$ defined by $T'(\varphi)=\varphi \circ T$

**Definition (annihilator)** The annihilator of $U \subset V$, denoted by $U^{\circ}$ is the subspace of linear functionals collapsing $U$ to 0

$$ U^{\circ} = \{ \varphi \in V' | (\forall u \in U) \varphi(u) = 0 \}$$

## 4. Eigenvalues and Eigenvectors
### 4.1. Invariant Subspaces
**Definition (invariant subspace)** Suppose $T \in \mathcal{L}(V)$ A subspace $U$ of $V$ is called invariant under $T$ if $u\in U \implies Tu \in U$

$U$ is invariant under $T$ is $T|_{U}$ is an operator on $U$

Note: ${0}, V, null(T), range(T)$ are invariant subspaces of $T$.

**Definition (eigenvalue, eigenvector)** Suppose $T \in \mathcal{L}(V)$. A number $\lambda \in F$ is called an eigenvalue of $T$ if there exists a non-zero $v \in V$ and $Tv = \lambda v$, and $v$ is called eigenvector of $T$ corresponding to eigenvalue $\lambda$

note: eigenvector is the basis of 1-dim invariant subspace of $T$

**Criterion (eigenvalue)** Suppose $V$ is finite-dimensional, $T \in \mathcal{L}(V), \lambda \in F$. Then $lambda$ is an eigenvalue of $T$ in either of the following case

- $T - \lambda I$ is not injective
- $T - \lambda I$ is not surjective
- $T - \lambda I$ is not invertible


**Definition (restriction and quotient operators)** Suppose $T \in \mathcal{L}(V)$ and $U$ is a subspace of $V$ invariant under $T$

The restriction operator $T|_{U} \in \mathcal{L}(U)$ is defined by

$$\forall (u \in U) T|_{U}(u) = Tu$$

The quotient operator $T/U \in \mathcal{L}(V/U)$ is defined by

$$\forall (u \in U) (T/U)(v+U)=Tv + U$$

### 4.2. Upper-Triangular Matrices
The main reason that a richer theory exists for operators than for more general limear maps is that operators can be raised to powers

**Definition (matrix of an operator)** Suppose $T \in \mathcal{L}(V)$ and $v_1, ..., v_n$ is a basis of $V$. The matrix of $T$ with respect to this basis is the n-by-n matrix whose entries $A_{j,k}$ are defined by $Tv_k = A_{1,k} v_1 + ... + A_{n,k} v_n$

**Definition (diagonal of a matrix)** The diagonal of a square matrix consists of the entries along the line from the upper left corner  to the bottom right corner

**Definition (upper-triangular matrix)** A matrix is called upper triangular if all the entries below the diagnoal equal 0

**Proposition (conditions for upper-triangular matrix)** Suppose $T \in \mathcal{L}(V)$ and $v_1, ..., v_n$ is a basis of $V$. Then the following are equivalent

the matrix of $T$ with respect to $v_1, ..., v_n$ is upper triangular
$(\forall j) Tv_j \in span(v_1, ..., v_j)$
$span(v_1, ..., v_j)$ is invariant under $T$ for each $j$

**Proposition  (every operator over C has an upper-triangular matrix)** Suppose $V$ is a finite-dimensional complex vector space and $T \in \mathcal{L}(V)$. Then $T$ has an upper-triangular matrix with respect to some basis of $V

### 4.3. Diagonal Matrices
**Definition (diagonal matrix)** A diagonal matrix is a square matrix that is 0 everywhere except possibly along the diagonal

**Definition (eigenspace)** Suppose $T \in \mathcal{L}(V), \lambda \in F$. The eigenspace of $T$ corresponding to $\lambda$ denoted $E(\lambda, T)$ is defined by

$$E(\lambda, T) = null(T - \lambda I)$$

**Proposition (Sum of eigenspaces is a direct sum)** Suppose $V$ is finite-dimensional and $T \in \mathcal{L}(V)$. Suppose also that $\lambda_1, ..., \lambda_m$ are distinct eigenvalues of $T$. Then $E(\lambda_1, T) + ... + E(\lambda_m, T)$ is a direct sum. Futhermore, $\dim (E(\lambda_1, T)) + ... + \dim E(\lambda_m, T) \leq \dim V$

**Definition (diagonalizable)** An operator $T \in \mathcal{L}(V)$ is called diagonalizable if the operator has a diagonal matrix with respect to some basis of $V$

**Proposition (conditions equivalent to diagonalizability)** Suppose $V$ is finite-dimensional and $T \in \mathcal{L}(V)$. Let $\lambda_1, ..., \lambda_m$ detnoe the distinct eigenvalues of $T$. Then the following are equivalent:

- $T$ is diagonalizable
- $V$ has a basis consisting of eigenvectors of $T$
there exist 1-dimensional subspaces $U_1, ..., U_n$ of $V$, each invariant under $T$, such that $V = U_1 \oplus ... \oplus U_n$
- $V = E(\lambda_1, T) \oplus ... \oplus E(\lambda_m, T)$
- $\dim V = \dim E(\lambda_1, T) + ... + \dim E(\lambda_m, T)$

**Proposition (enough eigenvalues implies diagonalizability)** If $T \in \mathcal{L}(V)$ has dim $V$ distinct eigenvalues, then $T$ is diagonalizable.

## 5. Operators on Inner Product Spaces
**Definition (adjoint)** Suppose $T \in \mathcal{L}(V,W)$. The adjoint of $T$ is the function $T^* : W \to V$ such that

$$(\forall v \in V)(\forall w \in W) \langle Tv, w \rangle = \langle v, T^*w \rangle$$

**Lemma (adjoint is a linear map)** If $T \in \mathcal{L}(V,W)$, then $T^* \in \mathcal{L}(W,V)$ 

**Lemma (The matrix of $T^*$)** Let $T \in \mathcal{L}(V,W)$ Suppose $e_1, ..., e_n$ is an orthonormal basis of $V$ and $f_1, ..., f_m$ is an orthonormal basis of $W$. Then $\mathcal{M}(T^*, (f_1, ..., f_m), (e_1,...,e_n))$ is the conjugate transpose of $\mathcal{M}(T, (e_1,..., e_n), (f_1, ..., f_m))$

### 5.1. Normal Operator
Normal operator is similar to complex number.

**Definition (normal operator)** An operator $T$ is called normal iff $TT^* = T^*T$

**Lemma (properties of normal operator)**
An operator $T$ is normal iff $||Tv|| = ||T^*v||$
If $T$ is normal, and $v$ is an eigenvector of $T$ with eigenvalue of $\lambda$, Then $v$ is also an eigenvector of $T^*$ with eigenvalue $\overline{\lambda}$
If $T$ is normal, then eigenvectors of $T$ corresponding to distinct eigenvalues are orthogonal
Theorem (complex spectral theorem) $T \in \mathcal{L}(V)$ is normal where field is $C$ $\iff$ $T$ can be diagonalized with respect to some orthonormal basis of $V$

### 5.2. Hermitian Operator
Hermitian operator is similar to real number

**Definition (Hermitian operator, self-adjoint operator)** An operator $T \in \mathcal{L}(V)$ is called hermitian or self-adjoint if $T = T^*$ 

$$\langle Tv, w \rangle = \langle v, Tw \rangle$$

**Lemma (properties of self-adjoint)**
Every eigenvalue of self-adjoint operator is real
over C, $((\forall v) \langle Tv, v \rangle = 0) \iff T = 0 $
over C, $(\forall v) \langle Tv, v \rangle \in R \iff T=T^*$
If $T=T^* \land (\forall v \in V) \langle Tv, v \rangle = 0 \iff T =0$

**Theorem (real spectral theorem)** $T \in \mathcal{L}(V)$ is self-adjoint where field is $R$ $\iff$ $T$ can be diagonalized with respect to some orthonormal basis of $V$

### 5.3. Positive Operator
positive operator is similar to non-negative number

**Definition (positive operator)** An operator $T \in \mathcal{L}(V)$ is called positive if $T$ is self-adjoint and $\langle Tv, v \rangle \geq 0$ for all $v \in V$

### 5.4. Unitary Operator
unitary operator is similar to 1

**Definition (isometry, unitary operator)** An operator $S \in \mathcal{L}(V)$ is called isometry if $ ||Sv || = ||v||$ for all $v \in V$

## 6. Operators on Complex Vector Spaces
### 6.1. Generalized Eigenvectors
**Proposition (space decomposition)** Suppose $T \in \mathcal{L}(V)$, and $n=\dim V$, then

$$V = null T^n  \oplus range T^n$$

Note that it is true that $V = null T  \oplus range T$

**Definition (generalized eigenvector)** Suppose $T \in \mathcal{L}(V)$ and $\lambda$ is an eigenvalue of $T$. A vector $v \in V$ is called a generalized eigenvector of $T$ corresponding to $\lambda$ if $v \neq 0$ and for some positive number $j$

$$(T-\lambda I)^j v = 0$$

**Definition (generalized eigenspace)** Suppose $T \in \mathcal{L}(V), \lambda \in F$. The generalized eigenspace of $T$ corresponding to $\lambda$, denoted $G(\lambda, T)$, is defined to be the set of all generalized eigenvectors of $T$ corresponding to $\lambda$

**Proposition (description of generalized eigenspace)** Suppose $T \in \mathcal{L}(V), \lambda \in F$, Then 

$$G(\lambda, T) = null (T - \lambda I)^{\dim V}$$

**Definition (nilpotent)** An operator is called nilpotent if some power of it equals to $0$. 

Note that this is a generalization of zero operator

**Lemma (description of nilpotent operator)** Suppose $N \in \mathcal{L}(V)$ is nilpotent, then $N^{\dim V} = 0$

### 6.2. Operator Decomposition
**Proposition (operator domain decomposition)** Suppose $V$ is a complex vector space and $T \in \mathcal{L}(V)$. Let $\lambda_1, ..., \lambda_m$ be the distinct eigenvalues of $T$. Then

$$V = \oplus_{i=1}^m G(\lambda_i, T)$$

**Lemma (basis of generalized eigenvectors)** Suppose $V$ is a complex vector space and $T \in \mathcal{L}(V)$, then there is a basis of $V$ consisting of generalized eigenvectors of $T$

**Definition (multiplicity)** The multiplicity of an eigenvalue $\lambda$ of $T$ is defined to be the dimension of the corresponding generalized eigenspace $G(\lambda, T)$ (i.e., $\dim null(T- \lambda I)^{\dim V}$)

**Proposition (square roots of inertible operators over C)** Suppose $V$ is a complex vector space and $T \in \mathcal{L}(V)$ is invertible, then $T$ has a square root

### 6.3. Characteristic and Minimal Polynomials
**Definition (characteristic polynomial)** Suppose $V$ is a complex vector space and $T \in \mathcal{L}(V)$. Let $\lambda_1, ..., \lambda_m$ denote the distinct eigenvalues of $T$, with multiplicities $d_1, ..., d_m$. The following polynomial is called the characteristic polynomials of $T$

$$ \prod_{i} (z - \lambda_i)^{d_i}$$

**Theorem (Cayley-Hamilton)** Suppose $V$ is a complex vector space and $T \in \mathcal{L}(V)$. Let $q$ denote the characteristic polynomial of $T$. Then $q(T)=0$

## 7. Operators on Real Vector Spaces


## 8. Reference
[1] Axler, Sheldon Jay. Linear algebra done right. Vol. 2. New York: Springer, 1997.

[2] Roman, Steven, S. Axler, and F. W. Gehring. Advanced linear algebra. Vol. 3. New York: Springer, 2005.

[3] Boyd, Stephen, and Lieven Vandenberghe. Introduction to applied linear algebra: vectors, matrices, and least squares. Cambridge university press, 2018.

