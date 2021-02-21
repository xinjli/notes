# 0x421 Supervised Learning

- [1. Foundation](#1-foundation)
    - [1.1. Generative Model](#11-generative-model)
    - [1.2. Discriminative Model](#12-discriminative-model)
- [2. Linear Model](#2-linear-model)
    - [2.1. Linear Regression Model](#21-linear-regression-model)
        - [2.1.1. Frequentist Linear Regression](#211-frequentist-linear-regression)
            - [2.1.1.1. MLE](#2111-mle)
            - [2.1.1.2. Ridge Regression](#2112-ridge-regression)
        - [2.1.2. Bayesian Linear Regression](#212-bayesian-linear-regression)
    - [2.2. Linear Classification Model](#22-linear-classification-model)
        - [2.2.1. Discriminant Functions](#221-discriminant-functions)
        - [2.2.2. Fisher's Linear Discriminant](#222-fishers-linear-discriminant)
        - [2.2.3. The perceptron algorithm](#223-the-perceptron-algorithm)
    - [2.3. Probabilistic Generative Model](#23-probabilistic-generative-model)
        - [2.3.1. Naive Bayes](#231-naive-bayes)
        - [2.3.2. Linear Discrimative Analysis](#232-linear-discrimative-analysis)
    - [2.4. Probabilistic Discriminative Model](#24-probabilistic-discriminative-model)
        - [2.4.1. Max Entropy](#241-max-entropy)
- [3. Sequential Data](#3-sequential-data)
    - [3.1. Markov Model](#31-markov-model)
- [4. Reference](#4-reference)

## 1. Foundation
The ML probabilistic model can be largely grouped into the following two groups.

### 1.1. Generative Model
Generative Model is to model the joint distribution $P(\textbf{x}, \textbf{y})$. This typically can be broken into modelling of conditional distribution and probability distribution:

- models a class conditional densities $P( \textbf{x} | \mathcal{C}_k)$
- models a prior $P(\mathcal{C}_k)$

With the joint distribution, the prediction task is easily solve with posterior distribution.
- compute posterior $P(\mathcal{C}_k | \textbf{x})$ with Bayes' theorem
  
Generative model tends to be better when training data are limited, but the bound of the asymptotic error is reached more quickly by a  generative model than a discriminative model.

### 1.2. Discriminative Model
The approach of a discriminative model is to model posterior distribution directly $P(\textbf{y} | \textbf{x})$ directly. For example, in the classification task, it is to model  $P(\mathcal{C}_k | \textbf{x})$ directly 

Parameters are typically estimated with MLE. for example, by iterative reweighted least squares (IRLS)

Discriminative model tends to achieve better results with asymptotic classification error (when training data are large enough)

## 2. Linear Model
### 2.1. Linear Regression Model
Linear regression is a model of the form

$$p(y|x, \theta) = \mathcal{N}(w^Tx, \sigma^2)$$

#### 2.1.1. Frequentist Linear Regression
##### 2.1.1.1. MLE
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

##### 2.1.1.2. Ridge Regression

#### 2.1.2. Bayesian Linear Regression
In a full Bayesian treatment, the parameter $w$ has a distribution, the conjugate prior of the likelihood can be given as follows (if variance is known)

$$p(w) = \mathcal{N}(m_0, S_0)$$

### 2.2. Linear Classification Model
The goal of classification is to take an input vector $\textbf{x}$ and assigned it to one of $K$ discrete classes $\mathcal{C_k}$

#### 2.2.1. Discriminant Functions
In the case of two classes, we assign to $C_1$ if $y \geq 0$, otherwise $C_0$

$$y(\textbf{x}) = \textbf{w}^T x + w_0$$

the decision boundary is $y = 0$

In the case of multiclasses, we create a single $K$-class discriminant comprising $K$ linear functions of the form

$$y_k(\mathbf{x}) = \mathbf{w}_k^T \mathbf{x} + w_{k0}$$

where we assgin a point $\mathbf{x}$ to $\mathcal{C}_k$ if $(\forall j \neq k) y_k(\mathbf{x}) > y_j(\mathbf{x})$

The decision regions are connected and convex

The following are three solutions

Least squares for classification
has the closed-form but lack robustness to outliers

#### 2.2.2. Fisher's Linear Discriminant
#### 2.2.3. The perceptron algorithm
Proposed by Rosenblatt [1]. Minsky's work analyzes perceptron [2]. When linear sepratable, perceptron converges in finite steps, upper-bounded by $\frac{R^2}{\gamma^2}$ where $R$ is the upper-bound of norm of training set $x$, and $\gamma$ is the learning rate.  [proof](https://www.cse.iitb.ac.in/~shivaram/teaching/old/cs344+386-s2017/resources/classnote-1.pdf)


### 2.3. Probabilistic Generative Model
The general Gaussian Discriminative Analysis (GDA) is to model the class conditional densities with multivariate Gaussian distribution

$$p(x | \mathcal{C}_k) = \mathcal{N}(x|\mu_k, \Sigma_k)$$

If there is no assumption about the $\Sigma_k$, then it is known as quadratic discriminant analysis (QDA), which is literally a quadratic classifier (because of $\Sigma$)

GDA has two simplifications: Naive Bayes and Linear Discriminative Analysis.

#### 2.3.1. Naive Bayes
If the $\Sigma_k$ is diagonal, this is equivalent to the Naive Bayes classifier.

Naive bayes is based on the assumption that features $\mathbf{x}$ are mutually independent given the output $\mathcal{C}_k$. The joint probability distribution is modeled as follows

$$p(\mathcal{C}_k, x_1, x_2, ..., x_n) = \mathcal{C_k} \prod_i p(x_i|\mathcal{C}_k)$$

#### 2.3.2. Linear Discrimative Analysis
When $\Sigma_k$ in GDA are shared or tied across all classes (i.e.: $\Sigma_k = \Sigma$), then it is known as the linear discrimative analysis (LDA)
$$p(\mathcal{C}_k | x) \propto \exp (\mu_c^T \Sigma^{-1} x -\frac{1}{2} \mu_c^T \Sigma^{-1} \mu_c + \log \pi_c)$$

It is called linear because the exponent can be expressed in linear with respect to $x$

LDA can be solved analytically with MLE

$$pi_k = \frac{1}{N} \sum_i 1\{ y_i = k \}$$

$$\mu_k = \frac{1}{N} \sum_i 1\{ y_i=k \} x_i$$

$$\Sigma = \frac{1}{N} \sum_i (x_i - \mu_{y_i})(x_i - \mu_{y_i})^T$$

### 2.4. Probabilistic Discriminative Model
Advantage of discrminative models is that it has fewer adaptive parameters which may lead to improved predictive performance

#### 2.4.1. Max Entropy
maximize the entropy of joint distribution $H(X) = -\sum p(x,y)\log(p(x,y))$ with the feature constraint of $E_p f_j = E_{p^{~}} f_j$

[Tutorial](https://web.stanford.edu/class/cs124/lec/Maximum_Entropy_Classifiers.pdf)

## 3. Sequential Data

### 3.1. Markov Model 

$$p_(\textbf{x}_1, ..., \textbf{x}_N) = \prod_{n=2}^{N} p(\textbf{x}_n | \textbf{x}_1, ..., \textbf{x}_{n-1})$$

## 4. Reference
[1] Bishop, Christopher M. Pattern recognition and machine learning. springer, 2006.

[2] Rosenblatt, Frank. Principles of neurodynamics. perceptrons and the theory of brain mechanisms. No. VG-1196-G-8. Cornell Aeronautical Lab Inc Buffalo NY, 1961.

[3] Minsky, Marvin, and Seymour A. Papert. Perceptrons: An introduction to computational geometry. MIT press, 2017.

[4] Sutton, Charles, and Andrew McCallum. "An introduction to conditional random fields." Foundations and Trends® in Machine Learning 4.4 (2012): 267-373.

[5] CS229 Lecture Note 

