---
layout: post
title: Normal Couting Skills
tags: [math, tricks]
---

一般来说一些东西各不相同比相同计数要好做, 一般来说期望题倒推比较稳. 

## 反演

### 二项式反演

### 斯特林数反演

### 莫比乌斯反演

### 单位根反演

我都 ~~懒得写~~ 不会. 

## 斯特林数

$$
x^{\underline n} = \sum\limits_{i} (-1)^{n - i}{n \brack i}x^i \\
x^{\overline n} = \sum\limits_{i} {n \brack i}x^i \\
{n \brace m} = {(-1)^m \over m!}\sum\limits_i (-1)^i i^n {m \choose i} \\
n^m = \sum\limits_i n^{\underline i}{m \brace i} \\
n! = \sum\limits_i {n \brack i} \\
{n + 1 \brace k + 1} = \sum\limits_i {n \choose i} {i \brace k}
$$

## 容斥

### 组合数容斥

$$
[n = 0] = (1 - 1)^n = \sum\limits_{i} (-1)^i {n \choose i} = \sum\limits_{T \subseteq S}(-1)^{\vert T\vert}
$$

这是不是说明了 $$0^0 = 1$$ 呢? 

### 斯特林数容斥

$$
x^{\underline n} = \sum\limits_i (-1)^{n - i}{n \brack i}x^i \\
[n = 0] = 1^{\underline n} = \sum\limits_i (-1)^{n - i}{n \brack i} = \sum\limits_{A}\prod\limits_{i}(-1)^{A_i - 1}(A_i - 1)!
$$

$$A$$ 是集合划分, 一般是正整数拆分枚举的. 