# 0x421 Supervised Learning

- [1. Foundation](#1-foundation)
    - [1.1. Generative vs Discriminative](#11-generative-vs-discriminative)
        - [1.1.1. Generative Model](#111-generative-model)
        - [1.1.2. Discriminative Model](#112-discriminative-model)
    - [1.2. Parametric vs Nonparametric](#12-parametric-vs-nonparametric)
        - [1.2.1. Nonparametric Model](#121-nonparametric-model)
- [2. Simple Generative Model](#2-simple-generative-model)
    - [2.1. Simple Discrete Model](#21-simple-discrete-model)
        - [2.1.1. Multinoulli Naive Bayes Model](#211-multinoulli-naive-bayes-model)
    - [2.2. Simple Continuous Model](#22-simple-continuous-model)
        - [2.2.1. Gaussian Model](#221-gaussian-model)
        - [2.2.2. Gaussian Discriminant Analysis](#222-gaussian-discriminant-analysis)
            - [2.2.2.1. Quadratic Discriminant Analysis](#2221-quadratic-discriminant-analysis)
            - [2.2.2.2. Gaussian Naive Bayes](#2222-gaussian-naive-bayes)
            - [2.2.2.3. Linear Discriminative Analysis (LDA)](#2223-linear-discriminative-analysis-lda)
        - [2.2.3. GMM](#223-gmm)
- [3. Linear Regression Model](#3-linear-regression-model)
    - [3.1. Frequentist Linear Regression](#31-frequentist-linear-regression)
        - [3.1.1. MLE](#311-mle)
        - [3.1.2. Ridge Regression](#312-ridge-regression)
        - [3.1.3. Lasso](#313-lasso)
    - [3.2. Bayesian Linear Regression](#32-bayesian-linear-regression)
- [4. Linear Classification Model](#4-linear-classification-model)
    - [4.1. Discriminant Functions](#41-discriminant-functions)
        - [4.1.1. Fisher's Linear Discriminant](#411-fishers-linear-discriminant)
        - [4.1.2. The perceptron algorithm](#412-the-perceptron-algorithm)
    - [4.2. Generative Model](#42-generative-model)
        - [4.2.1. Naive Bayes](#421-naive-bayes)
        - [4.2.2. Linear Discrimative Analysis](#422-linear-discrimative-analysis)
    - [4.3. Discriminative Model](#43-discriminative-model)
        - [4.3.1. Logistic Regression](#431-logistic-regression)
            - [4.3.1.1. Max Entropy](#4311-max-entropy)
            - [4.3.1.2. Logistic Regression vs Naive Bayes](#4312-logistic-regression-vs-naive-bayes)
- [5. Sparse Kernel Models](#5-sparse-kernel-models)
    - [5.1. Kernel Methods](#51-kernel-methods)
    - [5.2. Maximum Margin Classifier (SVM)](#52-maximum-margin-classifier-svm)
- [6. Tree Model](#6-tree-model)
    - [6.1. CART (Classification and Regression Tree)](#61-cart-classification-and-regression-tree)
        - [6.1.1. ID3](#611-id3)
        - [6.1.2. C4.5, C5](#612-c45-c5)
    - [6.2. Ensemble](#62-ensemble)
        - [6.2.1. Boosted](#621-boosted)
        - [6.2.2. Bootstrap Aggregation (Bagging)](#622-bootstrap-aggregation-bagging)
- [7. Sequential Model](#7-sequential-model)
    - [7.1. Markov Model](#71-markov-model)
- [8. Reference](#8-reference)

## 1. Foundation

### 1.1. Generative vs Discriminative
The ML probabilistic model can be largely grouped into two models: generative model and discriminative model. The former models the joint distribution $p(x,y)$ and the latter models the posterior distribution $p(y|x)$

Andrew Ng's famous [paper](https://papers.nips.cc/paper/2001/file/7b7a53e239400a13bd6be6c91c4f6c4e-Paper.pdf) suggests the following points when comparing generative models

- generative model has a higher asymptotic error than discrminative model
- generative model approach this asymptotic error much faster, with $O(log(N))$ samples vs $O(N)$ samples.


#### 1.1.1. Generative Model
**Model (Generative Model)** Generative Model is to model the joint distribution $P(\textbf{x}, \textbf{y})$. 

This typically can be broken into modelling of conditional distribution and probability distribution:

- models a class conditional densities $P( \textbf{x} | y=y_k)$
- models a class prior $P(y=y_k)$

With the joint distribution, the prediction task is easily solve with posterior distribution.
- compute posterior $P(y=y_k | \textbf{x})$ with Bayes' theorem
  
Generative model tends to be better when training data are limited, but the bound of the asymptotic error is reached more quickly by a generative model than a discriminative model. Additionally, it performs worse when the density assumption give a poort approximation to the true distribution.


#### 1.1.2. Discriminative Model
**Definition (Discriminative Model)**  The approach of a discriminative model is to model posterior distribution directly $P(\textbf{y} | \textbf{x})$ directly. 

For example, in the classification task, it is to model  $P(y=y_k | \textbf{x})$ directly 

Parameters are typically estimated with MLE. for example, by iterative reweighted least squares (IRLS)

Discriminative model tends to achieve better results with asymptotic classification error (when training data are large enough)

Models that do not have probabilistic interpretation but can learn decision boundary are called **discriminant function**, these can also be classified as the (nonprobabilistic model) discriminative model. For example, SVM.

### 1.2. Parametric vs Nonparametric

#### 1.2.1. Nonparametric Model

Pros:

- simple, explainable
- can be extremely flexible

Cons:

- retrieval can be difficult or slow
- too flexiable (high variance)


## 2. Simple Generative Model
Probably the most simple model for supervised learning is to just fit a single parametric distribution to the data, this is much simpler than linear models and nonlinear models.

For a single class, we simply model $p(x)$ with a simple parameteric distribution, for multiple class, we model it with

$$p(x, y; \theta) = p(y; \theta)p(x|y; \theta)$$

where $y$ is a class, and $x$ might be discrete or continuous.

These generative models can be used, for example, classification tasks by modeling generative distribution for each class.

### 2.1. Simple Discrete Model
Fit a parametric discrete model

#### 2.1.1. Multinoulli Naive Bayes Model
The motivation of using Naive Bayes is to reduce the complexity. Consider the model has $n$ features, each feature is a binary feature. Without any constraints, we would need to model

$$p(\mathbf{x}=\mathbf{x}_i | y=y_j; \theta_{ij})$$

for every $i,j$ and this results in around $O(2^{n+1})$ parameters to estimate, which is usually too expensive.

With naive Bayes assumptions, we can reduce this complexity significantly. It writes the class conditional density of one-dimensional density

$$p(x | y=y_k; \theta) = p((x_1, x_2, ..., x_n) | y = y_k; \theta) = \prod_i p(x_i | y=y_k; \theta_{i})$$

The parameters of NB model is small $O(CD)$ where $C$ is the number of class, $D$ is the number of feature, so relatively immune to overfitting.

The joint distribution $p(x, y)$ is then

$$p(x,y) = p(x | y)p(y) = p(y) \prod_i p(x_i | y)$$

And the posterior is

$$P(y=y_k | x) = \frac{p(y=y_k)\prod_i p(x_i | y=y_k)}{\sum_j p(y=y_j)\prod_i p(x_i | y=y_j)}$$

In this binary classification task, the decision boundary is $p(y=1|x) = p(y=0|x) \implies \log{\frac{p(y=1|x)}{p(y=1|x)} = 0}$

This simplifies to

$$\sum_{i}\log\frac{p(x_i|y=1)}{p(x_i|y=0)} + \log\frac{p(y=1)}{p(y=0)}$$



### 2.2. Simple Continuous Model
Fit a parametric continous model

#### 2.2.1. Gaussian Model

#### 2.2.2. Gaussian Discriminant Analysis
This looks to be a bad naming, it is actually a generative classifier.

It fits the Gaussian distribution for each class conditional distribution

$$p(x | y=c; \theta) = N(x | \mu_c, \Sigma_c)$$

##### 2.2.2.1. Quadratic Discriminant Analysis 
The most general form is to assume Gaussian distribution without any contraints on $\mu_c, \Sigma_c$

$$p(y=c | x; \theta) = \frac{\pi_i N(x|\mu_c, \Sigma_c)}{\sum_{c'} \pi_i N(x|\mu_{c'}, \Sigma_{c'})}$$

This will produce quadratic decision boundary (as its name indicates).

Gaussian Naive Bayes and Linear Discrimnative Analysis are two special forms of QDA.

##### 2.2.2.2. Gaussian Naive Bayes
Gaussian Naive Bayes assumes conditional independence, therefore the off-diagnoal entry of $\Sigma_c$ will be zero, therefore $\Sigma_c$ is contrained to be diagonal matrix.

Note that this still can produce quadratic decision boundary. It will produce linear boundary when variance are tied. 

##### 2.2.2.3. Linear Discriminative Analysis (LDA)
LDA are using the same covariance matrix.

$$\Sigma_c = \Sigma$$

This produces the linear decision boundary.

#### 2.2.3. GMM

## 3. Linear Regression Model
Linear regression is a probablistic discrminative model. Its conditiona probability is expressed by

$$p(y|x; \theta) = \mathcal{N}(w^Tx, \sigma^2)$$

### 3.1. Frequentist Linear Regression
#### 3.1.1. MLE
The target variable $t$ can be modeled as follows:

$$p(t|x, w, \beta) = \mathcal{N}(t|y(x, w), \beta^{-1})$$

The log likelihood function wrt $w$ can be written as

$$\mathcal{l}(w) = \sum_i \log \mathcal{N}(t_i | w^T x_i, \beta^{-1})$$

The MLE is to minimize the following formula

$$\frac{1}{2} \sum_i (t_i - w^T x_i)^2$$

In the matrix form, this is equivalent to the following convex function (this is convex because the twice derivative $w^Tw$ is positive semidefinite)

$$\frac{1}{2}(xw - t)^T (xw - t) = \frac{1}{2}w^T x^Tx w - w^Tx^Tt$$

To minimize this convex function, take the derivative to 0 gives the following solution

$$(x^Tx) w = x^T t$$

which is known as the normal equation.

#### 3.1.2. Ridge Regression

#### 3.1.3. Lasso

### 3.2. Bayesian Linear Regression
In a full Bayesian treatment, the parameter $w$ has a distribution, the conjugate prior of the likelihood can be given as follows (if variance is known)

$$p(w) = \mathcal{N}(m_0, S_0)$$

## 4. Linear Classification Model
**Definition (classification task)** The goal of classification is to take an input vector $\textbf{x}$ and assigned it to one of $K$ discrete classes $\mathcal{C_k}$

**Definition (decision region, decision boundary)** The input space is divided into *decision regions* whose boundaries are called *decision boundaries*

### 4.1. Discriminant Functions
In the case of two classes, we assign to $C_1$ if $y \geq 0$, otherwise $C_0$

$$y(\textbf{x}) = \textbf{w}^T x + w_0$$

the decision boundary is $y = 0$, which is a hyperplane

For any point $x$, the signed distance to the hyperplane is

$$r = \frac{y(x)}{||w||}$$

When $x$ is at the origin, it reduced to $r = -w_0/||w||$

In the case of multiclasses, we create a single $K$-class discriminant comprising $K$ linear functions of the form

$$y_k(\mathbf{x}) = \mathbf{w}_k^T \mathbf{x} + w_{k0}$$

where we assgin a point $\mathbf{x}$ to $\mathcal{C}_k$ if $(\forall j \neq k) y_k(\mathbf{x}) > y_j(\mathbf{x})$

The decision regions are connected and convex

#### 4.1.1. Fisher's Linear Discriminant
#### 4.1.2. The perceptron algorithm
Proposed by Rosenblatt [2]. Minsky's work analyzes perceptron [3]. 

The perceptron learns a threshold function to map its input $x$ to an output $f(x)$

$$f(x) = \begin{cases} 1 & \text{ if } w^Tx \geq 0 \\ -1 & \text{ otherwise } \end{cases}$$

The criterion is given by

$$E(w) = -\sum_i t_i (w^Tx_i)$$

Intuitively, the critrion is trying to match the sign of $t_i$ and $w^Tx$.

By applying the gradient descent, the $w$ can be updated by

$$w_{new} = w_{old} + \gamma t_i x_i$$

where $\gamma$ is the learning rate.


Convergence:
- When linear separable, perceptron converges in finite steps, upper-bounded by $\frac{R^2}{\gamma^2}$ where $R$ is the upper-bound of norm of training set $x$. The solution and convergence typically depends on the initial value. [proof of this statement](https://www.cse.iitb.ac.in/~shivaram/teaching/old/cs344+386-s2017/resources/classnote-1.pdf)
- When not linear separable, it will never converge


### 4.2. Generative Model
The general Gaussian Discriminative Analysis (GDA) is to model the class conditional densities with multivariate Gaussian distribution

$$p(x | y=k) = \mathcal{N}(x|\mu_k, \Sigma_k)$$

If there is no assumption about the $\Sigma_k$, then it is known as **quadratic discriminant analysis** (QDA), which is literally a quadratic classifier (because of $\Sigma$)

GDA has two simplifications: Naive Bayes and Linear Discriminative Analysis.

#### 4.2.1. Naive Bayes
If the $\Sigma_k$ is diagonal, this is equivalent to the Naive Bayes classifier.

Naive bayes is based on the assumption that features $\mathbf{x}$ are mutually independent given the output $\mathcal{C}_k$ (i.e. $y=k$). The joint probability distribution is modeled as follows

$$p(y=k, x_1, x_2, ..., x_n) = p(y=k) \prod_i p(x_i| y=k)$$

#### 4.2.2. Linear Discrimative Analysis
When $\Sigma_k$ in GDA are shared or tied across all classes (i.e.: $\Sigma_k = \Sigma$), then it is known as the linear discrimative analysis (LDA)
$$p(y=k | x) \propto \exp (\mu_c^T \Sigma^{-1} x -\frac{1}{2} \mu_c^T \Sigma^{-1} \mu_c + \log \pi_c)$$

It is called linear because the exponent can be expressed in linear with respect to $x$

LDA can be solved analytically with MLE

$$\pi_k = \frac{1}{N} \sum_i 1\{ y_i = k \}$$

$$\mu_k = \frac{1}{N} \sum_i 1\{ y_i=k \} x_i$$

$$\Sigma = \frac{1}{N} \sum_i (x_i - \mu_{y_i})(x_i - \mu_{y_i})^T$$

### 4.3. Discriminative Model
Advantage of discrminative models is that it has fewer adaptive parameters which may lead to improved predictive performance

#### 4.3.1. Logistic Regression
The logistic regression has the probabilistic form

$$p(y|x; w) = Bernoulli(y | \mu(x); w)$$

and

$$\mu(x) = \sigma(w^Tx)$$

The negative log-likelihood for logistic regression is given by

$$\mathcal{l}(w) = - \sum_i log(\mu_i^{y_i} (1-\mu_i)^{1-y_i}) = -\sum_i y_i \log \mu_i + (1-y_i) \log(1-\mu_i) $$

This is called the **cross entropy loss** function

Taking derivative of this, we derive

$$\nabla {l} = X^T(\mu - y)$$

By computing Hessian of this function, we know

$$H = \sum_i \mu_i(1-\mu_i) x_i x_i^T = X^TSX$$

Therefore, the objective is convex and has a unique global minimum.

##### 4.3.1.1. Max Entropy
maximize the entropy of joint distribution 

$$H(X) = -\sum p(x,y)\log(p(x,y))$$

with the feature constraint of $E_p f_j = E_{p^{~}} f_j$

[Tutorial](https://web.stanford.edu/class/cs124/lec/Maximum_Entropy_Classifiers.pdf)

##### 4.3.1.2. Logistic Regression vs Naive Bayes
Each parameter of Logistic Regression is corresponding to a set of Gaussian Naive Bayes parameters. (i.e. every Gaussian Naive Bayes can be mapped to a logistic regression model)

In gaussian naive bayes, we have
$$p(y=1 | x) = \frac{p(x|y=1)p(y=1)}{p(x|y=1)p(y=1)+p(x|y=0)p(y=0)} = \frac{1}{1+exp(-a)}$$

where

$$a = log\frac{p(x|y=1)p(y=1)}{p(x|y=0)p(y=0)}$$



However, the general Gaussian Naive Bayes cannot be represent with logistic regression, for example, decision boundary of Gaussian Naive can be curved, but logistic regression cannot. When Naive Bayes has the same covariance across all classes, then they have the same form.

See Andrew Ng's paper for asymptotic convergence comparison.

## 5. Sparse Kernel Models

### 5.1. Kernel Methods

### 5.2. Maximum Margin Classifier (SVM)



## 6. Tree Model
### 6.1. CART (Classification and Regression Tree)
The decision tree models are defined by recursively partitioning the input space, and defining a local model in each resulting region of input space. They are popular for several reasons.

Pros
- easy to interpret
- can handle discrete and continuous features
- insensitive to monotone transformation (scaling)

Cons
- accuracy is not as good as other models
- high variance

#### 6.1.1. ID3
ID3 is an algorithm by Ross Quilan in 1986. It recursively split the tree based on the Information gain.
The splitting process is by greedy search (the optimal split is NP-hard)

**Definition (information gain)** Information gain is defined as follows
$$IG(S,A) = H(S) - H(S|A) = H(S) - \sum_{t \in T} p(t)H(t)$$
where $S$ is the entropy of parent node, $A$ is the target splitting attribute, $T$ is the subsets splitted by $A$

#### 6.1.2. C4.5, C5
These have some improvements from ID3 including
- can handle discrete (categorical feature) as well
- can handle missing values

### 6.2. Ensemble
#### 6.2.1. Boosted
Adaboost

#### 6.2.2. Bootstrap Aggregation (Bagging)
As mentioned, the CART model is a high variance model. To reduce the vairance, we can apply the Bagging to ensemble $n$ trees
Typically, each tree receives a randomly chosen subset of the original data.

$$f(x) = \sum_{i=1}^N \frac{1}{N} f_i(x)$$

Unfortunately, simply rerun the same tree model will result in highly correlated predictors (which still results in high variance). Random forest can decorrelate it by randomly choosing the subset of input variables for each tree.

## 7. Sequential Model

### 7.1. Markov Model 

$$p_(\textbf{x}_1, ..., \textbf{x}_N) = \prod_{n=2}^{N} p(\textbf{x}_n | \textbf{x}_1, ..., \textbf{x}_{n-1})$$

## 8. Reference
[1] Bishop, Christopher M. Pattern recognition and machine learning. springer, 2006.

[2] Rosenblatt, Frank. Principles of neurodynamics. perceptrons and the theory of brain mechanisms. No. VG-1196-G-8. Cornell Aeronautical Lab Inc Buffalo NY, 1961.

[3] Minsky, Marvin, and Seymour A. Papert. Perceptrons: An introduction to computational geometry. MIT press, 2017.

[4] Sutton, Charles, and Andrew McCallum. "An introduction to conditional random fields." Foundations and Trends® in Machine Learning 4.4 (2012): 267-373.

[5] CS229 Lecture Note 

[6] Mitchell, Tom M. "Machine learning." (1997).
