---
layout: post
title: Facts in Number Theory
tags: [math, tricks]
---

$$
\mu * I = \epsilon \\
\phi * I = id \\
id * \mu =\phi
$$

* 一个数的约数个数 = $$O(n^{1 \over 3})$$. 
* 整除分块是 $$O(n^{0.5})$$ 的, 整除分块套整除分块是 $$O(n^{0.75})$$ 的, 加记忆化就是 $$O(n^{2 \over 3})$$ 的, 也就是杜教筛. 
* 遇到再说吧. 
* 对于一些函数 $$gcd(f(a), f(b))=f(gcd(a, b))$$, 尤其是一些如此递推的数列: $$f(n + 2) = f(n) + f(n + 1)$$. 
* $$fi(n + m) = fi(m)fi(n + 1) + fi(m - 1)fi(n)$$. 

