---
layout: post
title: On Polynomials
tags: [math, polynomials]
---

多项式小记. 

## 单位根相关

### 单位根反演

$$
[n | k] = {1 \over n}\sum\limits_{i \in [0, n)}w_n^{ki}
$$

如果在复数域下是好证的, 在模意义下只要想象成复数域, 想必...

由此我们还可以推导 FFT. 

假设我们的第一个矩阵: 

$$
P_{i, j} = w_n^{ij}
$$

第二个矩阵: 

$$
Q_{i, j} = w_n^{-ij}
$$

我们要对向量 $$a$$ 进行正变换: $$a \leftarrow a \times P$$, 逆变换: $$a \leftarrow a \times Q$$. 

观察 $$a \leftarrow a \times P \times Q$$ 到底发生了什么——观察 $$a_x$$ 对 $$a_y$$ 的贡献: 

$$
\begin{aligned}
&a_x \sum\limits_{k \in [0, n)} w_n^{xk - ky} \\
= &a_x n [n | x - y] \\
= &[x = y]n a_x
\end{aligned}
$$

这也就是为什么逆变换后要除以向量长度的原因. 

然后单位根反演还可以求很多别的东西, 比如对一个多项式做关于指数取模的系数筛选: [uoj 450](http://uoj.ac/problem/450)

### 分圆多项式

$$
\Phi_n = \prod\limits_{\gcd(i, n) = 1, i \in [1, n]}(x - w_n^i)
$$

这有什么用呢? 我们在做 $$n$$ 进制不进位加法卷积的时候, 要做长度为 $$n$$ 的 FFT, 没有原根怎么办? 嗯. 

[codeforces 1103 E](https://codeforces.com/contest/1103/problem/E)

[uoj 272](http://uoj.ac/problem/272)

[哎, 可惜这种科技好像只能出裸题…](https://en.wikipedia.org/wiki/Cyclotomic_polynomial)

## 牛顿迭代

如果: 

$$
F(G(x)) = 0 \\
F(G_0(x)) \equiv 0 \pmod{x^{\lceil{n \over 2}\rceil}}
$$

发现如果将第二行这个式子泰勒展开最多只有前两项 $$\mod{n}$$ 有值...

所以有: 

$$
F(G(x)) \equiv F(G_0(x)) + F'(G_0(x))(G(x)-G_0(x)) \equiv 0 \pmod{x^n}
$$

可以解出 $$G(x) \mod{n}$$. 

## 多项式大家族

### 各种操作...

#### 多项式求逆

$$
G(x) = {1 \over F(x)}
$$

以后都是默认对着 $$F(x)$$ 解 $$G(x)$$, 如果不写自变量, 变量都是 $$x$$, 就是说 $$F \text{ stands for } F(x)$$. $$G_0 \equiv G \mod{x^{\lceil{n \over 2}\rceil}}$$. 

用牛顿迭代列出方程: 

$$
F - G^{-1} \equiv 0 \pmod{x^n} \\
F - G_0^{-1} + G_0^{-2}(G - G_0) \equiv 0 \pmod{x^n} \\
G \equiv 2G_0 - G_0^2F \pmod{x^n}
$$

这里比较奇怪的是: 如果不列 $$F - G^{-1} \equiv 0 \pmod{x^n}$$ 就解不出来, 比如列成 $$F^{-1} - G \equiv 0 \pmod{x^n}$$ 又或者 $$FG - 1 \equiv 0 \pmod{x^n}$$ 都解不出来...

#### 多项式求 $$\ln$$

$$
\ln F = \int \ln'(F)dx = \int {F' \over F}dx
$$

#### 多项式求 $$\exp$$

$$
F - \ln G \equiv F - \ln G_0 - {1 \over G_0}(G - G_0) \pmod{x^n} \\
G \equiv G_0(1 + F - \ln G_0) \pmod {x^n}
$$

可以看到你如果要求个 $$\exp F$$ 你就要求 $$\ln F$$, 你就要求 $$F^{-1}$$, 这很不好. 

$$
\exp F = G \\
\exp(F) F' = G' \\
GF' = G'
$$

然后就可以分治 FFT 了. 

### 分治 FFT

关于这个, 有时分治 FFT 的式子里有自己卷自己, 怎么办呢? 

#### 从一道题说起

> 求有多少颗有标号有根树, 满足如下性质: 
> 1. 标号保持堆的性质; 
> 2. 两人在上面玩游戏: 轮流将石子往叶子的方向移动, 不能移动者输. 先手有必胜策略. 

显然地, 设其 EGF 为 $$F(x)$$, 则: 

$$
\int e^F dx = -ln(1 - x) - F
$$

但如果设先手输的 EGF 为 $$F(x)$$, 则: 

$$
F = \int e^{-ln(1 - x) - F} dx
$$

我们分别来观察两者. 

### 前者

我们设 $$G = -ln(1 - x)$$, 然后两边连续求导两次: 

$$
\begin{aligned}
e^F &= G - F' \\
e^F F' &= G' - F''\\
\end{aligned}
$$

将 $$e^F = G - F'$$ 代入: 

$$
(G - F')F' = G' - F''
$$

这样就可以分治 FFT 了. 

但注意到这里有 "自己乘自己" 的项, 这样我们在 $$Solve(l, r)$$, 其中 $$l = 1$$时,  求 $$[0, mid)$$ 项到 $$[mid, r)$$ 项的贡献的时候会出事的. (我们并没有 $$[0, r - l)$$ 项的值. )

于是我们莽一点, 直接用 $$[0, mid)$$ 项卷 $$[0, mid)$$ 项, 然后我们会少算一些东西. 然后我们在 $$Solve(l, r)$$, $$l \not= 0$$ 时, 求 $$[l, mid)$$ 项卷 $$[0, r - l)$$ 项的时候 所有贡献 $$\times 2$$ 这样本来 $$[0, r - l)$$ 项卷 $$[l, mid)$$ 原来少算的就补充上啦! 

### 后者

$$
\begin{aligned}
F &= \int e^{-ln(1 - x) - F} dx \\
{dF \over dx} &= {e^{-F} \over 1 - x} \\
{e^F dF} &= {dx \over 1 - x} \\
\int e^F dF &= \int {dx \over 1 - x} \\
e^F &= -ln(1 - x) + C (it\ seems\ C = 1) \\
F &= ln(1 - ln(1 - x))
\end{aligned}
$$

看起来就是先列微分方程然后参数分离. 


## 牛顿级数

首先在有限微积分中: 

$$
\Delta F(x) = F(x + 1) - F(x) \\
\Delta x^{\underline{n}} = nx^{\underline{n - 1}}
$$

所以我们对于任何一个: 

$$
F(x) = \sum\limits_{i \ge 0} {\Delta^{i}F(0) \over i!}x^{\underline{i}}
$$

这样一来, 我们对于一个从 $$f(0)...f(n - 1)$$ 的点值序列, 只要 $$O(n\log n)$$ 就可以求出其下降幂多项式的形势. (当然一般就写 $$O(n^2)$$)


