---
title: powerful-number
date: 2020-07-26 21:53:37
tags: ["数论"]
---

定义大写函数为小写函数的前缀和。

powerful number（也）是用来求一类积性函数的前缀和的。
假如一个数x为powerful number，那么他的每一个质因子的次数都超过一次，即x可以写作$a^ 2b^ 3$
由$x=a^ 2b^ 3$可知n以内的powerful number的个数是$O(n^ \frac 2 3)$级别的。
找的话直接枚举质因子爆搜就是了，反正到时候也需要powerful number的质因数分解。

现在考虑怎么用这个性质。
现在告诉你一个积性函数f(n),求f(n)的前缀和。
现在考虑构造两个积性函数g(n),h(n)，使得$f=g\times h$。

先考虑构造一个g,使得对于所有的质数p，满足$g(p)=f(p)$。
这时我们会发现$f(p)=g(p)h(1)+h(p)g(1)=g(p)+h(p)$（f不是全0函数，所以根据积性得g(1)=1,h(1)=1）
得到$h(p)$为0，又h为积性函数，所以只有下标为powerful number的地方h才可能不为0。
那么要求的东西可以写成：
$$
\begin{aligned}
F(n)=\sum_ i^ nf(i)&=\sum_ {ij<=n}h(i)g(j) \\
&=\sum_ {i<=n}h(i)G(\lfloor \frac n i\rfloor)
\end{aligned}
$$

这样我们只需要遍历使h(i)可能不是0的i即可求出答案。
很多时候h是可以用特殊性质快速求的，但一般情况可以分解质因数并对于每一个质数p预处理:
~~反正又不会成为瓶颈~~ 你写起来不烦吗
（听说这等价于多项式求逆但我看不出来。。。）
$$
\begin{aligned}
f(p^ q)&=\sum_ {i=0}^ q g(p^ i)h(p^ {q-i}) \\
h(p^ q)&=f(p^ q)-\sum_ {i=1}^ q g(p^ i)h(p^ {q-i})

% f(n)&=\sum_ {d|n} g(d)h(\frac n d) \\ 
% h(n)&=f(n)-\sum_ {d|n,d\not =1}g(d)h(\frac n d)
\end{aligned}
$$

例题：在做了（进度：0%）
