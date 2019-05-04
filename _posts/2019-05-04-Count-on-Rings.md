---
layout: post
title: Count on Rings
tags: [math]
---

圆环上的计数问题, 一般有一些诸如: 旋转不同构, 翻转不同构, 之类的限制. 

## 如果说这个圆环非常地自由, 我们可以使用 Polya

### 先从 *The Lemma That's Not Burnside's* 说起

$$
|X/G| = {1 \over |G|}\sum\limits_{g \in G} |X^g|
$$

> 轨道数等于被 $$G$$ 中一个元素保持不动的点的个数的平均数. 

我不懂...

### *Pólya Enumeration Theorem*

$$
l = {1 \over |G|}\sum\limits_{g \in G} t^{c(a_g)}
$$

注意这里的群和 Burnside 的群是不一样的. 这里的置换是纯粹点的置换, 而 Burnside 中的置换是染色方案的置换. 

#### 生成函数形式

设: 

$$
S_k = \sum\limits_{i = 1}^m b_i^k, k = 1, 2, ..., n.
$$

则 Polya 计数定理的生成函数形式为: 

$$
P(G) = {1 \over |G|}\sum\limits_{g \in G}\prod\limits_{i \in [1, n]} S_i^{c_i(g)}
$$

$$c_i(g)$$ 是指 $$g$$ 中长度为 $$i$$ 的环的个数. 这很好理解. 

## 如果这个环并不

更具体地说: 如果我们只能计算 $$g(n)$$ 即不论循环同构的方案数, 那么循环同构本质不同方案数: 

$$
f(n) = {1 \over n}\sum\limits_{d | n} g(d)\phi({n \over d})
$$

证明: 

$$
\begin{aligned}
f(n) &= \sum\limits_{d | n}{1 \over d}\sum\limits_{k | d}\mu({d \over k})g(k) \\
&= \sum\limits_{k | n}g(k)\sum\limits_{k | d | n}\mu({d \over k}){1 \over d} \\
&= {1 \over n}\sum\limits_{k | n}g(k)\sum\limits_{d | {n \over k}}mu(d){n \over kd} \\
&= {1 \over n}\sum\limits_{d | n} g(d)\phi({n \over d})
\end{aligned}
$$

当然也可以用调和级数复杂度的做法随便搞...
