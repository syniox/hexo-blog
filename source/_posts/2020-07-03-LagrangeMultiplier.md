---
title: "拉格朗日乘数法"
date: 2020-07-03 15:39:30
category: Note
tags: ["数学"]
---

一年多前学的东西，现在全都忘了，也没有时间深入。。。

现在有一个连续可导的函数$f(x_ 1,x_ 2,...)$。
给出一些限制条件$g_ i(x_ 1,x_ 2,...)=0$。
求$f$的最大值（最小值同理）。

一些定义：
$\frac{\partial f}{\partial x_ i}$代表$f$对$x_ i$的偏导。
$\nabla f=[\frac{\partial f}{\partial x_ 1},\frac{\partial f}{\partial x_ 2},...]$表示$f$的梯度向量

可以发现一个极大值点他的梯度向量一定为0，否则总可以沿着梯度向量的方向走足够小的一段距离达到更大的值。

合法范围如果不连续直接求就是了。
边界情况还没考虑清楚，但有些地方并不完全适用。

结论：如果这个点是合法范围的一个极值点，那么$\nabla f$一定能被$\nabla g$线性表示出来。
感性理解：把$\nabla g$表示出来的空间想象成一个超平面。$\vec x$可以向这个超平面的法向量方向走一步，而不引起$g$的变化，却因为走的这一步不和$\nabla f$垂直（否则$\nabla f$在超平面内）导致$f$的值可以发生变化。
所以$\frac{\partial f}{\partial x_ i}=\sum_ j \lambda j \frac{\partial g_ j}{\partial x_ i},\forall i,j$
与$g$的限制联立可以得到典型方程组：

$$
\left\{ \begin{array}{rcl}
\frac{\partial f}{\partial x_ i} & = & \sum_ j \lambda_ j \frac{\partial g_ j}{\partial x_ i} & \forall i,j \\
g_ j(x_ 1,x_ 2,...) & = & 0 & \forall j
\end{array}\right.
$$

---

如果g只有一项的话,等式就变成了这个样子：


$$
\left\{ \begin{array}{rcl}
\frac{\partial f}{\partial x_ i} & = & \lambda \frac{\partial g}{\partial x_ i} & \forall i,j \\ 
g(x_ 1,x_ 2,...) & = & 0 & \forall j
\end{array}\right.
$$

对于一个$\lambda$，可以根据根据第一条算出每一个$x_ i$。
假如$g$对于$\lambda$单调，可以通过二分$\lambda$的形式来逼近限制。
