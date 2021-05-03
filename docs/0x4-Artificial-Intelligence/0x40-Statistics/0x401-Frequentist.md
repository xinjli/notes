# 0x401 Frequentist Inference

- [1. Sampling Theory](#1-sampling-theory)
    - [1.1. Sample Mean](#11-sample-mean)
    - [1.2. Sample Variance](#12-sample-variance)
    - [1.3. Sample Order](#13-sample-order)
- [2. Data Reduction Principles](#2-data-reduction-principles)
    - [2.1. The sufficiency principle](#21-the-sufficiency-principle)
        - [2.1.1. Minimal Sufficient statistics](#211-minimal-sufficient-statistics)
    - [2.2. The Likelihood Principle](#22-the-likelihood-principle)
- [3. Point Estimation](#3-point-estimation)
    - [3.1. Methods of Finding Estimators](#31-methods-of-finding-estimators)
        - [3.1.1. Method of Moments](#311-method-of-moments)
        - [3.1.2. Maximum Likelihood Estimators](#312-maximum-likelihood-estimators)
        - [3.1.3. Bayes Estimators](#313-bayes-estimators)
    - [3.2. Algorithms of Finding estimators](#32-algorithms-of-finding-estimators)
        - [3.2.1. Newton-Raphson](#321-newton-raphson)
        - [3.2.2. The EM algorithm](#322-the-em-algorithm)
    - [3.3. Methods of Evaluating Estimators](#33-methods-of-evaluating-estimators)
        - [3.3.1. Mean Squared Error](#331-mean-squared-error)
        - [3.3.2. Best Unbiased Estimator](#332-best-unbiased-estimator)
        - [3.3.3. Sufficiency and Unbiasedness](#333-sufficiency-and-unbiasedness)
- [4. Hypothesis Testing](#4-hypothesis-testing)
    - [4.1. Methods of Finding Tests](#41-methods-of-finding-tests)
        - [4.1.1. Likelihood Ratio Tests](#411-likelihood-ratio-tests)
    - [4.2. Methods of Evaluating Tests](#42-methods-of-evaluating-tests)
- [5. Interval Estimation](#5-interval-estimation)
- [6. Reference](#6-reference)

The basic problem of statistical inference is the inverse of probability: Given the outcomes, what can we say about the process that generated the data?

More formally, Statistical inference is the process of using data analysis to infer properties of an underlying distribution of probability.

- **Frequentist Inference**: the unknown quantity is assumed to be a fixed quantity

- **Bayesian Inference**: the unknown quantity is assumed to be a random variable, we have some initial guess about the distribution, and update the distribution after observing the data

## 1. Sampling Theory
Sample is a sequence of iid random variable, statistic is its function.

**Definition (random sample)** The collection of random variables $X_1, X_2, ... X_n$ is said to be a random sample of size $n$ if they are independent and identically distributed (i.i.d), i.e

- $X_1, ..., X_n$ are independent random variables
- They have same distribution

$$F_{X_1}(x) = ... = F_{X_n}(x)$$

$x_1, x_2, ..., x_n$ is said to their realizations. The joint pdf or pmf or $X_1, ..., X_n$ is given by

$$f(x_1, ..., x_n) = f(x_1) f(x_2) ... f(x_n) = \prod_{i=1}^n f(x_i)$$

This random sampling model is called sampling from an infinite population. Its assumption is that, after observing $X_1 = x_1$, the probability distribution $X_2$ is unaffected.

In the case of sampling from a finite population, there are two cases

- *sampling with replacement*: this meets the previous definition
- *sampling without replacement*: the random variables are no longer independent (but still identically distributed). When population is large enough, it can still be approximated with the previous condition.


**Definition (statistic, sampling distribution)** The random variable $Y$ defined over a random sample $X_1, ..., X_n$ and a real-valued function $T$ is called a ***statistic***,

$$Y=T(X_1, ..., X_n)$$

The statistics, however, cannot depend on any parameter $\theta$!!

The distribution of a statistic $Y$ is called the ***sampling distribution*** of $Y$. Once the sample is drawn, the $t$ is called the realization of $T$, where

$$t = T(x_1, x_2, ..., x_n)$$

!!! info "statistics is random variable"

    I always get confused, but be careful that statistic is a random variable, not a scalar (because it is a transformations (function) of random variables)

    - variance is a scalar
    - sample variance is a random variable



**Lemma (expectation of random sample)** Let $X_1, ..., X_n$ be a random sample and $g(x)$ be a function such that $Eg(X)$ and $Var(g(X))$ exists then

$$E(\sum_{i=1}^n g(X_i)) = n E(g(X_1)) $$

$$\mathrm{Var}(\sum_{i=1}^{n} g(X_i)) = n (\mathrm{Var}(g(X_1)))$$

Note: the second one is proved using zero covariance between iid variables

**Definition (statistical model)** A statistical model is a set of distributions. 

**Definition (parametric, non parametric)** A parametric model is a set of statistical models that can be parameterized by a finite number of parameters (e.g: normal distribution). A nonparametric model is a set that cannot be.


### 1.1. Sample Mean
**Definition (sample mean)** The sample mean is the statistic defined by

$$\bar{X} = \frac{X_1 + ... + X_n}{n}$$

**Lemma (mean, variance of sample mean)** Let $X_1, ..., X_n$ be a random sample with mean $\mu$ and variance $\sigma^2 < \infty $

$$E\bar{X} = \mu$$

$$\mathrm{Var}(\bar{X}) = \frac{\sigma^2}{n}$$

Therefore, $\bar{X}$ is an *unbiased estimator* of $\mu$.


!!! example "anti-pattern in Cauchy distribution"

    Unlike the variance of sample mean is reduced by the sample size. It is important to note that the dispersion of the sample mean $\bar{X}$ of Cauchy distribution $Cauchy(\mu, \sigma)$, which is measured by $\sigma$ is invariant of the sample size. Cauchy distribution does not have mean or variance.

**Lemma (pdf of sample mean)** By applying transformation, we can obtain

$$f_{\bar{X}} = nf_X(nx)$$

**Lemma (mgf of sample mean)** Let $X_1, ..., X_n$ be a random sample from a population with mgf $M_X(t)$. Then the mgf of the sample mean is

$$M_{\bar{X}}(t) = [ M_X(t/n) ]^n$$

**Lemma (sample mean of normal distribution)** Let $X_1, ..., X_n$ be a random variable from $n(\mu, \sigma^2)$ distribution, then

$$\bar{X} \sim n(\mu, \sigma^2/n)$$

Or 

$$\frac{\bar{X}-\mu}{\sigma/\sqrt{n}} = n(0, 1)$$

**Theorem (Weak Law of Large Number)** Let $X_1, ..., X_n$ be iid random variables with mean and variance, then for every $\epsilon$

$$\lim_{n \to \infty} P(|\bar{X}_n - \mu| < \epsilon) = 1$$

**Theorem (central limit theorem)** Let $X_1, ..., X_n$ be iid random variables with mean and variance, let $G_n(x)$ denote the cdf of $\sqrt{n}(\bar{X}_n - \mu)/\sigma$, then

$$\lim_{n \to \infty} G_n(x) = \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}} e^{-y^2/2} dy$$

that is, $\sqrt{n}(\bar{X}_n - \mu)/\sigma$ has a limiting standard normal distribution.

### 1.2. Sample Variance

**Definition (sample variance)** The sample variance is the statistic defined by

$$S^2 = \frac{1}{n-1} \sum_{i=1}^{n} (X_i - \bar{X})^2$$

A useful transformation to compute $(n-1)S^2$ is

$$\sum_i (X_i - \bar{X})^2 = \sum_i X_i^2 - n\bar{X}^2$$

Notice the analogy between this and variance computing.

$$Var(X) = EX^2 - (EX)^2$$

**Lemma (mean, variance of sample variance)** 
$$ES^2 = \sigma^2$$

$$\text{Var}(S^2) = \frac{1}{n} (\theta_4 - \frac{n-3}{n-1}\theta^2_2)$$

where $\theta_i$ is the i-th central moment. The first part is easy, the second part is crazy, see solution of Casella Berger exercise 5.8.

Therefore, $S^2$ is an *unbiased estimator* of $\sigma^2$

In the case of normal distribution, the sample mean and variance have several good properties as follows:

**Proposition (sample variance of normal distribution)**
Let $X_1, ..., X_n$ be a random sample from a $n(\mu, \sigma^2)$ distribution. Then

$$\frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$$

Taking variance on both side, we obtain

$$Var(S^2) = \frac{2\sigma^4}{n-1}$$

**Lemma (independence of $\bar{X}, S^2$ in normal distribution)** $\bar{X}, S^2$ are independent 
  
Note that in general, $\bar{X}, S^2$ are not always independent, it requires the 3rd central moment to be 0 to be independent.

### 1.3. Sample Order
**Definition (order statistics)** The order statistics of a random sample $X_1, ..., X_n$ are sample values placed in ascending order. They are denoted by $X_{(1)}, ..., X_{(n)}$.

**Definition (sample range)** the sample range is the distance between the smallest and largest observtions.

$$R=X_{(n)}-X_{(1)}$$

**Definition (sample median)** the sample median $M$ is defined as

$$M = \begin{cases} X_{((n+1)/2)} & \text{ if n is odd} \\ (X_{(n/2)} + X_{(n/2+1)}) /2 & \text{ if n is even} \\ \end{cases}$$

One advantage of sample median over the sample mean is that it is less affected by extreme observations.

Other related statistics are lower quartile and upper quartile.

**Proposition (discrete order statistics)** Let $X_1, ..., X_n$ be a random sample from a discrete distribution with pmf $f_X(x_i) = p_i$ where $x_1 < x_2 < ...$ are possible values of $X$ in ascending order. Let $P_i = \sum_{k=1}^i p_k$, then cdf of order statistics is

$$P(X_{(j)} \leq x_i) = \sum_{k=j}^n \binom{n}{k} P_i^k (1-P_i)^{(n-k)}$$

and the pmf is

$$P(X_{(j)} = x_i) = \sum_{k=j}^n \binom{n}{k} [ P_i^k (1-P_i)^{(n-k)} - P_{i-1}^k (1-P_{i-1})^{(n-k)}]$$

**Proposition (continuous order statistics)** Consider the continuous population with cdf $F_X(x)$ and pdf $f_X(x)$, then the cdf is

$$F_{X_{(j)}} (x) = \sum_{k=j}^n \binom{n}{k} [F_X(x)]^k [1-F_X(x)]^{n-k}$$

By differentiating this one, we can get

$$f_{X_{(j)}}(x) = \frac{n!}{(j-1)!(n-j)!} f_X(x) [F_X(x)]^{j-1} [1-F_X(x)]^{n-j}$$

**Proposition (joint pdf)** The joint pdf of all the order statistics is given by

$$f_{X_{(1)},..., X_{(n)}}(x_1, ..., x_n) = n! \prod_i f_X(x_i)$$

if $x_1 < ... < x_n$, otherwise 0.

## 2. Data Reduction Principles
Data reduction in terms of a particular statistic $T$ can be thought of as a partition of the sample space into $A_t = \{ x | T(x)=t \}$. The partition should not discard important information about the unknown parameter $\theta$. Instead of reporting $x$, we only report its partition $T(x)$ (whose size is much smaller than $x$)

**Definition (experiment)** Formally an experiment $E$ is defined to be

$$E = (X, \theta, \{ f(x|\theta) \})$$

**Definition (evidence)** An experimenter, knowing what experiment $E$ is performed and having observed a sample $x$, can make some inference or draw some conclusion about $\theta$, which denoted by

$$Ev(E, x)$$

which stands for the evidence about $\theta$ arising from $E, x$

### 2.1. The sufficiency principle
The sufficiency principle says the sufficient statistics summarizes all the information about $\theta$ in the sample. (You can only keep $T(x)$ and discard $x$ to save your memory)

**Principle (sufficiency)** Consider an experiment $E=(X, \theta, f(x|\theta))$ and suppose $T(X)$ is a sufficient statistics for $\theta$.

$$T(x) = T(y) \implies Ev(E,x) = Ev(E,y)$$

Intuitively, this means: If $\mathbf{x}, \mathbf{y}$ are two sample points such that $T(\mathbf{x}) = T(\mathbf{y})$, then the inference about $\theta$ should be the same whether $\mathbf{X}=\mathbf{x}$ or $\mathbf{X}=\mathbf{y}$ is observed


The sufficient statistic is defined as follows

**Definition  (sufficient statistic)** A statistic $T(\mathbf{X})$ is a sufficient statistic for $\theta$ if the conditional distribution of the sample $\mathbf{X}$ given the value of $T(\mathbf{X})$ does not depend on $\theta$

**Criterion (condition of sufficient statistics)** If the following ratio, is constant as a function of $\theta$, then $T(\mathbf{X})$ is a sufficient statistic for $\theta$

$$\frac{p(\mathbf{x}|\theta)}{q(T(\mathbf{x})|\theta)}$$ 

Sufficient statistic can be interpreted with the concept of sufficient partition

!!! example "Bernoulli sufficient statistic"

    Let $X_1, ..., X_n$ be Bernoulli random variables with parameter $\theta$. Then one of the sufficient statistic for $\theta$ is

    $$T(X) = X_1 + ... + X_n$$

    This can be proved by consider $p(x|\theta)$ and $q(T(x)\theta)$
    $$p(x|theta) = \pi_i \theta^x_i (1-\theta)^{1-x_i} = \theta^t (1-\theta)^{n-t}$$

    $$q(t|\theta) = \binom{n}{t} \theta^{t} (1-\theta)^{n-t}$$

    Their ratio is constant with respect to $\theta$

**Criterion (Fisher-Neyman factorization)** Let $f(\mathbf{x}|\theta)$ denote the joint pdf of a sample $\mathbf{X}$. A statistic $T(\mathbf{X})$ is a sufficient statistic for $\theta$ iff

$$f(\mathbf{x}|\theta) = g(T(\mathbf{x}) | \theta) h(\mathbf{x})$$

Note that $g(T(x)|\theta)$ is not necessarily a distribution.

!!! example "sufficient statistics of exponential distribution"

    Let $X_1,..., X_n$ from a exponential family

    $$f(x|\theta)= h(x)c(\theta) \exp (\sum_{w_i}(\theta) t_i(x))$$

    then the following is a sufficient statistic for $\theta$

    $$T(X) = ( \sum_j t_1(X_j), ..., \sum_j t_k(X_j))$$

It turns out that outside of the exponential family of distributions, it is rare to have a sufficient statistic of smaller dimension than the size of the sample, so in many cases the order statistics are the best that we can do.

**Definition (sufficient partition)** A partition $B_1, ..., B_k$ is called sufficient partition if $f(x|X \in B)$ does not depend on $\theta$.

A statistic $T$ induces a partition. $T$ is sufficient iff its partition is sufficient. If we get finer partition from one sufficient partition, it is also sufficient partition (statistics). 

#### 2.1.1. Minimal Sufficient statistics
There are more than one sufficient statistics, the sufficient statistics which achieve the most data reduction is the minimal sufficient statistic. 

Their partition is corresponding to the most coarse sufficient partition. A more coarse partition will remove the sufficiency (it will depend on $\theta$)

**Definition (minimal sufficient statistics)** A sufficient statistics $T(\mathbf{X})$ is called a minimal sufficient statistics if, for any other sufficient statistics $T'(\mathbf{X})$, $T(x)$ is a function of $T'(x)$

**Criterion (condition of minimality)** $T(\mathbf{X})$ is a minimal sufficient statistics for $\theta$ when 

the ratio $f(x|\theta)=f(y|\theta)$ is constant as a function of $\theta$ iff $T(x)=T(y)$

**Definition (ancillary statistics)** A statistic $S(X)$ whose distribution does not depend on the parameter $\theta$ is called an *ancillary statistic*

**Definition (complete statistic)** Let $f(t|\theta)$ be a family of pdfs or pmfs for a statistic $T(X)$, the family of probability distributions is called complete if 

$$\forall(\theta)E_{\theta}(g(T)) = 0 \implies \forall(\theta) P_{\theta}(g(T)=0) = 1$$

**Theorem (Basu)** If $T(X)$ is a complete and minimal sufficient statistic, then $T(X)$ is independent of every ancillary statistic.

### 2.2. The Likelihood Principle
The likelihood principle says that the likelihood function summarizes all information about $\theta$ from the sample. (You can only keep $L(\theta|x)$ and discard $x$ to save your memory)

**Principle (likelihood)** Suppose we have two experiments $E_1 = (X_1, \theta, \{ f_1(x_1|\theta) \}), E_2= (X_2, \theta, \{ f_2(x_2|\theta) \})$ where $\theta$ is same in both experiments. Suppose $x^*_1, x^*_2$ are two sample points from $E_1, E_2$ such that their likelihoods function are propostional

$$L(\theta | x^*_2) = CL(\theta | x^*_1)$$
then

$$Ev(E_1, x^*_1) = Ev(E_2, x^*_2))$$

**Definition (likelihood function)** Let $f(x|\theta)$ denoted the joint pdf or pmf of the sample $X$, given that $X=x$ is observed, the function of $\theta$ defined as follows is called the likelihood function

$$L(\theta|x) = f(x|\theta)$$

The likelihood principles can be derived from the sufficiency principles and conditionality principles, the latter says that if one of two experiments is randomly chosen and done, the information about $\theta$ depends only on the experiment performed.


## 3. Point Estimation
Point estimation consists of two part: how to find a point estimator, how to evaluate them

**Definition (point estimator)** A point estimator is any function $W(X_1, X_2, ..., X_n)$ of a sample; that is, any statistic is a point estimator.

An *estimator* is a function of the sample, an *estimate* is the realized value of estimator. There might be natural candidates for point estimators, but not always follow our intuitions

### 3.1. Methods of Finding Estimators
#### 3.1.1. Method of Moments

This method is perhaps the oldest method of finding point estimators, it is a good start place when other methods prove intractable. Also it can be applied to obtain approximations to the distributions of statistics. (Satterthwaite approximation)

**Definition (method of moments estimator)** Equating the sample moments to the corresponding population moments and solve the resulting system.

$$\mu_1(\theta_1, ..., \theta_k) = \frac{1}{n} \sum_i X_i$$
$$\mu_2(\theta_1, ..., \theta_k) = \frac{1}{n} \sum_i X^2_i$$
$$...$$
$$\mu_k(\theta_1, ..., \theta_k) = \frac{1}{n} \sum_i X^k_i$$

The left side is a function of $\theta_1, ..., \theta_k$ and the right side and moments statistics. Solving this systems we obtain

$$\theta_i = f(\frac{1}{n}\sum_i X_1, \frac{1}{n}\sum_i X^2_1, ..., \frac{1}{n}\sum_i X^k_1)$$

which is the estimator for $\theta_i$


#### 3.1.2. Maximum Likelihood Estimators
**Definition (maximum likelihood estimator)** Maximum likelihood estimator $\hat{\theta}(\mathbf{x})$ is the parameter $\theta$ to maximize $L(\theta | \mathbf{x})$

$$L(\theta | \mathbf{x}) = \prod_i f(x_i | \theta_1, ..., \theta_k)$$


**Theorem (invariance property of MLE)** If $\hat{theta}$ is the MLE of $\theta$, then for any function $\tau(\theta)$, the MLE of $\tau(\theta)$ is $\tau(\hat\theta)$

**Proposition (properties of MLE)**
- $\hat{\theta}_{MLE}$ is asymptotically consistent
- $\hat{\theta}_{MLE}$ is asymptotically unbiased
- $\hat{\theta}_{MLE}$ is approximately a normal random variable
  
**Properties (Drawbacks of MLE)** The drawbacks of MLE are
- finding and verifying the global maximum is difficult 
- numerical sensitivity (easy to overfitting, high variance).

How to solve these two problems?
- To solve the first one, we can apply the numerical approach. MLE might be maximized numerically if likelihood can be written down.
 
- To solve the 2nd, The Bayesian approach might be helpful to solve this issue or try to scale up the dataset...

For example, in the Markov language model, MLE language model have the zero count issue, therefore smoothing is necessary. This is a Bayesian approach: Laplace smoothing can be interpreted as a MAP with a uniform prior.



#### 3.1.3. Bayes Estimators
In the classical approach, the parameter $\theta$ is thought to be an unknown, but fixed quantity. In the Bayesian approach, $\theta$ is considered to be a random variable from a probability distribution $\pi(\theta)$(prior distribution), which is subjective distribution by the experimenter's belief.

The distribution is updated into posterior distribution $\pi(\theta|x)$ based on sample observed

$$\pi(\theta|x) =\frac{f(x|\theta) \pi(\theta)}{\int f(x|\theta)\pi(\theta) d\theta}$$

Note that there are lots of ways to get Bayes estimators. For example,

One way to compute Bayes point estimator is to take its mean

$$\hat{\theta} = E[\pi(\theta|x)]$$

**Definition (MAP)** Another is to get the mode, which is the maximum a posteriori probability (MAP) estimate
$$\hat{\theta} = \mathrm{argmax}_\theta \pi(\theta|x)$$

###  3.2. Algorithms of Finding estimators
In some cases, we can find MLE analytically, but more often we need to find it by numerical methods

#### 3.2.1. Newton-Raphson
#### 3.2.2. The EM algorithm
EM is an algorithm which is guaranteed to converge to the MLE or MAP

### 3.3. Methods of Evaluating Estimators
The general topic of evaluating statistical procedures is the branch known as decision theory

#### 3.3.1. Mean Squared Error
**Definition (mean squared error)** The mean squared error (MSE) of an estimator $W$ of a parameter $\theta$ is the function of $\theta$ defined by $E_{\theta}(W-\theta)^2$

$$E_{\theta} (W(x1, ..., x_n) - \theta)^2 = \int ... \int (W(x_1, ..., x_n) - \theta)^2 f(x_1|\theta) ... f(x_n|\theta) dx_1 ... dx_n$$

**Lemma (bias-variance decomposition)** The mean square error have a bias-variance decomposition as follows:

$$E_{\theta} (W-\theta)^2 = (E_\theta W  - \theta)^2 + Var_\theta(W)$$

In ML terms (Andrew Ng' lecture)

- Bias is an error from the algorithm/estimator itself, it is corresponding to underfitting (high error in training set)
- Variance is an error from sensitivity to small fluctuations in the training set, which causes the bad performance in dev set. It is corresponding to overfitting (high error in test set).

**Definition (bias)** The bias of a point estimator $W$ of a parameter $\theta$ is the difference between the expected value of $W$ and $\theta$; that is 

$$Bias_{\theta}W = E_{\theta}W - \theta$$

**Definition (unbiasedness)** An estimator whose bias is identically equal to 0 is called unbiased when for all $\theta$

$$E_{\theta} W = \theta$$

!!! example "MSE for normal distribution"

    Let $X_1, ..., X_n$ be $n(\mu, \sigma^2)$ distribtuion, the statistics $\bar{X}, S^2$ are both unbiased estimator, therefore their MSE are

    $$E(\bar{X} - \mu)^2 = Var(\bar{X}) = \frac{\sigma^2}{n} \\
    E(S^2 - \sigma)^2 = Var(S^2) = \frac{2\sigma^4}{n-1}$$


#### 3.3.2. Best Unbiased Estimator
There is no one "best MSE" estimator as the class of all estimators is too large (e.g: the estimator $\hat{\theta}=17$ cannot be beaten in MSE at $\theta=17$, but is terrible otherwise).

One way to make it trackable is to limit the class of estimators to consider the unbiased estimators, under this assumption, we can only compare the variance to minimize MSE 

**Definition (unbiased best estimator)** An esitmator $W^*$ is a best unbiased estimator of $\tau(\theta)$ if it satisfies $E_\theta W^* = \tau(\theta)$ for all $\theta$. For any other estimator $W$ with $E_\theta(W) = \tau(\theta)$ we have for all $\theta$ 

$$Var_{\theta} W^* \leq Var_{\theta} W$$

$W^*$ is also called a *uniform minimum variance unbiased estimator*.

Even within the class of unbiased estimators, candidates of best estimators can be infinitely many, so it might be hard to verify that an estimator is the best one. The following inequality can guarantee the found estimator is the best one

**Theorem (Cramer-Rao Lower bound)** Let $X_1, ..., X_n$ be a sample of pdf $f(x|theta)$, and let $W(X)=W(X_1, ..., X_n)$ be any estimator satisfying

$$ \frac{d}{d\theta} E_\theta W(X) = \int \frac{\partial}{\partial \theta} [W(x)f(x|\theta)] dx$$

and

$$Var_\theta W(X) < \infty$$

then

$$Var_\theta (W(X)) \geq \frac{(\frac{d}{d\theta} E_\theta W(X))^2}{E_\theta((\frac{\partial}{\partial \theta} log(f(X|\theta)))^2)}$$

Note the formula might be cleaned a bit more, if $W(X)$ is the unbiased estimator, then obviously the nominator is

$$\frac{d}{d\theta} E_\theta W(X) = 1$$

Under the iid assumption of sample, the denominator can be 

$$E_\theta((\frac{\partial}{\partial \theta} log(f(X|\theta)))^2) = n E_\theta ((\frac{\partial}{\partial \theta} \log f(x|\theta))^2)$$

A shortcoming of Cramer-Rao is its bound may be strictly smaller than the variance of any unbiased estimator.

**Definition (Fisher information)** The following quantity is called the Fisher information

$$E_\theta((\frac{\partial}{\partial \theta} log(f(X|\theta))^2)$$

The bigger Fisher information indicates more information about $\theta$, therefore small variance of the best unbiased estimator

For exponential family, this can be simplified into

$$E_\theta((\frac{\partial}{\partial \theta} log(f(X|\theta))^2) = - E_\theta(\frac{\partial^2}{\partial \theta^2}\log f(X|\theta))$$

#### 3.3.3. Sufficiency and Unbiasedness

**Theorem (Rao-Blackwell)** Let $W$ be an unbiased estimator for $\tau(\theta)$, and $T$ be a sufficient statistic for $\theta$. Then the following $\phi(T)$ is a uniformly better unbiased estimator of $\tau(\theta)$

$$\phi(T)=E(W|T)$$

## 4. Hypothesis Testing
Like point estimation, hypothesis testing is another statistical inference method.

**Definition (hypothesis)** A hypothesis is a statement about a population parameter. The complementary hypotheses are called **null hypothesis** and **alternative hypothesis**, denoted by $H_0, H_1$ respectively. The general form of hypothesis about $\theta$ is that $H_0 = \Theta_0$ and $H_1 = \Theta_0^c$

If the hypothesis specify only one possible distribution (the parameter space has only one element, e.g; $\Theta = \{  0.5 \}$), then it is called a **simple hypothesis**, otherwise it is called **composite hypothesis**. It is often the case that the null hypothesis is chosen to be a simple hypothesis.

**Definition (hypothesis test)** A hypothesis test is a rule that specifies

- For which sample value the decision is made to accept $H_0$
- For which sample value $H_0$ is rejected and $H_1$ is accepted as true

Be careful that to say accept/reject a hypothesis is not equivalent to saying that the hypothesis is true/false.

!!! info "procedure of hypothesis test"
    Typically, a hypothesis test is specified in terms of a test statistic. In particular, we can construct test by

    - choose a test statistics $T(X_1, ..., X_n)$
    - choose a critical value $t$ and define the rejection region $R=\{ (x_1,...,x_n) | T(x_1,...,x_n) \geq t \}$
    - if $T \geq t$ or equivalently $(X_1, ..., X_n) \in R$, we reject $H_0$ otherwise we retain $H_0$

### 4.1. Methods of Finding Tests
#### 4.1.1. Likelihood Ratio Tests
**Definition (likelihood ratio test statistic, LRT)** The likelihood ratio test statistic for testing $H_0 : \theta \in \Theta_0$ versus $H_1: \theta \in \Theta_0^c$ is

$$\lambda(x) = \frac{\sup_{\Theta_0} L(\theta | \mathbf{x})}{\sup_{\Theta} L(\theta | \mathbf{x})}$$

A likelihood ratio test (LRT) is any test that has a rejection region of the form $\{ \mathbf{x} : \lambda(\mathbf{x}) \leq c \}$ where $0 \leq c \leq 1$

!!! example "normal LRT"

    Let $X_1, ..., X_n$ be a random sample from $n(\theta, 1)$ distribution, suppose the test $H_0: \theta = \theta_0, H_1: \theta \neq \theta_0$

    The LRT statistic is

    $$\lambda(x) = \frac{L(\theta_0 | x)}{L(\bar{x}|x)} = \exp( -n (\bar{x} - \theta_0)^2)$$

    The rejection region $\{ x: \lambda(x) \leq c \}$ is

    $$\{ |\bar{x} - \theta_0| \geq \sqrt{-2\log(c)/n} \}$$


Note that the rejection region can be simplified to an experssion involving a simpler sufficient statistic.

**Theorem (test based on sufficient statistics)** If $T(\mathbf{X})$ is a sufficient statistic for $\theta$ and $\lambda^{*}(t), \lambda(\mathbf{x})$ are the LRT statistics based on $T,\mathbf{X}$, then $\lambda^{*}(T(\mathbf{x}))=\lambda(\mathbf{x})$ for every $\mathbf{x}$ in the sample space

**Theorem (union-intersection)** The union-intersection method of test construction might be useful when the null hypothesis is conveniently experssed as an intersection.

$$H_0: \theta \in \bigcap_{\gamma \in \Gamma} \Theta_{\gamma}$$

Suppose the test for each problem is $H_{0\gamma}$ vs $H_{1\gamma}$, and the rejection region for the test is $\{ x: T_{\gamma}(x) \in R_{\gamma} \}$, the rejection region is their union

$$\bigcup_{\gamma \in \Gamma} \{ x: T_{\gamma}(x) \in R_{\gamma} \}$$

### 4.2. Methods of Evaluating Tests
**Definition (Type I, II error)** 

- Type I error is the false negative error (i.e.: $\theta \in \Theta_0$ but $H_0$ is rejected)
- Type II error is the false positive error (i.e: $\theta \in \Theta_1$ but $H_0$ is accepted)

In general, an attempt to decrease one type of error is accompanied by an increase in the other type of error, so a compromise has to be made. The only way to reduce both types of error is to increase the sample size.

**Definition (power function)** Suppose $R$ denotes the reject region for a test. Then the power function of this test is the function of $\theta$ defined by

$$\beta(\theta) = P_\theta (X \in R)$$

Ideally, we would like $\beta(\theta)=0$ when $\theta \in \Theta_0$ (minimize False Negative, Type I Error) and $\beta(\theta)=1$ when $\theta \in \Theta_0^c$ (minize False Positive, Type II Error)

Typically, the power function of a test will depend on the sample size $n$, therefore by considering the power function, the experimenter can choose $n$ to achieve some test goal.

!!! example "normal power function"

    Let $X_1, ..., X_n$ be a random sample from $n(\theta, \sigma^2)$ population with $\sigma^2$ known.

    We consider a LRT $H_0: \theta \leq theta_0$ VS $H_1: \theta > \theta_0$ is a test that the rejection region is

    $$R = \{ X_1, ..., X_n | \frac{\bar{X}-\theta_0}{\sigma/\sqrt{n}} > c \}$$

    Then, the power function of this test is

    $$\beta(\theta) = P_{\theta}(\frac{\bar{X}-\theta_0}{\sigma/\sqrt{n}} > c) = P(Z > c+\frac{\theta_0 - \theta}{\sigma/\sqrt{n}})$$

    where $Z$ is a standard normal random variable.


For a fixed sample size, it is impossible to make both errors arbitrarily small, so it is common to restrict consideration to tests that control the Type I Error at a specified level, and within that level, minimize Type II as much as possible. 

!!! info "point estimation and hypothesis testing"

    Notice the similarity between point estimation and hypothesis testing
    
    - in point estimation, we restrict estimators to a restricted class (unbiased estimator) and then minimize variance within that class
    - in hypothesis testing, we restrict test to a specfic level-$\alpha$ test and minimize the Type II error (find the most powerful test) within this class.

**Definition (size $\alpha$ test, alpha $\alpha$ test)** 

For $0 \leq \alpha \leq 1$, a test with power function $\beta(\theta)$ is called size $\alpha$ test if $sup_{\theta \in \Theta_0} \beta(\theta) = \alpha$. It is called level $\alpha$ test if $sup_{\theta \in \Theta_0} \beta(\theta) \leq \alpha$.

$\alpha$ is called the **level of significance**

The previous tests only yields test statistics and general form for rejection regions, but do not lead to one specific test. For example, LRT does not specify $c$. The restriction to size $\alpha$ may lead to the choice of $c$ out of the class of tests.

**Definition (unbiased test)** A test with power function $\beta(\theta)$ is called unbiased iff $\beta(\theta') \geq \beta(\theta'')$ for all $\theta' \in \Theta_0^c, \theta'' \in \Theta_0$

**Definition (uniformly most powerful)** Let $\mathcal{C}$ be a class of tests for testing $H_0: \theta \in \Theta_0$ versus $H_1: \theta \in \Theta_0^c$. A test in class $\mathcal{C}$, with power function $\beta(\theta)$ is a uniformly most powerful (UMP) class test if $\beta(\theta) \geq \beta'(\theta)$ for every $\theta \in \Theta_0^c$ and every $\beta'(\theta)$ that is a power function of a test in the class.

**Theorem (Neyman-Pearson)** Consider testing $H_0: \theta = \theta_0$ vs $H_1: \theta = \theta_1$, using a test with rejection region $R$ that satisfies

$$f(x | \theta_1) > k f(x|\theta_0) \implies x \in R$$

$$f(x | \theta_1) < k f(x|\theta_0) \implies x \in R^c$$

for some $k \geq 0$ and 

$$\alpha = P_{\theta_0}(X \in R)$$

- (Sufficiency) Any test that satisfies those conditions are UMP level $\alpha$ test

- (Necessity) If there exists a test satisfying those condition with $k > 0$, then every UMP level $\alpha$ test is a size $\alpha$ test.

**Theorem (Karlin-Rubin)** Consider testing $H_0: \theta \leq \theta_0$ vs $H_1: \theta > \theta_0$. Suppose that $T$ is a sufficient statistic for $\theta$ and the family of pdfs $\{ g(t|\theta): \theta \in \Theta \}$ of $T$ has an MLR (monontone likelihood ratio) property.  Then for any $t_0$, the test that rejects $H_0$ iff $T > t_0$ is a UMP level $\alpha$ test, where $\alpha = P_{\theta_0}(T > t_0)$


Instead of reporting "accept" or "reject", we can report a continuous value to indicate how close we are using p-value

Intuitively, p-value is the lowest significance level $\alpha$ that results in rejecting the null hypothesis.

**Definition (p-value)** A p-value $p(X)$ is a test statistics satisfying $0 \ leq p(x) \leq 1$ for every sample $x$, small values of $p(x)$ give evidence that $H_1$ is true. A p-value is valid iff for every $\theta \in \Theta_0, 0 \leq \alpha \leq 1$

$$P_{\theta}(p(X) \leq \alpha) \leq \alpha$$

The most common way to define a valid p-value is
**Theorem (valid p-value related to test)** Let $W(X)$ be a test statistic such that large values of $W$ give evidence that $H_1$ is true. For each sample point $x$, define

$$p(x) = \sup_{\theta \in \Theta_0} P_\theta (W(X) \geq W(x))$$

Then, $p(X)$ is a valid p-value

## 5. Interval Estimation

**Definition (interval estimate)** An interval estimate of a parameter $\theta$ is any pair of functions, $L(x_1, ..., x_n)$ and $U(x_1, ..., x_n)$ of a sample that satisfy $L(\mathbf{x}) \leq U(\mathbf{x})$ for all $\mathbf{x}$. The following random interval is called an interval estimator

$$[L(\mathbf{X}), U(\mathbf{X})]$$


**Definition (confidence level)** Let $X_1, X_2, X_3, ..., X_n$ be a random sample from a distribution with a parameter $\theta$. An interval estimator with confidence level $1-\alpha$ consists of two estimators $\hat{\Theta}_l(X_1, ..., X_n)$ and $\hat{\Theta}_h(X_1, ..., X_n)$ such that

$$P(\hat{\Theta}_l(X_1, ..., X_n) \leq \theta \land \hat{\Theta}_h(X_1, ..., X_n) \geq \theta) \geq 1 - \alpha$$

**Definition (pivotal quantity)** Let $(X_i)_{i=1}^{n}$ be a random sample from a distribution with parameter $\theta$ that is to be estimated. The random variable $Q$ is said to be a pivotal quantity iff:

It is a function of $(X_i)_{i=1}^{n}$ and the unknown parameter $\theta$, but it does not edepend on any other params
The probability distribtuion of $Q$ does not depend on $\theta$ or any other unknown params

## 6. Reference
[1] H. Pishro-Nik, "Introduction to probability, statistics, and random processes", available at https://www.probabilitycourse.com, Kappa Research LLC, 2014.

[2] Wasserman, Larry. All of statistics: a concise course in statistical inference. Springer Science & Business Media, 2013.

[3] Casella, George, and Roger L. Berger. Statistical inference. Vol. 2. Pacific Grove, CA: Duxbury, 2002.

[4] Hogg, Robert V., Joseph McKean, and Allen T. Craig. Introduction to mathematical statistics. Pearson Education, 2005.