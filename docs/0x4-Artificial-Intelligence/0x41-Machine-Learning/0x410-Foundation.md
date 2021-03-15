# 0x410 Foundation

- [1. Decision Theory](#1-decision-theory)
    - [1.1. Frequentist Decision Theory](#11-frequentist-decision-theory)
        - [1.1.1. Bayes Risk](#111-bayes-risk)
        - [1.1.2. Minimax Risk](#112-minimax-risk)
    - [1.2. Bayesian Decision Theory](#12-bayesian-decision-theory)
- [2. Information Theory](#2-information-theory)
- [4. Reference](#4-reference)


Machine Learning is to find a function

$$f: X \to Y$$

The task of machine learning can be roughly classified into following groups
- When $Y$ is a float scalar, it is called a regression task
- When $Y$ is an integer scalar, it is called the classification task
- When it is a more complex structure, it is called the structured learning.

## 1. Decision Theory

Mean square error loss is a special case of loss function, the study of the performance of estimators using loss function is a branch of decision theory

### 1.1. Frequentist Decision Theory

**Definition (risk function)** The quality of an estimator is quantified in its risk function wrt estimator $\delta(X)$

$$R(\theta, \delta) = E_{\theta} L(\theta, \delta(X))$$

!!! example "MSE is the risk with square error loss"
    For square error loss, 

    $$L(\theta, a) = (a - \theta)^2$$
    
    the risk function is mean square error (MSE) where 

    $$R(\theta, \delta) = E_{\theta}(\delta - \theta)^2 = \mathrm{Var}_\theta \delta(X) + (\mathrm{Bias} \delta(X))^2$$

For a fixed $\theta$, the risk function is the average loss that will be incurred if the estimator $\delta(x)$ is used. However, since the true $\theta$ is unknown, we would like to use an estimator that has a samll value $R(\theta, \delta)$ for all values of $\theta$

As the optimality will change based on different $\theta$, we have variosu solutions here

#### 1.1.1. Bayes Risk
**Definition (Bayes risk)** In Bayesian analysis wewould use the prior distribution $\pi(\theta)$ to compute an average risk, known as the *Bayes risk*

$$R_{B} (\delta) = \int_{\Theta} R(\theta, \delta) \pi(\theta) d\theta$$

The Bayes estimator or Bayes decision rule is one which minimizes the expected risk:

$$\delta_{B} = \argmin_{\delta} (R_B(\delta))$$

#### 1.1.2. Minimax Risk
An alternative approach is to use minimax risk

**Definition (minimax risk)** The maximum risk of an estimator is

$$R_{max}(\delta) = \max_{\theta} R(\theta, \delta)$$

A minimax rule is one which minimizes the maximum risk

$$\delta_{MM} = \argmin_{\delta} R_{max}(\delta)$$

### 1.2. Bayesian Decision Theory


## 2. Information Theory
Information Theory is concerned with representing daata in a compact fashion, the most important concepts are summarized here

**Definition (entropy)** The entropy of a random variable $X$ with distribution $p$ is

$$H(X) = \sum_{k=1}^K p(X=k) \log_2 p(X=k)$$

**Definition (relative entropy, KL divergence)** One way to measure the dissimilarity of two probability distribution $p, q$ is the Kullback-Leibler divergence (KL divergence) or relative entropy

$$KL(p||q) = \sum_k p_k \log\frac{p_k}{q_k} = -H(p) + H(p, q)$$

**Definition (cross entropy)** $H(p,q)$ is called cross entropy, it is to measure the average number of bits to encode data of distribution $p$ using codebook of distribution $q$, it is defined as

$$H(p, q) = -\sum_k p_k \log q_k$$


**Definition (conditional entropy)** The conditional entropy $H(Y|X)$ is defined as

$$H(Y|X) = \sum_x p(x) H(Y|X=x)$$

**Definition (mutual information)** Mutual information or MI is an approach to estimate how similar the joint distribution $p(X,Y)$ can be factored into $p(X)p(Y)$

$$I(X;Y) = KL(p(X,Y)||p(X)p(Y)) = \sum_x \sum_y p(x,y)\log \frac{p(x,y)}{p(x)p(y)}$$

Obviously, MI is zero iff two random variables are independent.

MI can be expressed using entropy as follows

$$I(X;Y) = H(X) - H(X|Y) = H(Y) - H(Y|X)$$

**Definition (pointwise mutual information)** A related concept is pointwise mutual information or PMI, this is about two events $x,y$

$$PMI(x,y) = \log \frac{p(x,y)}{p(x)p(y)}$$


## 4. Reference
[1] Murphy, Kevin P. Machine learning: a probabilistic perspective. MIT press, 2012.