# 0x431 Classification

- [1. Vocabulary Modeling](#1-vocabulary-modeling)
    - [1.1. Word Models](#11-word-models)
    - [1.2. Character-based Models](#12-character-based-models)
    - [1.3. Subword Models](#13-subword-models)
        - [1.3.1. Byte pair encoding](#131-byte-pair-encoding)
        - [1.3.2. Unigram-based segmentation](#132-unigram-based-segmentation)
- [2. Language Model](#2-language-model)
    - [2.1. N-gram LM](#21-n-gram-lm)
        - [2.1.1. Concepts](#211-concepts)
        - [2.1.2. Models](#212-models)
        - [2.1.3. Tools](#213-tools)
- [3. Topic Model](#3-topic-model)
    - [3.1. Latent Semantic Analysis (LSA)](#31-latent-semantic-analysis-lsa)
    - [3.2. PLSA](#32-plsa)
    - [3.3. Latent Dirichlet Analysis (LDA)](#33-latent-dirichlet-analysis-lda)
- [4. Fixed Embedding Models](#4-fixed-embedding-models)
- [5. Contextualized Models](#5-contextualized-models)
    - [5.1. ELMO](#51-elmo)
    - [5.2. BERT](#52-bert)
    - [5.3. GPT](#53-gpt)
- [6. Reference](#6-reference)

This page covers the classification models based on neural networks

## 1. Vocabulary Modeling
### 1.1. Word Models
The easiest way to model vocabulary is to use word embedding. 

The issues of word embedding

- huge vocabulary requires more memory and computation in morphological rich languages.
- not all words are not appearing in training data (UNK words)

One of the Common ways to solve the first issue is to use a threshold.

### 1.2. Character-based Models
encode characters for the entire sentence, but very slow to train.

### 1.3. Subword Models
Separate rarer words into subwords, then embed. The cons is that it cannot handle non-cancatenative morphology. 

Common way to find subword are

#### 1.3.1. Byte pair encoding
segment into characters
merge most frequent subword sequence for fixed number of operations

#### 1.3.2. Unigram-based segmentation
create vocabulary of most frequent character n-grams
use EM algorithm to optimize probabilities, remove subwords with low prob

## 2. Language Model
### 2.1. N-gram LM
#### 2.1.1. Concepts
**Maximum Likelihood Estimator**
$$\hat{P}(w_n | w_1, w_2, ... , w_{n-1}) = \frac{c(w_1, ...., w_n)}{c(w_1, ..., w_{n-1})} $$

MLE does not work in practice because of sparseness
Backoff
Backoff assigns probability with n-1 gram if n-gram is not seen in the training set

$$ P(w_n | w_1^{n-1}) = P(w_n | w_1^{n-1})
\begin{cases}
P(w_n | w_1^{n-1})  & \text{if the n-gram is seen in the training set } \\
b(w_1^{n-1}) p(w_n | w_2^{n-1})  & \text{otherwise} \end{cases} $$

#### 2.1.2. Models
Major models are as follows:

**LM (Witten-Bell)**
**LM (Good Turing)**

without tear
**LM (Jelinek-Mercer)**
interpolation

**LM (Kneser-Ney Smoothing)**
high order is to use count-based probability with absolute discount

$$ P(w) \propto \max (c(w)-d , 0) $$

low order is to use the fertility context as the backoff smoothing

$$ P(w) \propto | w': c(w', w) > 0 | $$

**Stupid Backoff**

#### 2.1.3. Tools
[1] provides a very good tutorial for efficient implementation

SRILM
Tutorial

ARPA format
How backoff is estimated in srilm

// compute ppl
```bash
ngram -lm corpus.arpa -ppl test_corpus.txt
```

MSRLM
numerator, denominator of normalization are delayed until query. Therefore costs more CPU time for querying. [1]
memory-mapping implementation
IRSLTM
Kenlm
data

Google 1 Trillion n-gram (2006)
Implementations
bit packing: if unigram is less than 1M, trigram can be packed into a 64bit long long by using index of 20 bit for each word
rank: store the rank of counting instead of the count themselves

## 3. Topic Model
### 3.1. Latent Semantic Analysis (LSA)
Apply SVD to term-document matrix, then approximate with low rank matrix

### 3.2. PLSA
### 3.3. Latent Dirichlet Analysis (LDA)

## 4. Fixed Embedding Models

## 5. Contextualized Models
Topic models and naive embedding models assign fixed embedding or representations to each word. However, the word might have different meaning in different contexts, therefore some recent models are using contextualized representations instead of the fixed embeddings.

### 5.1. ELMO
param (100M)

### 5.2. BERT
param (340M)

There are two approaches to train bert: Masked LM and Next Sentence Prediction. They are used at the same time.
- Masked LM: randomly mask a word and use other words to predict it
- next sentence prediction: classify whether one sentence come after the other sentence

**How to use BERT**
- If input is a single sentence and output is a sentence class task, connect the CLS token's embedding with a linear classifier to predict. BERT can be fine-tuned, linear-classifier is trained from scratch

- If input is a sentence and output is the class for each word, then connect every word's embedding with a classifier to train.

- If input is two sentencs and output is a single class (e.g: NLI task), connect two sentences with SEP token and use the CLI to predict.
 
- If extraction-based QA, suppose document $D={d_1, d_2, ..., d_N}$ and query $Q= {q_1, q_2,...,q_M}$, then train a model to use $D,Q$ to predict two integer $s,e$ which indicates the answer is ${d_s, ..., d_e}$. $s,e$ can be found by training two embedding which should be near the target index word's embedding respectively.

### 5.3. GPT
GPT is a language model using transformer.
GPT-1 param (0.1M)
GPT-2 param (1.5B)
GPT-3 param (175B)...

GPT can do some zero-shot/few-shot learning by giving the task description to model somehow. For example, 

- reading comprehension: formulate sentence like this $d_1, d_2, ..., d_N, "Q:", q_1, q_2, ..., q_M, "A:"$, then it will generate the answer somehow. results look to be good now
- summarization: formulate sentence like this $d_1, d_2, ..., d_N, "TL;DR:"$ and predict, results not that good

In the few-shot learning, you give several samples to the model, however, no gradient descent is required.
- translation: $e_1, e_2, "=" f_1, f_2, "next", e_1, e_2 "="$, results no that good

## 6. Reference
[1] Kenneth Heafield' PDF thesis
[2] [ELMO, BERT, GPT lecture](https://www.youtube.com/watch?v=UYPa347-DdE)
[3] CMU 11-737 Multilingual Natural Language Processing