---
title: （扩展）欧拉定理
date: 2020-07-28 19:14:17
tags: ["数论"]
category: Note
---

### 前置知识
裴蜀定理：存在整数x,y使得gcd(a,b)=ax+by
拓展欧几里得一波完事。

### 欧拉定理
$\forall a,s.t. \gcd(a,p)=1, a^ {\phi(p)}\equiv 1\pmod p$
随便口胡的，类比费马小定理。
考虑把那$\phi(p)$个元素拎出来形成一个集合。
现在把集合里的元素每个都乘上a对p取模然后扔到另一个集合中。
随便根据裴蜀定理随便口胡一下发现新的集合和原来的集合使一样的，所以膜意义下的乘积也没有变。
但是实际上新的集合比原集合多乘了$\phi(p)$个a,所以$a^ {\phi(p)} \equiv 1\pmod p$

### 扩展欧拉定理
考虑不互质的一对数a,m（当然就算互质也成立）。下面等式中百分号为取模。
$$
\left\{ \begin{array}{rcl}
a^ b \equiv &a^ b                   &\pmod m,\forall b < \phi(m) \\
a^ b \equiv &a^ {b\%\phi(m)+\phi(m)}&\pmod m,\forall b\geq \phi(m)
\end{array}\right.
$$
$b<\phi(m)$时显然，现在考虑$b \geq \phi(m)$时的情况。
考虑将m质因数分解，则$m=\prod_ i p_ i^ {q_ i}$
那么只需要保证$\forall i,a^ b \equiv a^ {b\%\phi(m)+\phi(m)}\pmod {p_ i^ {q_ i}}$
因为假设$x \equiv y\pmod {m_ 1},x \equiv y\pmod {m_ 2}$，那么$x-y$一定是$m_ 1m_ 2$的倍数。
现在考虑某一个$p_ i^ {q_ i}$。
1. 假如a与$p_ i^{q_ i}$互质，那么根据欧拉定理显然。
2. 若不互质，那么由$p_ i$是质数得a是$p_ i$的倍数，即$a=k_ ip_ i$。

考虑第2种情况。
~~用脚都能想到$a^ b \equiv 0\pmod p$~~
首先，因为$\phi$是积性函数，所以$\phi(m)\geq\phi(p_ i^{q_ i})$。
又可以归纳说明$\forall q \in \mathbb Z^ +,\phi(p^ q)>=q$
所以$\phi(m)\geq q_ i$，得$a^ {\phi(m)}=k_ i^ {\phi(m)}p_ i^ {\phi(m)}\equiv 0\pmod {p_ i^ {q_ i}}$
而$b\geq\phi(m)$时等式两侧a的指数都显然$\geq\phi(m)$，所以两边都为0，也成立。
以上。

例题：在做了（进度：0%）
