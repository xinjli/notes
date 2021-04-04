# 0x040 Probability

- [1. Probability Theory](#1-probability-theory)
    - [1.1. Basic Concepts](#11-basic-concepts)
    - [1.2. Conditional Probability](#12-conditional-probability)
    - [1.3. Random variable](#13-random-variable)
    - [1.4. Distribution](#14-distribution)
- [2. Univariate models](#2-univariate-models)
    - [2.1. Transformation](#21-transformation)
    - [2.2. Expectation and Variance](#22-expectation-and-variance)
    - [2.3. Moments](#23-moments)
- [3. Multivariate Models](#3-multivariate-models)
    - [3.1. Joint and Marginal Distributions](#31-joint-and-marginal-distributions)
    - [3.2. Conditioning and Independence](#32-conditioning-and-independence)
    - [3.3. Bivariate Transformation](#33-bivariate-transformation)
    - [3.4. Hierarchical/Mixture Models](#34-hierarchicalmixture-models)
    - [3.5. Covariance and Correlation](#35-covariance-and-correlation)
    - [3.6. Multivariable Models](#36-multivariable-models)
- [4. Convergence](#4-convergence)
    - [4.1. Inequalities and Tail Bound](#41-inequalities-and-tail-bound)
    - [4.2. Convergence Concepts](#42-convergence-concepts)
- [5. Reference](#5-reference)

## 1. Probability Theory
### 1.1. Basic Concepts

**Definition (sample space)** $\Omega$ is called the sample space. Intuitively,  it is the set of possible outcomes of an experiment. 

Unfortunately, we can not assign measure to every subset of sample space in general, therefore, we only consider the event space which is a subset of all subsets.
**Definition (event space)** $\mathcal{F}$ is called the event space when $\mathcal{F}$ is a $\sigma$-algebra on a set $\Omega$. An event is an element of $\mathcal{F}$ 

On this proper event space, we can define the probability measure
**Definition (probability measure)** A probability measure on $(\Omega, \mathcal{F})$ is a measure $P$ on $(\Omega, \mathcal{F})$ such that $P(\Omega)=1$. If $A$ is an event, then $P(A)$ is called the probability of $A$

With these three components, we can define the probability space
**Definition (probability space)** If $P$ is a probability measure on $(\Omega, \mathcal{F})$, then the triplet $(\Omega, \mathcal{F}, P)$ is called a probability space.

To form a valid probability, we need a couple of more contraints, which induced by Andrey Kolmogorov in 1933.
**Axiom (Axiom of probability, Kolmogorov)**: A function $P$ that assigns a real number $P(A)$ to each event $A$ is a probability distribution or a probability measure if it satisfies the following three axioms.

- $P(A) \geq 0 $ for every A
- $P(\Omega)=1$
- $P(\cup_i A_i) = \sum_i P(A_i) $  if A are disjoint


**Frequentist vs Bayesian Interpretations** There are two interpretations $P(A)$. The two common interpretations are frequencies and degrees of beliefs. Frequentist says that $P(A)$ is the long run proportion of times that $A$ is true in reptitions. The degree of belief interpretation says that $P(A)$ is the observer's strength of belief that $A$ is true.

Note that probability in quantum mechanics probably does not belong to either of these interpretations.

**Lemma (Inclusion Exclusion Principle)** 

$$P(A \cup B) = P(A) + P(B) - P(AB)$$

**Theorem (Continuity of Probability)** If $A_n \rightarrow A$ then 

$$P(A_n) \rightarrow P(A)$$

**Definition (Discrete Probability Model)** Consider a sample space $S$. If $S$ is a countable set, this refers to a discrete probability model. 

In this case, since $S$ is countable, we can list all elements in $S$, $S = \{ s_1, s_2, ... \}$,  If $A \subset S$ is an event, then $A$ is also countable, and by the third axiom of probability, we can write

$$ P(A) = P(\cup_{s_j \in A}) = \sum_{s_j \in A} P(s_j) $$

In a finite sample space $S$,  where all outcomes are equally likely, the probability of any event $A$ can be found by $P(A) = \frac{|A|}{|S|}$

### 1.2. Conditional Probability
Conditional Probability
All probabilities are calculated with respect to a sample space, but in many cases, we are in a position to update the sample space with new information. In this case, we use conditional probability.

**Definition (Conditional Probability)** If $A,B$ are two events in a sample space and if $P(B) > 0$ then the conditional probability of $A$ given $B$ is 

$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$

Note that $B$ becomes that sample space here. In particular $P(\dot | B)$ is a probability (satisfying Kolmogorov's axioms)

For any fixed $B$ such that $P(B) > 0$, $P( \cdot | B)$ is a probability measure (satisfying three axioms of probability)

**prosecutor's fallacy**: fallacy from misunderstanding of $P(A|B) \neq P(B|A)$

**Lemma** : for any pair of events $A$ and $B$

$$P(AB) = P(A|B)P(B) = P(B|A)P(A)$$

**Theorem (The Law of Total Probability)** Let $A_1, ..., A_k$ be a partition of $\Sigma$, Then for any event $B$

$$P(B) = \sum_i P(B|A_i)P(A_i)$$

**Theorem (Bayes' Theorem)** 
$$ P(A_i | B) = \frac{P(B|A_i)P(A_i)}{\sum_j P(B|A_j)P(A_j)}$$

Independent Events
**Definition (Independence)** Two events $A$ and $B$ are independent if 

$$P(AB) = P(A)P(B)$$

Independence can arise in two distinct ways

- explicitly assume independence
- derive independence by verifying the previous definition
  
Note that disjoint events with positive probability is not independent.

Mutual independence is a much stronger assumption. Pairwise independence for all pairs does not imply mutual independence.

**Definition (mutual independence)** A collection of events $A_1, ..., A_n$ are mutually independent iff for any subcollection $A_{i_1}, ..., A_{i_k}$ 

$$P( \cap_{j=1}^{k} A_{i_{j}} ) = \prod_{j} P(A_{i_j})$$

### 1.3. Random variable
random variable is neither random nor a variable

**Definition (Random Variable)** Suppose $(\Omega, \mathcal{F}, P)$ is a probability space. A random variable on $(\Omega, \mathcal{F})$ is a measurable function from $\Omega$ to $R$. Intuitively, a random variable is a function from the sample space to another sample space (i.e. R)

Note that random variable can even be defined to project to measurable space other than $(R, B)$. 

**Definition ((more general) random variable)** Let $(E, \mathcal{E})$ be a measurable space. A mapping $X: \Omega \to E$ is called a random variable if $X$ is a measurable function with respect to $\mathcal{F}$ and $\mathcal{E}$, which means

$$\forall(A \in \mathcal{E}) X^{-1} (A) \in \mathcal{F}$$

**Definition (induced probability function)** The induced probability function with respect to the original function is defined as

$$ P_X(\{ x_i \}) =  P_X(X = x_i) = P( \{ s_j \in S | X(s_j) = x_i \} ) $$

Note that this is a formal probability distribution, which means it satisfies Kolmogorov's axioms

Note that $X$ is a discrete random variable if its range is countable

$$R_X = \{ x_1, x_2, ... \}$$

### 1.4. Distribution
**Definition (cumulative density function)** The cumulative density function of a random variable $X$, denoted by $F_X(x)$ is defined by

$$F_X(x) = P_X(X \leq x)$$

**Proposition (characterization of cdf)** The function $F(x)$ is a cdf iff

$\lim_{x \to -\infty} F(x) = 0$
$\lim_{x \to \infty} F(x) = 1$
$F(x)$ is nondecreasing function and right-continuous

**Definition (Probability Mass Function)** Let $X$ be a discrete random variable with range $R_x = \{ x_1, x_2, x_3, ... \}$ the following function is called the probability mass function of $X$

$$P_X(x_k) = P(X=x_k) = P( \{ x \in S | X(s) = x_k \}) $$

$$P(X \in A) = \sum_{x \in A} P_X(x)$$

By definition, PMF is a probability measure. In particular, we have

$$0 \leq P_X(x_k) \leq 1$$

$$\sum_{x \in R_X} P_X(x) =1$$

## 2. Univariate models

### 2.1. Transformation
**Definition (transformation)** If $X$ is a random variable, then any function of $X$, $g(X)$ is also a random variable (if $g$ is a Borel measurable function), then probability distribution of $Y$ is defined by

$$P(Y \in A) = P(X \in g^{-1}(A))$$

**Corollary (transformation of support)** It is important to keep track of the sample spaces of $X$ and $Y$, the support of $Y$ is

$$\mathcal{Y} = \{ y | (\exists x \in \mathcal{X}) y = g(x) \}$$

**Corollary (monotone transformation of cdf)** If $X$ have cdf $F_X(x)$, let $Y=g(X)$

if $g$ is an increasing function, then
$$F_Y(y) = F_X(g^{-1}(y))$$

if $g$ is a decreasing function, then

$$F_Y(y) = 1 - F_X(g^{-1}(y))$$

By taking derivative of both sides, we obtain the transformation rules of pdf for monotone functions.

**Theorem (monotone transformation of pdf)** Let $X$ have pdf $f_X(x)$ and $Y=g(X)$, where $g$ is a monotone function. Suppose $f_X(x)$ is continuous and $g^{-1}(y)$ has a continuous derivative on $\mathcal{Y}$, then

$$f_Y(y) = \begin{cases} f_X(g^{-1}(y))|\frac{d}{dy}g^{-1}(y)| & y \in \mathcal{Y} \\ 0 & \text{ otherwise}\end{cases}$$


Intuitively, the discussion above is simply

$$dF_X = dF_Y \implies f_X(x) dx = f_Y(y) dy$$

therefore, we get
$$f_Y(x) = f_X(x) |\frac{dx}{dy}|$$

!!! note

    this only applies to the monotone functions, for functions that are not monotone (e.g.: $Y=X^2$), we need to compute a partition of $X$ into where each $X_i$ is monotone over $g(X)$, then sum the inverse density $f_X(g^{-1}(y))$ with its weight $\frac{dg^{-1}(y)}{dy}$.



### 2.2. Expectation and Variance
**Definition (expectation)** Formally, Suppose $(\Omega, \mathcal{F}, P)$ is a probability space, If $X \in \mathcal{L}^1 (P)$, then the expectation of the random variable $X$ is devoted $EX$ and defined by

$$EX = \int_{\Omega} X dP$$

When $X$ is a discrete random variable with range $R_X = \{ x_1, x_2, ... \} $ (finite or countably infinite). The expected value of $X$, denoted by $EX$ is defined as

$$ EX = \sum_{x_k \in R_X} x_k P(X=x_k) $$

Note that expectation does not always exist for any distribution, for example, the Cauchy distribution does have an expectation

$$f_X(x) = \frac{1}{\pi} \frac{1}{1+x^2}$$

**Theorem (linearity of expectation)** 
$$ E(aX + b) = aE(X) + b$$

$$ E(X_1 + X_2 + ... + X_n) = EX_1 + EX_2 + ... + EX_n $$

**Theorem (expectation of transformation)** There are two ways to compute $E[g(X)]$. One way is to compute PMF of $Y = g(X)$, the other one is using follows (easier)

$$ E(g(X)) = \int g(x) f_X(x) dx$$

### 2.3. Moments
Moments reflects characteristics of distributions, however, the set of infinite moments is not enough to character the distribution. Two distinct random variables might have same moments set. To characterize distribution, both random variables have to have bounded support.

**Definition (moment, central moment)** For each integer $n$, the $n$-th moment of $X$, $mu_n$ is 

$$\mu^{'}_n = EX^n$$

The $n$th central moment of $X$, $\mu_n$ is

$$\mu_n = E(X-\mu)^n$$

The 2nd central moment is the variance defined as follows

**Definition (Variance)** The variance of a random variable $X$, with mean $EX = \mu_X$ is defined as

$$ Var(X) = E[ (X-\mu_X)^2 ] $$

The standard deviation of a random variable $X$ is defined as

$$SD(X) = \sigma_X = \sqrt{Var(X)}$$

A simple way to compute variance is as follows

$$Var(X) = E[X^2] - (EX)^2 $$

**Proposition (Properties of variance)**

$$Var(aX + b) = a^2Var(X)$$

$$Var(X) = Var(X_1) + Var(X_2) + ... Var(X_n) \text{  if } X = X_1 + X_2 + ... + X_n$$

$$Var(X+Y) = Var(X) + Var(Y) + 2Cov(X,Y)$$

If $X, Y$ are independent

$$Var(XY) = E(X^2Y^2) - (EXY)^2 = Var(X)Var(Y) + Var(X)E(Y)^2 + Var(Y)E(X)^2$$

**Definition (Standardized moment)** The standardized moment is the normalized central moment defined as

$$\hat{\mu}_k = \frac{\mu_k}{\sigma^k}$$

The 3rd standardized moment is called the skewness, which measures the lack of symmetry

The 4th standardized moment is called the kurtosis, which measures the peakedness of the pdf

While the moments might not be efficient to characterize distributions, the following moment generating function can characterize distributions if it exists

**Definition (moment generating function, mgf)** The moment generating function of $X$, denoted by $M_X(t)$ is following, provided that expectation exist for $t$ in some neighborhood of 0.

$$M_X(t) = Ee^{tX}$$

Note: $M_X(t)$ is the Laplace transform of $f_X(x)$

$$M_X(t) = \int_{-\infty}^{\infty} e^{tx} f_X(x) dx$$

**Lemma (algebra over mgf)**

$$M_{aX+b} = e^{bt} M_X(at)$$
$$M_{X+Y} = M_X(t)M_Y(t)$$

The moment generation function is called as it is because it can be used to generate moments by differentiation.

**Theorem (moment generation)** If $X$ has mgf $M_X(t)$, it can generate moments as follows

$$EX^n = M_X^{(n)} (0)$$

Note that the main use of the mgf is not to generate moments, but to characterize distributions, this characterizes an infinite set of moments. However, characterizing a infinite set of moments is not enough to determine a distribution uniquely. Two different distribution might have same moments.

To uniquely determine moments, we require the bounded support.

**Theorem (determinations of distribution)** Let $F_X(x), F_Y(y)$ be two cdfs all of whose moments exist, If the moment generating function exists and $M_X(t)=M_Y(t)$ for all $t$ in some neighborhood of 0, then

$$F_X(u) = F_Y(u)$$


**Theorem (convergence of mgfs)** Convergence for $|t| < h$ of mgfs to an mgf implies convergence of pdfs

While moment generating functions might not always exist, the characteristic function always exist and also characterize the random variable

**Definition (characteristic function)** The characteristic function for a random variable is defined as

$$\varphi_X(t) = E(e^{itX})$$

## 3. Multivariate Models
The probability models that involve more than one random variable are called *multivariate models*.

**Definition (n-dimensional random vector)** An n-dimensional random vector is a function from a sample space $S$ in to $R^n$, n-dimensional Euclidean space.

### 3.1. Joint and Marginal Distributions

The random vector is called a *discrete random vector* when it has only a countable number of possible values, otherwise it is called a *continuous random vector*.

**Definition (joint PMF)** Let $(X,Y)$ be a discrete bivariate random vector. Then the function $f(x,y): R^2 \to R$ defined by $f(x,y) = P(X=x, Y=y)$ is called the joint probability mass function or joint pmf of $(X,Y)$.

The joint pmf can be used to compute the probability of any event.

$$P((X,Y) \in A) = \sum_{(x,y) \in A} f(x,y)$$

**Definition (marginal PMF)** Let $(X,Y)$ be a discrete bivariate random vector with joint pmf $f_{X,Y}(x,y)$. Then the marginal pmfs of $X$, $f_X(x) = P(X = x)$ is given by

$$f_X(x) = \sum_{t \in R} f_{X,Y}(x,y)$$

**Definition (joint PDF)** A function $f(x,y): R^2 \to R$ is called a joint probability function or joint pdf of the continuous bivariate random vector $(X,Y)$ if for every event $A \in R^2$,

$$P((X,Y) \in A) = \iint_A f_{XY}(x,y) dxdy$$

**Definition (marginal PDF)** The marginal probability density function of $X,Y$ are also defined as in the discrete case with integrals replacing sums.

$$f_X(x) = \int_{-\infty}^{\infty} f_{XY}(x,y) dy$$

**Definition (joint CDF)** The joint distribution of $(X,Y)$ can also be completely described with the joint cdf

$$F_{XY}(x,y) = P(X \leq x, Y \leq y) = \int_{-\infty}^{y} \int_{-\infty}^{x} f_{XY}(u, v) du dv$$

### 3.2. Conditioning and Independence
Oftentimes when two random variables $(X,Y)$ are observed, the values of the two variables are related. Knowledge about the value of $X$ gives us some infomation about the value of $Y$.

**Definition (conditional pmf, pdf)** Let $(X,Y)$ be a discrete/continuous bivariate random vector with joint pmf/pdf $f(x,y)$ and marginal pmfs/pdfs $f_X(x), f_Y(y)$, the conditional pmf/pdf of $Y$ given that $X=x$ is the function of $y$ denoted by $f(y|x)$

$$ f_(y|x) = \frac{f(x,y)}{f_X(x)}$$

Note that this is a valid probability with respect to $y$.

Since $Y|x$ is a valid random variable, we can compute expectation of $g(Y)$
**Definition (Conditional expectation)** The conditional expected value of $g(Y)$ given that $X=x$ is denoted by $E(g(Y)|x)$

$$E(g(Y)|x) = \int g(y) f(y|x) dy$$

Note that this is a function of $x$

Similarly, we can compute the conditional variance of $Y|x$.

$$Var(Y|x) = E(Y^2|x) - (E(Y|x))^2$$

The conditional distribution of $Y$ given $X=x$ is possibly a different prob distribution for each $x$, therefore we have a family of prob distribution for $Y$ for each $x$, when we wish to describe this entire family, we use the phrase "the distribution of $Y|X$

In some situations, the knowledge that $X=x$ does not give us any information about $Y$, this relationship is called independence.

**Definition (independence)** Let $(X,Y)$ be a bivariate random vector with joint pdf or pmf $f(x,y)$ and marginal pdfs or pmfs $f_X(x), f_Y(y)$. Then $X,Y$ are called independent random variables if for every $x, y \in R$
$$f(x, y) = f_X(x) f_Y(y)$$

If they are independent

$$f(y|x) = f_Y(y)$$


To check that two random variables are independent, one way is to check **all** $x, y \in R$ combinations. This require the knowledge of $f_X(x), f_Y(y)$, which is sometimes difficult. 

**Criterion (joint pdf factorization)** Another good criterion is to check whether the joint distribution $f(x,y)$ can be factorized into two components as follows

$$f(x,y) = g(x) h(y)$$

Those independence can simplifying computations as follows

**Theorem (independent computing)** Suppose that $X,Y$ are independent random variables, then their events are also independent which means

$$P(X \in A, Y \in B) = P(X \in A) P(Y \in B)$$

The expectation can also be factorized into respective components

$$E(g(X)h(Y) = E(g(X)) E(h(Y))$$

Additionally, let $g(x)$ be a function only of $x$ and $h(y)$ be a function only of $y$, then the random variable $U=g(x), V=h(y)$ are independent

**Theorem** Let $X,Y$ be independent random variables. Let $g(X)$ be a function only of $x$ and $h(y)$ be a function only of $y$. Then the random variables $U,V$ are independent

$$U=g(X)$$
$$V=h(Y)$$

**Proposition (mgf of independent random variables)** Let $X,Y$ be independent random variables with moments generating functions $M_X(t), M_Y(t)$. Then the moment generating function of the random variable $Z = X+Y$ is given by

$$M_Z(t) = M_X(t) M_Y(t)$$

**Proposition (law of total probability)**
$$P(A) = \int_{-\infty}^{\infty} P(A|X=x) f_X(x) dx$$

**Proposition (two continuous random variables)**
$$E[g(X,Y)] = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} g(x,y) f_{XY}(x,y) dx dy$$

### 3.3. Bivariate Transformation

**Theorem (the method of transformations)** 
Let $X, Y$ be two jointly continuous random variables. Let $(Z,W) = g(X,Y) = (g_1(X,Y), g_2(X,Y))$ where $g: R^2 \to R^2$ is a continuous invertible function with continuous partial derivatives. Let $h = g^{-1}, ie.e., (X,Y) = h(Z,W) = (h_1(Z,W), h_2(Z,W))$ Then $Z,W$ are jointly continuous and their joint PDF $f_{ZW}(z,w)$ is given by

$$f_{ZW}(z,w) = f_{XY}(h_1(z,w), h_2(z,w)) |J|$$

where $J$ is the Jacobian of $h$

This can be used to compute multivariate distribution such as $X+Y, XY$

### 3.4. Hierarchical/Mixture Models
The advantage of the hierarchical models is that complicated process might be modeled by a sequence of relatively simple models.

**Definition (mixture model)** A random variable $X$ is said to have a mixture distribution if the distribution of $X$ depends on a quantity that also has a distribution.

Recall $E(X|y)$ is a function of $y$ and $E(X|Y)$ is a random variable whose value depends on $Y$
**Proposition (law of total expectation)** If $X,Y$ are any two random variables

$$ E[Y] = \int_{-\infty}^{\infty} E[Y|X=x] f_X(x) dx $$

$$ E[Y] = E[E[Y|X]] $$

!!! example "application of the law total expectation"

    Suppose we have two random variables $X,Y$ where
    
    $$X|Y \sim binomial(Y,p)$$
    $$Y \sim Poisson(\lambda)$$

    We can compute EX as follows

    $$EX = E[E[X|Y]] = E[pY] = p\lambda$$

Similarly we can expand the variance with respect to the other random variable.
**Proposition (law of total variance)**
$$Var(Y) = E[Var(Y|X)] + Var(E[Y|X])$$

There is an interesting interpretation in the Bayesian statistics, when $Y=\theta$

$$Var(\theta) = E[Var(\theta|X)] + Var(E(\theta|X))$$

This implies 

$$ E[Var(\theta|X)]  \leq Var(\theta)$$

which means on average, the posterior variance of $\theta$ given dataset $X$ is samller than the prior variance.

### 3.5. Covariance and Correlation
The covariance and correlation measure the strength of a kind of linear relationship.

**Definition (covariance)** The covariance between $X,Y$ is defined as 

$$\text{Cov}(X,Y) = E[(X - EX)(Y-EY)]$$

It can be simplified by

$$ \text{Cov}(X,Y) = E[XY] - (EX)(EY)$$

**Definition (correlation coefficient)** The correlation of $X,Y$ is the number defined by

$$\rho_{XY} = \frac{Cov(X,Y)}{\sigma_X \sigma_Y}$$

If we define $U,V$ as
$$U = \frac{X - EX}{\rho_X}, V = \frac{Y-EY}{\rho_Y}$$
then 

$$\rho_{XY} = Cov(U,V)$$


**Lemma (properties of covariance)**
- $Cov(X,X) = Var(X)$ 
- If $X, Y$ are independent then $Cov(X,Y)=0$
- $Cov(X,Y) = Cov(Y,X)$
- $Cov(aX,Y) = aCov(X,Y)$
- $Cov(X+c, y)=Cov(X,Y)$
- $Cov(X+Y, Z)=Cov(X,Z)+Cov(Y,Z)$
- $$Cov(\sum_i a_iX_i, \sum_j b_j Y_j) = \sum_i \sum_j a_i b_j Cov(X_i, Y_j)$$

**Proposition (independence and covariance)** If $X,Y$ are independent random variables, then $\text{Cov}(X,Y) = 0$

However, the opposite is not always true, i.e. covariance does not necessarily means independance.

Covariance and correlation measure only a particular kind of *linear* relationship.

!!! example "$(X,Y)$ has covariance 0 but dependent"

    Consider random variable $X$ is takes +/-1 with 0.5 prob each, $Y$ is 0 when $X=0$ and $Y=+/-1$ when $X=1$.

    It is clearly dependent but $Cov(X,Y) = 0$

**Proposition (variance of a sum)**
$$ Var(aX+bY) = a^2Var(X) + b^2Var(Y) + 2abCov(X,Y)$$

If $X,Y$ are independent

$$Var(aX+bY) = a^2Var(X)+b^2Var(Y)$$


**Proposition (properties of correlation coefficient)**
$ -1 \leq \rho(X,Y) \leq 1$
$\rho(aX+b, cY+d) = \rho(X,Y)$
If $X,Y$ are uncorrelated, then $Var(X+Y)=Var(X)+Var(Y)$

### 3.6. Multivariable Models
**Definition (multivariable random vector)** The random vector $X=(X_1, ..., X_n)$ has a sample space that is a subset of $R^n$. If $(X_1, ..., X_n)$ is a discrete random vector (sample space is countable), the joint pmf of $(X_1, X_2, ..., X_n)$ is defined by 

$$f(x) = f(x_1, ..., x_n) = P(X_1=x_1, ..., X_n=x_n)$$

then the for any $A \subset R^n$

$$P(X \in A) = \sum_{x \in A} f(x)$$

If $(X_1, ..., X_n)$ is a continuous random vector, 

$$P(X \in A) = \int_A f(x_1, ..., x_n) dx_1 ... dx_n$$

**Definition (expected value)** Let $g(x) = g(x_1, ..., x_n)$ be a real-valued function defined on the sample space of $X$. THen $g(X)$ is a random variable and expected value of $g(X)$ is 

$$Eg(X) = \int g(x) f(x) dx$$

**Definition (marginal pdf)**

$$f(x_1, ..., x_k) = \int f(x_1, ..., x_n) dx_{k+1} ... dx_n$$

**Definition (conditional pdf)** 

$$f(x_{k+1}, ..., x_n | x_1, ..., x_k) = \frac{f(x_1, ..., x_n)}{f(x_1, ..., x_k)}$$

**Definition (mutual indepednent random vector)** Let $X_1, ..., X_n$ be random vectors with joint pdf/pmf $f(x_1, ..., x_n$). Let $f_{X_i}(x_i)$ denote the marginal pdf/pmf of $X_i$, then $X_1, ..., X_n$ are called *mutually independent random vectors* if for every $x_1, ..., x_n$

$$f(x_1, ..., x_n) = f_{X_1}(x_1) \cdot ... \cdot f_{X_n}(x_n) = \prod_{i=1}^n f_{X_i}(x_i)$$

## 4. Convergence
### 4.1. Inequalities and Tail Bound
The following inequalities are mostly about the bound of distribution tail.

**Inequality (Markov)** Let $X$ be a nonnegative random variable (i.e. $X \geq 0$). Then

$$P(X \geq t) \leq \frac{EX}{t} = O(\frac{1}{t})$$

Chebyshev can be obtained from Markov inequality by taking the absolute value. (to maintain the nonnegativity)

It has a better bound  $O(\frac{1}{t^2})$ than Markov.

**Inequality (Chebyshev)** Let $X$ be a random variable and $EX = \mu, \mathrm{Var} X = \sigma^2$, then for any $t > 0$

$$P( | X - \mu | \geq t \sigma) \leq \frac{1}{t^2} = O(\frac{1}{t^2})$$

Chernoff bound can also be obtained from Markov inequality by taking exp.

Chebyshev's inequality is conservative and it has an better exponential bound.

**Inequality (Chernoff)** 
$$P((X - \mu) \geq u) = P(\exp(t(X-\mu)) \geq \exp(tu)) \leq \frac{E[\exp(t(X-\mu)]}{\exp(tu)}$$

Suppose mgf exist in a neighbourhood of $b$, then

$$P((X-\mu) \geq u) \leq \inf_{0 \leq t \leq b} \exp(-t(u+\mu)) E[\exp(tX)]$$

**Definition (sub-Gaussian random variable)** A sub-Gaussian random variable whose tails decay faster or equal than a Gaussian. Formally, a random variable $X$ with mean $\mu$ is sub-Gaussian if there exists a positive number $\sigma$ such that

$$E[\exp(t(X-\mu))] \leq \exp(\sigma^2 t^2/2)$$

**Inequality (Hoeffding)** Suppose a random variable is bound between $[a,b]$, then

$$P(|\bar{X} - \mu| < t) \leq 2 \exp (-\frac{2nt^2}{(b-a)^2})$$

**Inequality (Hölder)** Let $X,Y$ be any two random variables and $1/p + 1/q = 1$, then

$$|EXY| \leq E |XY| \leq (E|X|^p)^{1/p} (E|Y|^q)^{1/q}$$

**Inequality (Cauchy-Schwarz)** When $p=q=2$, it is the Cauchy-Schwarz inequality

$$|EXY| \leq E|XY| \leq (E|X|^2)^{1/2} (E|Y|^2)^{1/2}$$

**Inequality (Minkowski)** Let $X,Y$ be any two random variables and $ 1 \leq p \leq \infty$

$$(E|X+Y|^p)^{1/p} \leq (E|X|^p)^{1/p} + (E|Y|^{p})^{1/p}$$

**Inequality (Jensen)** For any random variable $X$, if $g(x)$ is a convex function, then

$$Eg(X) \geq g(EX)$$

### 4.2. Convergence Concepts
Convergence concepts are useful in approximating finite size sample because their expression can be simplified when taking limits. The relation between convergences are as follows:

almost sure convergence $\subset$ convergence in probability $\subset$ convergence in distribution

**Definition (almost sure convergence)** A sequence of random variables, $X_1,X_2, ...$ converges almost surely to a random variable $X$ if, for every $\epsilon > 0$

$$P(\lim_{n \to \infty} |X_n - X| \leq \epsilon) = 1$$

Formally, the almost sure convergence is defined as follows:

Let $\Omega$ be a set of probability mass $1$ ($P(\Omega)=1$), then for any $\omega \in Omega$ and for any $\epsilon > 0$, there exists a $N(\omega, \epsilon)$ such that when $n > N$

$$|X_n(\omega) - X(\omega)| \leq \epsilon$$

**Theorem (Strong Law of Large Numbers)** Let $X_1, X_2, ...$ be iid random variables with $EX_i = \mu$ and $Var(X_i) = \sigma^2 < \infty$, then for every $\epsilon > 0$

$$P(\lim_{n \to \infty} |\bar{X}_n  - \mu| < \epsilon) = 1$$

**Definition (convergence in probability)** A sequence of random variables $X_1, X_2, ..., $ converges in probability to a random variable $X$ if for every $\epsilon > 0$

$$\lim_{n \to \infty} P(|X_n - X| \geq \epsilon) = 0$$

Note that $X_n$ are usually not IID random variable, and $X$ is common to be a fixed number. The most famous result is the following one:

**Theorem (Weak Law of Large Numbers)** Let $X_1, X_2, ...$ be iid random variables with $EX_i=\mu, Var(X_i) = \sigma^2 < \infty$. Then for very $\epsilon > 0$

$$\lim_{n \to \infty} P(|\bar{X}_n - \mu|<\epsilon) = 1$$

that is, $\bar{X}_n$ converges in probability to $\mu$

This theorem can be proved by using the Chebychev's inequality

$$P(|\bar{X}_n - \mu| \geq \epsilon) = \frac{Var(\bar{X}}{\epsilon^2} = \frac{\sigma^2}{n \epsilon^2} \to 0$$

**Definition (convergence in quadratic mean)** Sometimes to show a stronger form of convergence is useful to prove convergence in probability. The following one is known as the convergence in quadratic mean
$$\lim_n E(X_n - X)^2 \to 0$$

Convergence in quadratic mean implies convergence in probability because

$$P(|X_n - X| \leq \epsilon) \leq \frac{E(X_n - X)^2}{\epsilon^2} \to 0$$

Intuitively, quadratic mean convergence penalizes the deviation by the square form while the probability convergence penalize deviation by the absolute form, therefore quadratic mean is a stronger form.

Convergence in probability is highly related to the consistency concept in statistics. Suppose we have an estimator $\hat{\theta}$ for some quantity $\theta$, $\hat{\theta}$ is said to be consistent if it converges to $\theta$ in probability.

One related useful theorem about consistency is the following one

**Theorem (consistency preserved by continuous function)** Suppose $X_1, X_2, ...$ converges in probability to a random variable $X$ and that $h$ is a continuous function. Then $h(X_1), h(X_2), ... $ converges in probability to $h(X)$

Among those convergence concepts, convergence in distribution is the weakest form.

**Definition (convergence in distribution)** A sequence of random variables $X_1, X_2, ...$ converges in distribution to a random variable $X$ if

$$\lim_{n \to \infty} F_{X_n}(x) = F_X(x)$$

at all points where $F_X(x)$ is continuous

## 5. Reference
- [1] Pishro-Nik, Hossein. "Introduction to probability, statistics, and random processes." (2016).
- [2] Casella, George, and Roger L. Berger. Statistical inference. Vol. 2. Pacific Grove, CA: Duxbury, 2002.
- [3] Axler, Sheldon. Measure, Integration & Real Analysis. Springer Nature, 2020.APA
- [4] Çınlar, Erhan. Probability and stochastics. Vol. 261. Springer Science & Business Media, 2011.

