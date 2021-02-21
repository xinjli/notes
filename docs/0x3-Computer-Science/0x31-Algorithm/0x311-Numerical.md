# 0x311 Numerical Algorithm

- [1. Matrix Computation](#1-matrix-computation)
    - [1.1. Foundation](#11-foundation)
        - [1.1.1. QR Algorithms](#111-qr-algorithms)
            - [1.1.1.1. Gram-Schmidt algorithm](#1111-gram-schmidt-algorithm)
            - [1.1.1.2. Modified Gram-Schmidt algorithm](#1112-modified-gram-schmidt-algorithm)
            - [1.1.1.3. Householder Triangularization](#1113-householder-triangularization)
    - [1.2. Eigenvalue and Eigenvectors](#12-eigenvalue-and-eigenvectors)
    - [1.3. Least Square Problems](#13-least-square-problems)
    - [1.4. Stability and Conditioning](#14-stability-and-conditioning)
        - [1.4.1. Condition Number](#141-condition-number)
- [2. Differentiation](#2-differentiation)
- [3. Integral](#3-integral)
- [4. Reference](#4-reference)

## 1. Matrix Computation
### 1.1. Foundation
#### 1.1.1. QR Algorithms
QR algorithm is one of the most important algorithm used in numerical matrix analysis. For example, it can be used to solve the linear equation 

$$Ax = B$$
By following steps 
- factorizing $A = QR$
- $Rx = Q^* B$
- solve previous one backward

Note that it is not the most efficient solution.

##### 1.1.1.1. Gram-Schmidt algorithm
The classical GS algorithm is to normalize each column by removing previous orthogonal components backward. This computes a single orthogonal projection of rank $m-(j-1)$ by
$$v_j = P_j a_j$$

It is not stable due to the rounding error issue.

```python
for j=1 to n
    v_j = a_j
    for i=1 to j-1
        r_ij = q_i*a_j
        v_j = v_j - r_ij*q_i
    r_jj = ||v_j||_2
    q_j = v_j / r_jj
```

##### 1.1.1.2. Modified Gram-Schmidt algorithm
Modified version decomposes the projection into $j-1$ projection of rank 1. It removes orthogonal components forward.
$$P_j = P_{\perp q_{j-1}} ... P_{\perp q_1}$$
```python
for i=1 to n
    r_ii = ||v_i||
    q_i = v_i / r_ii
    for j=i+1 to n
        r_ij = q_i*v_j
        v_j = v_j - r_ij q_i

```

Both classical and modified version requires flops around $2mn^2$, therefore $O(mn^2)$


##### 1.1.1.3. Householder Triangularization
Householder applies a succession of elementary unitary matrix $Q_k$ to create a upper-triangular
$$Q_n ... Q_2 Q_1 A = R$$
where $Q^* = Q_n .... Q_1$

Each $Q_i$ applies a Householder reflection to a submatrix, introducing zeros column by column.

```python
for k=1 to n
   x = A_{k:m,k}
   v_k = sign(x_1)||x||_2 e_1 + x
   v_k = v_k / ||v_k||_2
   A_{k:m,k:n} = A_{k:m,k:n} - 2 v_k(v_k*A_{k:m,k:n})
```

This will produce the triangular matrix $R$. $v_k$ is normal vector for hyperplanes, it can be used to act on other vectors. For example, to compute $Qx$

```python
for k=n downto 1
    x_{k:m} = x_{k:m} - 2 v_k(v_k* x_{k:m})
```
$Q^* x$ can be done similarly by reversing the order.

To construct $Q$ explicitly, we apply $Qx$ algorithm to $e_1, ..., e_m$
Householder flops is around $2mn^2 - 2/3(n^3)$, therefore better than GS algorithms.



### 1.2. Eigenvalue and Eigenvectors
**Algorithm (QR algorithm)** To find the eigenvalue of a given matrix. Iteratively compute $A_k = Q_k R_k$, then construct $A_{k+1} = R_k Q_k$ where $A_{k+1} \sim A_k$ and it converges to a triangular matrix (Schur form), in which eigenvalue can be easily identified

### 1.3. Least Square Problems
**Problem (least square problem)** Consider a linear system of equation

$$Ax = b$$

where $A \in \mathbb{C}^{m \times n}, m>n$. In general this problem has no solution and is *overdetermined*. Instead of solving this problem, we minimize the norm of residual

$$\text{minimize}_x ||b-Ax||_2$$

The best solution is to project $b$ into $A$'s column space. In this case, the residual vector is perp to A's column space, therefore the inner product is 0

$$A^* (b-Ax) = 0$$

This implies the normal equation

$$A^*A x = A^*b$$

When $A$ is consistent (full rank), $A^*A$ is non-singular, and 
$$x = (A^*A)^{-1}A^*b$$

The standard method to solve normal equation is not to take the inverse, we introduce 3 algorithms to solve normal equation. Each of them is advantageous in certain situations.

**Algorithm (Cholesky)** solve normal equation with Cholesky factorization, first rewrite the equation as
$$R^*Rx = A^*b$$

The applies forward, backward substitution.

**Algorithm (QR)** It is also possible to solve via QR, rewrite the normal equation as
$$Rx = Q^*b$$

then solve

**Algorithm (SVD)** rewrite the equation as
$$\Sigma V^* x = U^*b$$

then solve

### 1.4. Stability and Conditioning

#### 1.4.1. Condition Number
A *well-conditioned* problem is one with the property that all small perturbations of $x$ lead to only small changes in $f(x)$, while an *ill-conditioned* problem is the one that $x$ leads to large change in $f(x)$

The examples of *ill-conditioned* problems:
- roots of polynomial with pertubation to coefficients
- eigenvalues of nonsymmetric matrix

**Definition (absolute condition number)** The absolute condition number $\hat \kappa = \hat \kappa(x)$ of the problem $f$ at $x$ is defined as

$$\hat \kappa = \lim_{\delta \to 0} \sup_{||\delta x|| \leq \delta} \frac{||\delta f||}{||\delta x||}$$ 

If $f$ is differentiable, $\hat \kappa$ can be defined using Jacobian $J(x)$
$$\hat \kappa = ||J(x)||$$

**Definition (relative condition number)** The relative condition number $\kappa = \kappa(x)$$ is defined as

$$\kappa = \lim_{\delta \to 0} \sup_{||\delta x|| \leq \delta} \frac{||\delta f||}{||f(x)||} / \frac{||\delta x||}{||x||}$$ 

If differentiable,
$$\kappa = \frac{||J(x)||}{||f(x)||/||x||}$$


**Theorem (condition number of $Ax=b$)** Let $A \in \mathbb{C}^{m \times m}$ be nonsingular and consider the equation $Ax=b$, the problem of computing $b$, given $x$, has condition number

$$\kappa = ||A||||x||/||b|| \leq ||A|| ||A^{-1}||$$

with respect to pertubations of $x$. The problem of computing $x$, given $b$ has a similar condition number

The number on the right hand is called the condition number of $A$, denoted by $\kappa(A)$

$$\kappa(A) = ||A|| ||A^{-1}||$$

In the case of 2-norm, 

$$\kappa(A) = \frac{\sigma_1}{\sigma_m}$$



## 2. Differentiation

## 3. Integral
**Algorithm (Simpson)** Approximating definite integral as follows. Usually works very well

$$\int_{a}^{b} f(x) dx = \frac{dx}{3} (f(x_0) + 4f(x_1) + 2f(x_2) + 4f(x_3) + 2f(x_4) ... + 4f(x_{n-1}) + f(x_n)$$

## 4. Reference
- Trefethen, Lloyd N., and David Bau III. Numerical linear algebra. Vol. 50. Siam, 1997.