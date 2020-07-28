---
title: powerful-number
date: 2020-07-26 21:53:37
tags: ["数论"]
---

powerful number（也）是用来求一类积性函数的前缀和的。
假如一个数x为powerful number，那么他的每一个质因子的次数都超过一次，即x可以写作$a^ 2b^ 3$
由$x=a^ 2b^ 3$可知n以内的powerful number的个数是$O(n^ \frac 2 3)$级别的。
找的话直接枚举质因子爆搜就是了，反正到时候也需要powerful number的质因数分解。

现在考虑怎么用这个性质。
现在告诉你一个积性函数f(n),求f(n)的前缀和。
现在考虑构造两个积性函数g(n),h(n)，使得$f=g\times h$。

先考虑构造一个g,使得对于所有的质数p，满足$g(p)=f(p)$。

