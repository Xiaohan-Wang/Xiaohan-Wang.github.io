---
layout:     post
title:      A Few Useful Things to Know About Machine Learning
subtitle:   2012 (Communications of the ACM)
date:       2020-02-11
author:     Xiaohan
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - ML
---

## 12 trick lessons in ML

### 1. learning algorithm = representation + evaluation + optimization
**representation**:  choosing a representation for a learner is tantamount to choosing the hypothesis space
 
**evaluation**: evaluation function

**optimization**: the method to search among the hypothesis space

![-w801](/img/15817081275431.jpg)
三者同样重要

### 2. generalization counts
strict separation between training and test set.

###  3. data alone is not enough
1. data alone is not enough, no matter how much of it you have. (e.g. Consider learning a Boolean function of (say) 100 variables from a million examples. There are 2^100 − 10^6 examples whose classes you don’t know.)

2. every learner must embody some **knowledge or assumption** beyond the data it's given in order to generalize beyond it.

3. learners are like lever: less knowledge/assumption + (data) -> useful results. But it still need more than zero input knowledge to work.

4. corollary: one of the key criteria for choosing a representation is which kinds of knowledge are easily expressed in it.

### 4. overfitting
if the knowledge and data we have are not sufficient to completely determine the correct classifier -> risk of overfitting

Note: A common misconception about overfitting is that it is caused by noise, but severe overfitting can occur even in the absence of noise.

### 5. high dimensions
1. curse of dimensionality:  our intuition, which come from a three-dimensional world, often do not apply in high-dimensional ones. Naively, one might think that gathering more features never hurts, since at worst they provide no new information about the class. But in fact their benefits may be outweighed by the curse of dimensionality.

2. blessing of non-uniformity: In most applications examples are not spread uniformly throughout the instance space, but are concentrated on or near a lower-dimensional manifold. 

### 6. theoretical guarantees
The main role of theoretical guarantees in machine learning
is not as a criterion for practical decisions, but as a source of
understanding and driving force for algorithm design. In this
capacity, they are quite useful; indeed, the close interplay
of theory and practice is one of the main reasons machine
learning has made so much progress over the years. But
caveat emptor: learning is a complex phenomenon, and just
because a learner has a theoretical justification and works in
practice doesn’t mean the former is the reason for the latter.

### 7. feature engineering
 Often, the raw data is not in a form that is amenable to learning, but you can construct features from it that are. 
   
Note: features that look irrelevant in isolation may be relevant in combination. For example, if the class is an XOR of k input features, each of them by itself carries no information about the class.
 
### 8. MORE DATA BEATS A CLEVERER ALGORITHM
As a rule of thumb, a dumb algorithm with lots and lots of data beats a clever one with modest amounts of it.

### 9. LEARN MANY MODELS, NOT JUST ONE
model ensembles (researchers noticed that, if instead
of selecting the best variation found, we combine many variations, the results are better—often much better—and at
little extra effort for the user)

### 10.  SIMPLICITY DOES NOT IMPLY ACCURACY
1. contrary to intuition, there is no necessary connection between the number of parameters of a model and its tendency to overfit.

2. the size of the hypothesis space is only a rough guide to what really matters for relating training and test error: the procedure by which a hypothesis is chosen.

### 11. REPRESENTABLE DOES NOT IMPLY LEARNABLE
Just because a function can be represented does not mean it can be learned (e.g.  if the hypothesis space has many local optima of the evaluation function, as is often the case, the learner may not find the true function even if it is representable.). Therefore the key question is not “Can it be represented?”, to which the answer is often trivial, but “Can it be learned?”

### 12. CORRELATION DOES NOT IMPLY CAUSATION