# 0x002 Sequence and Series

- [1. Sequence](#1-sequence)
    - [1.1. Sequence](#11-sequence)
        - [1.1.1. Convergence](#111-convergence)
        - [1.1.2. Convergence Criterions](#112-convergence-criterions)
        - [1.1.3. Subsequences](#113-subsequences)
        - [1.1.4. limsup, liminf](#114-limsup-liminf)
    - [1.2. Series](#12-series)
        - [1.2.1. Conditional Convergence](#121-conditional-convergence)
        - [1.2.2. Absolute Convergence](#122-absolute-convergence)
- [2. Function Sequence](#2-function-sequence)
    - [2.1. Function Sequence](#21-function-sequence)
        - [2.1.1. Pointwise Convergence](#211-pointwise-convergence)
        - [2.1.2. Uniform Convergence](#212-uniform-convergence)
            - [2.1.2.1. Properties of Uniform Convergence](#2121-properties-of-uniform-convergence)
    - [2.2. Function Series](#22-function-series)
        - [2.2.1. Convergence](#221-convergence)
        - [2.2.2. Power Series](#222-power-series)
        - [2.2.3. Taylor Series](#223-taylor-series)

## 1. Sequence

### 1.1. Sequence
This subsection is about

$$a_n \to a$$

#### 1.1.1. Convergence

**Definition (Convergence)** A sequence $(a_n)^{\infty}_{n=N}$ is convergent to $L$ iff the sequence is $L$ is eventually $\epsilon$-close to $L$ for every $\epsilon > 0$

$$ (\forall \epsilon) (\exists N) (\forall n \geq N)  ( |L - a_n| < \epsilon ) $$

**Theorem (Arithmetic Limit Laws)**
If $\lim a_n$ and $\lim b_n$ exists, then

$$ \lim_{n \to \infty} (a_n + b_n) = \lim_{n \to \infty} a_n + \lim_{n \to \infty} b_n $$

$$ \lim_{n \to \infty} (a_n b_n) = (\lim_{n \to \infty} a_n) (\lim_{n \to \infty} b_n) $$

$$ \lim_{n \to \infty} (c a_n) = c \lim_{n \to \infty} a_n $$

$$ \lim_{n \to \infty} \frac{a_n}{b_n} = \frac{ \lim_{n \to \infty} a_n } { \lim_{n \to \infty} b_n } $$

**Theorem (Order Limit Laws)** 
$$(\lim a_n = a) \land (\lim b_n=b) \land (a_n \leq b_n) \implies a \leq b$$

**Definition (sup/inf of sequences)** Let $(a_n)_{n=m}^\infty$ be a sequence of real numbers. Then we define $sup(a_n)_{n=m}^{\infty} := sup( \{ a_n : n \geq m \} )$

**Proposition (property of sequence sup)**
- (sup is an upper bound) $(\forall n \geq m) a_n \leq sup(a_n)_{n=m}^{\infty}$
- (sup is the least upper bound) $(\forall y < sup(a_n)_{n=m}^{\infty}) (\exists n \geq m) y \leq a_n \leq sup(a_n)_{n=m}^{\infty}$


The followings are some criterions useful to decide sequence convergence.

#### 1.1.2. Convergence Criterions

The next two criterions are important because they do not require explicit limit to prove convergence.
**Criterion (Cauchy)** A sequence converges iff it is a Cauchy sequence

**Criterion (Monotone bounded convergence)** Let  $(a_n)_{n=m}^{\infty}$ be a sequence of real numbers which has some finite upper bound $M \in R$ and which is also increasing. Then  $(a_n)_{n=m}^{\infty}$ is convergent and

$$ \lim_{n \to \infty} a_n = \sup(a_n)_{n=m}^{\infty} \leq M$$

**Criterion (squeeze test)** 

$$ (a_n \leq b_n \leq c_n) \land (L = \lim a_n = \lim c_n) \Longrightarrow \lim b_n = L $$

**Criterion (Cesaro means)** If $x_n$ converges, then the mean sequence $y_n$ also converges to the same limit

$$y_n = \frac{1}{\sum_{i=i}^{n} x_i}$$

#### 1.1.3. Subsequences
**Definition (subsequence)** $(b_n)$ iis a subsequence of $(a_n)$ iff there exists a function $f: \mathbb{N} \to \mathbb{N}$ that is strictly increasing such that $b_n = a_{f(n)}$

**Propositions (limits of subsequences)** Following statements are equivalent
- sequence $(a_n)$ converges to $L$
- every subsequence of $(a_n)$ converges to $L$
  
**Proposition (limit points of subsequences)** Following statements are equivalent
- $L$ is a limit point of sequence $(a_n)$
- There exists a subsequence of $(a_n)$ which converges to $L$
  
**Theorem (Bolzano-Weirstrass)** A bounded sequence has at least one convergent subsequence

 Proof: sequence bounded -> limsup is bounded -> limsup is a limit point -> subsequence exists


#### 1.1.4. limsup, liminf
limit points over a sequence is a more general concept of limit. limit, limsup and liminf are instances of limit points. Normal Limit requires all points to be close enough to its convergence eventually, whereas limit points only ask for infinite points to be close enough.

**Definition (limit points, adherent points over sequence)** $x$ is a limit points (adherent point) of $(a_n)_{n=m}^{\infty}$ when

$$ (\forall \epsilon) ( \forall N \geq m ) (\exists n \geq N) ( |x - a_n| \leq \epsilon ) $$

Intuitively, the sequence visits $\epsilon$ neighborhood of a limit point infinitely often (In contrast with the eventual visit of limits)

limsup and liminf are also special cases of limit points. Unlike limits, limsup and liminf exist for every sequence. I think they are useful to estimate the boundaries of sequences when they are oscillating.  

**Definition (limsup/liminf)** limsup is the inferior over supremum of all elements. liminf is the superior over inferiors. (Both are defined over the extended reals to handle the divergence case)

$$a_N^{+} := sup(a_n)_{n=N}^{\infty}$$

$$\limsup a_n := inf(a_N^{+})_{N=m}^{\infty}$$

Note limsup and liminf always exist for any sequence (it might be infity though)

**Proposition (properties of limsup/liminf)** Let $L^+$ be limsup and $L^-$ be liminf of sequence $(a_n)_{n=m}^{\infty}$. Then

- $\forall x > L^+$, the sequence $(a_n)_{n=m}^{\infty}$ are eventually less than $x$
- $\forall x < L^+$, the sequence $(a_n)_{n=m}^{\infty}$ exceeds $x$ infinitely often
- $\inf(a_n)_{n=m}^{\infty} \leq L^- \leq L^+ \leq \sup(a_n)_{n=m}^{\infty}$
- If $c$ is any limit points, then $L^- \leq c \leq L^+$
- If $L^+$ is finite, then it is a limit point
- $\lim_{n \to \infty} a_n \Longleftrightarrow c L^+ = L^- = c$
- 
**Lemma (sup/limsup preserves order)** if $a_n \leq b_n$, then

$$ \sup (a_n)_{n=m}^{\infty} \leq \sup (b_n)_{n=m}^{\infty}$$

$$ \limsup (a_n)_{n=m}^{\infty} \leq \limsup (b_n)_{n=m}^{\infty}$$

Proof: by contradition. Suppose $\sup (a_n)_{n=m}^{\infty} > \sup (b_n)_{n=m}^{\infty}$, then take an $epsilon$ smaller than two sup diff, there exists one $a_n$ be $epsilon$ closer enough to its sup. This $a_n$ is larger than b's sup, so its larger than every b.

### 1.2. Series

This subsection is about

$$\sum_{n=0}^{\infty} a_n \to a$$

There are two types of convergence in series convergence: absolute convergence and conditional convergence. When a series converges absolutely, then it allows many manipulations such as rearrangement.

$$\text{Absolute Convergence } \subset \text{Conditional Convergence} $$

The series convergence is defined with respect to the convergence of the partial sum.
**Definition (series convergence)** The convergence of series $\sum_{k=0}^{\infty} a_k$ is defined in terms of the convergence of partial sum $s_n = \sum_{k=1}^n a_k$

$$\sum_{n=0}^{\infty} a_n = \lim_{n \to \infty} s_n$$

!!! note "Example (Basel problem)"
    The following series is a convergent series, firstly solved by Euler.
    $$\sum_{i=1}^{\infty} \frac{1}{n^2} = 1 + \frac{1}{2^2} + \frac{1}{3^2} + ... = \frac{\pi^2}{6}$$

  

**Theorem (Algebraic limit theorem for series)** If $\sum_{k=0}^{\infty} a_k = A$ and $\sum_{k=0}^{\infty} b_k = B$, then

$$\sum_{k=0}^{\infty} c a_k = cA$$

$$\sum_{k=0}^{\infty} (a_k + b_k) = A + B$$

#### 1.2.1. Conditional Convergence
**Definition (conditional convergence)** If $\sum_{k=0}^{\infty} |a_k|$ not converge but $\sum_{k=0}^{\infty} a_k$ converges, then $\sum_{k=0}^{\infty} a_k$ is called *conditional convergence*

!!! example "Alternating Harmonic Series"

    The alternating harmonic series is an example of conditional convergence, it does not converge absolutely.

    $$\sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{n} $$


#### 1.2.2. Absolute Convergence
Absolute convergence is a stronger version of convergence over series. (It does not make much in standard sequence though). It has many good properties such that allow rearrangement of sequence.

**Definition (absolute convergence)** If the $\sum_{k=0}^{\infty} |a_k|$ converges, then $\sum_{k=0}^{\infty} a_k$ will converge and is called *absolute convergence*. 

**Theorem (rearangement on absolute convergence)** If a series converges absolutely, then any rearangement of this series converges to the same limit

**Theorem (rearangement over double sum)** if $\sum_{i}^{\infty} \sum_{j}^{\infty} | a_{ij} |$  converges, then rearangement is allowed and gives the same value

$$\sum_{i}^{\infty} \sum_{j}^{\infty} a_{ij} = \sum_j^{\infty} \sum_i^{\infty} a_{ij} = \lim_{n \to \infty} \sum_{i}^n \sum_j^n a_{ij} $$

Generally, speaking, it is much easier to determine whether a sequence converges or not rather than to compute the actual sum. For example, the series

$$\sum_{n=1}^{\infty} \frac{1}{n^2}$$

can be easily confirmed that converges to something less than 2, but is much harder to compute its sum $\frac{\pi^2}{6}$, which by the way discovered by Euler. Followings are some useful criterions to determine whether an series converges or not

**Criterion (Cauchy)** The series $\sum_{k=0}^{\infty} a_k$ converges iff 

$$ (\forall \epsilon) (\exists N) (\forall n > m \geq N) |a_{m+1} + ... + a{n}| < \epsilon$$

**Criterion (comparison test)** Assume $a_k$ and $b_k$ are sequences satisfying $(\forall k \in N)0 \leq a_k \leq b_k$

if $\sum_{k=1}^{\infty} b_k$ converges, then $\sum_{k=1}^{\infty} a_k$ converges

if $\sum_{k=1}^{\infty} b_k$ diverges, then $\sum_{k=1}^{\infty} a_k$ diverges

**Criterion (absolute convergence test)** If series absolutely converges, then it converges as well

**Criterion (Leibniz, alternating series test)** Let $(a_n)$ be a sequence that $a_1 > a_2 > a_3 ...$ and $a_n \to 0$. Then the alternating series $\sum_{n=1}^{\infty} (-1)^{n+1} a_n$ converges.

**Criterion (ratio test)** Given a series $\sum_{n=1}^{\infty} a_n$, it will converges absolutely if

$$\lim | \frac{a_{n+1}}{a_n}| = r < 1 $$


**Criterion (Dirichlet's test)** If the partial sum of $\sum_{k=1}^{\infty} x_k$ are bounded, and $y_k$ are monotone decreasing to 0, then $\sum_{k=1}^{\infty} x_k y_k$ converges

## 2. Function Sequence
Infinite series representations of functions are both useful and elegant. Manipulations such as differentiation and anti-derivative can lead to remarkable conclusions when handled properly, however, they are not always justified.

### 2.1. Function Sequence

This subsection is about 

$$f_n \to f$$

#### 2.1.1. Pointwise Convergence

**Definition (pointwise convergence)** The sequence $(f_n)$ of functions converges pointwise on $A$ to a function $f$ if for all $x \in A$, the sequence of real numbers $f_n(x)$ converges to $f(x)$

The point here is that the convergence speed depends on the point $x$, it is possible for different values to require different, larger $N$ to bound diff into $\epsilon$

The problem of pointwise convergence is that it might not preserve good properties such as continuity and differentiability. To preserve those good properties, we need to propose a more restricted class of convergence.

!!! example "Counter Example (pointwise convergence does not preserve continuity)"
    Let $f_n(x)=x^n$ on the set $x \in [0,1]$ where $f_n(x)$ is continous function. when $n \to \infty$, it converges to 0 for $0 < x < 1$, 1 for $x=1$, which is not a continuous function

!!! example "Counter Example (pointwise convergence does not preserve differentiability)
    Let $f_n(x)=x^{1+\frac{1}{2n-1}}$ on the set $[-1,1]$. This function converges to $f(x)=|x|$, which is not differentiable.


#### 2.1.2. Uniform Convergence
pointwise convergence is a local property, while the uniform convergence is a global property. Uniform convergence have a couple of good properties as follows. It preserves continuity, differentiability and integrability.

**Definition (uniform convergence)** The sequence $(f_n)$ converges uniformly on $A$ to a limit function $f$ defined on $A$ if for every $\epsilon > 0$, there exists an $N$ such that $\forall (n \geq N) \forall (x \in A) |f_n(x) - f(x)| < \epsilon$

**Criterion (Cauchy)** $f_n$ converges uniformly to $f$ iff for every $\epsilon > 0$, there exists a $N$ such that

$$\forall(x)\forall(m,n \geq N) |f_n(x) - f_m(x)| < \epsilon$$

**Criterion (Dini's theorem)** Assume $f_n \to f$ pointwise on a compact set $K$ and assume that for each $x \in K$, the sequence $f_n(x)$ is increasing (wrt $n$). If $f_n, f$ are continuous on $K$, then $f_n \to f$ uniformly.

##### 2.1.2.1. Properties of Uniform Convergence
**Theorem (continuity)** Let $f_n$ be a sequence of functions defined on $A \subset R$ that converges uniformly on $A$ to a function $f$. If $f_n$ is continuous at $c \in A$, then $f$ is continuous at $c$

Proof idea is to evaluate $|f(x)-f(y)|$ by 3 pieces

$$|f(x)-f(y)| \leq |f(x) - f_n(x)| + |f_n(x)-f_n(y)| + |f(y)-f_n(y)|$$

where each piece can be bounded uniformly.

**Corrolary (uniform continuity)** uniform continuity is also preserved by uniform convergence by a similar proof

Both pointwise convergence and uniform convergence of $f_n$ implies nothing about the sequence of $f'_n$, neither uniform convergence or pointwise convergence of $f'_n$ is guaranteed.

!!! example "$f_n$ uniform convergence does not imply $f'_n$'s uniform convergence"

    Consider the function

    $$f_n(x) = \frac{x^n}{n}$$

    This function converges to 0 uniformly on $[0,1]$, however, $f'_n(x)$ is not converge uniformly on $[0,1]$

!!! example "$f_n$ uniform convergence does not even imply $f'_n$'s pointwise convergence"

    Consider the function
    
    $$f_n(x) = \frac{sin(nx)}{\sqrt{n}}$$

    This function converges to 0 uniformly on $R$ but $f'_n$ diverges for every $x$

**Theorem (differentiability)** Let $f_n$ be a sequence of differetiable functions defined on $[a,b]$ and $f'_{n}$ converges uniformly to a function $g$ on $[a,b]$. If there exists a point $x_0 \in [a,b]$ for which $f_n(x_0)$ is convergent, then $f_n$ converges uniformly. Moreover, the limit function $f=\lim f_n$ is differentiable and satisfies $f' = g$

Note again that $f_n$'s uniform convergence does not imply $f'_n$'s convergence, but $f'_n$'s uniform convergence almost implies $f_n$'s uniform convergence

!!! example "$\lim$ and $\int$ might not interchange when $f_n$ is pointwise convergence"

    Consider the function $f(x)$ with domain $[0,1]$

    $$f_n(x) = \begin{cases} n & \text{ if } 0 < x < 1/n \\ 0 & \text{ if } x=0, x\geq 1/n$$

    This converges pointwise to $f(x) = 0$ on $[0,1]$, however,

    $$0 \neq \lim_{n \to \infty} \int_0^1 f_n$$

Again, the interchange is valid when the convergence is uniform convergence
**Theorem (integrability)** Assume that $f_n \to f$ uniformly on $[a, b]$, and each $f_n$ is integrable. Then $f$ is integrable and

$$\lim_{n \to \infty} \int_a^b f_n = \int_a^b f$$

### 2.2. Function Series
This subsection is about 

$$\sum_{n=1}^{\infty} f_n(x) \to f(x)$$

#### 2.2.1. Convergence

**Definition (function series convergence)** For each $n$, let $f_n$ and $f$ be functions defined on a set $A$. The infinite series

$$\sum_{n=1}^{\infty} f_n(x)$$

*converges pointwise* on A to $f(x)$ iff the sequence $s_k(x)$ of partial sums defined by

$$s_k(x) = f_1(x) + f_2(x) + ... + f_k(x)$$

converges pointwise to $f(x)$. The series *converges uniformly* on $A$ to $f$ if the sequence $s_k(x)$ converges uniformly on $A$ to $f(x)$.

By applying uniform convergence properties to series, we get following conclusions.

**Theorem (Term-by-Term Continuity Theorem)** Let $f_n$ be continuous functions defined on a set $A$, and $\sum_{n=1}^{\infty} f_n$ converges uniformly on $A$ to a function $f$, then $f$ is continuous on $A$.

**Theorem (Term-by-Term Differentiability Theorem)** Let $f_n$ be differentiable functions defined on an interval $A$, and $\sum_{n=1}^{\infty} f'_n(x)$ converges uniformly to a limit $g(x)$ on $A$. If there exists a point $x_0 \in [a,b]$ where $\sum_{n=1}^{\infty} f_n(x_0)$ converges, then the series $\sum_{n=1}^{\infty} f_n(x)$ converges uniformly to a differentiable function $f(x)$ satisfying $f'(x)=g(x)$, which means

$$f'(x) = \sum_{n=1}^{\infty} f'_n(x)$$

**Criterion (Cauchy)** A series $\sum_{i} f_n$ converges uniformly on $A \subseteq R$ iff

$$ (\forall \epsilon > 0) (\exists N) (\forall m > m \geq N)| f_{m+1} + ... + f_{n} | < \epsilon$$

**Criterion (Weierstrass M-test)** For each $n \in N$, let $f_n$ be a function defined on a set $A \subset R$ and let $M_n > 0$ be a real number satisfying 

$$|f_n(x)| \leq M_n$$

where $\sum_{n=1}^{\infty} M_n$ converges, then $\sum_{n=1}^{\infty} f_n$ converges uniformly on $A$

!!! example "M-test's opposite is not true"
    It $f_n$ converges uniformly, it does not always exist a upper bound convergent series $M_n$, think about the constant function of the alternating harmonic series

    $$f_n(x) = \frac{(-1)^{n+1}}{n}$$

#### 2.2.2. Power Series
**Definition (power series)** a power series centered at $a \in \mathcal{R}$ is any series of the form

$$\sum_{n=0}^{\infty} c_n (x-a)^n$$

where $c_n$ is a sequence of real numbers not depending on $x$

**Definition (radius of convergence)** Let $\sum_{n=0}^{\infty} c_n (x-a)^n$ be a formal power series. we define the radius of convergence $R$ of this series to be 

$$R := \frac{1}{\limsup_{n \to \infty} |c_n|^{1/n}} $$

There are three cases depending on the radius of convergence

!!! note "Example (radius is 0)"

    Consider the series

    $$\sum n! x^n$$

    This has the radius of convergece $R=0$, it converges only at 0, and diverges all other points

!!! note "Example (radius is infinity)"

    Consider the series

    $$\sum \frac{x^n}{n!}$$

    This is $e^x$ and has radius of convergence $R=\infty$, it converges at every point

!!! note "Example (radius = r)"

    When radius=r, there are 4 possibility of convergence set 
    
    1) convergence happens at $(-r, r)$
   
    $$\sum x^n$$

    1) convergence happens at $[-r, r)$
    
    $$\sum \frac{1}{n} x^n$$

    1) convergence happens at $(-r, r]$
    
    $$\sum \frac{(-1)^{n}}{n} x^n$$

    1) convergence happens at $[-r, r]$
    
    $$\sum \frac{1}{n^2} x^n$$


**Theorem** If a power series $\sum_{n=0}^{\infty} a_n x^n$ has the raidus of convergence $R$, then it converges absolutely for any $x$ such that $|x| < R$. It diverges for any $x$ when $|x| > R$

The main implication here is that the set of convergence has to be ${0}, R$ or a bounded interval.

**Theorem (Abel)** Let $g(x) = \sum_{n=0}^{\infty} a_n x^n$ be a power series that converge at $x=R > 0$, then it converges uniformly on the interval $[0, R]$.

**Theorem** If a power series converges pointwise on the set $A \subseteq R$, then it converges uniformly on any compact set $K \subseteq A$

**Theorem** Assume $f(x)=\sum_{n=0}^{\infty} a_n x^n$ converges on an interval $A \subseteq R$. The function $f$ is continuous on $A$ and differentiable on any open interval $(-R,R) \subseteq A$. The derivative is given by $f'(x) = \sum_{n=1}^{\infty} na_n x^{n-1}$.

On its interval of convergence, a power series can be manipulated more or less as if they are polynomials: they are continuous and infinitely differentiable. Successive derivatives and antiderivatives can be computed by performing the desired operation on each individual term in the series.

#### 2.2.3. Taylor Series
**Theorem (Taylor series)** Let $f(x)$ has a power series representation. i.e.: 
$$f(x) = a_0 + a_1 x + a_2 x^2 a_3 x^3 ...$$
be defined on some nontrivial interval centered at zero, then

$$a_n = \frac{f^{(n)}(0)}{n!}$$

Therefore, the *Talyor series (Maclaurin series)* is

$$\sum_{n=0}^{\infty} \frac{f^{(n)}(0)}{n!} x^n$$

Note this is saying if $f(x)$ has a power series, then it has to be the Taylor series.
It is not saying that the Taylor series has to be the power series representation.

!!! note "Example (Talyor series might not be convergent on R)"
    Consider the following representation

    $$\frac{1}{1-x} = \sum_n x^n$$

    This series is only convergent in (-1,1)

The following example shows that not every infinitely differentiable function can be represented by its Taylor series.
!!! note "Example (Even Taylor series converges, it might not converges to the target function)"

    Consider the function
    $$f(x) = \begin{cases} e^{(-1/x^2)} & \text{ for } x \neq 0 \\ 0 \text{ for } x=0 \end{cases}$$

    The Taylor series of this function is $0$ everywhere, therefore it does not converges to the original $f(x)

To measure the diff between the Talyor series and the actual value, we have a powerful tool.
**Theorem (Lagrange's Remainder Theorem)** Let $f$ be differentiable $N+1$ times on $(-R, R)$, define $a_n = f^{(n)}(0)/n!$, Given $x \neq 0$ in $(-R,R)$, there exists a point $c$ such that $|c| < |x|$ , then the error function $E_N(x) = f(x) - S_N(x)$ is

$$E_N(x) = \frac{f^{N+1}(c)}{(N+1)!}x^{N+1}$$


**Theorem (Stone-Weierstrass)** Let $f: [a,b] \to R$ be continuous. Given $\epsilon > 0$ there exists a polynomial $p(x)$ satisfying $\forall{x \in [a,b] }$

$$| f(x) - p(x) | < \epsilon $$

Note the requirement here is only the continuity, not infinite differentiability.

Note that not all infinitely differentiable function can be represented by its Taylor series. There are cases that Taylor series not converging to the target function.

Reference
[1] Tao, Terence. Analysis. Vol. 1. Hindustan Book Agency, 2006.

[2]  Tao, Terence. Analysis. Vol. 2. Hindustan Book Agency, 2006.

[3] Abbott, Stephen. Understanding analysis. Vol. 2. New York: Springer, 2001.

[4] Lax, Peter D., and Maria Shea Terrell. Multivariable Calculus with Applications. Springer, 2017.

[5] 杉浦光夫. "解析入門 I." 東京大学出版会
[6] 杉浦光夫. "解析入門 II." 東京大学出版会
