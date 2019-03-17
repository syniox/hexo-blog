---
layout: post
title: "支配树简单笔记"
category: Note
tag: [支配树]
---

严谨证明见参考链接。
[参考链接](https://www.cnblogs.com/meowww/archive/2017/02/27/6475952.html)

### 定义
现在有一个有向图，我们选定一个根叫$r$。（就是流程图（单源有向图）……）
不考虑$r$不能到所有点的情况。
定义一个点$a$支配$b$（$a$是$b$的支配点）当且仅当从$r$出发到$b$的所有路径都经过$a$。
显然$r$和$b$是$b$的支配点。

一个性质: 若$a$支配$c$，且$b$支配$c$，那么必然有$a$支配$b$或$b$支配$a$。
如果都不满足，那么$b$到$c$的所有路径必须经过$a$，$a$到$c$的路径必须经过$b$。（不会严谨的说明，但这样的图真找不到。)

这样的话就可以把支配关系搞成一颗树了。对于每个点，有且仅有它的祖先支配它。
(图盗自顶部链接)
![这张图本来是一个支配树的例子](dom_tr_example.png)

### 求法

在彻底把支配树求出来之前，忽视它。所有的思路和说法都基于DFS树。
我们先对原图跑一边dfs求出dfs树和dfn(点的dfs序）。
dfs树上可能出现三种非树边: 前向边(祖先->后代)、后向边(后代->祖先)、横边(两端无祖先后代关系)。
横边起点的dfn是一定比终点的dfn大的。

> 引理#1: 对于$\forall a,b$满足$dfn[a] \leq dfn[b]$，a到b的路径必然经过a和b的公共祖先(不一定是最近的)。
证明: 考虑把a和b的公共祖先全部删掉。此时a和b在不同的子树中。**剩下的**前向边和后向边不能超越子树，而a所在子树的dfn均比b所在子树小，不存在横边能从a所在子树到b所在子树。

现在定义$x$的最近支配点为$idom(x)$(immediate dominator)。
再定义一个$x$的半支配点为$sdom(x)$(semi-dominator)，用来辅助求出$idom$。
注意: $sdom(x)$不一定支配$x$。
半支配点的定义是这样的：
在图中找出所有点$y$,满足在原图中存在一条$y$到$x$的路径$p_ 1p_ 2\cdots p_ kx$(y不计入路径)，使$\forall i \leq k,dfn[i] \geq dfn[x]$。
(换句话说就是从$y$出发后，不经过$x$的祖先到达$x$，考虑引理#1)
对于所有满足条件的$y$，我们让dfn最小的那个$y$成为$sdom(x)$。
有一个性质是$y$一定是$x$的祖先：
显然x的父亲一定满足条件，所以$dfn[sdom(x)]\leq dfn[x]$。
因为如果不是的话，根据上一行和引理#1总能找到dfn更小的。
还有两个性质（第二个依赖于第一个）：

* $idom(x)$一定是$x$的祖先，因为总有一条路径只经过$x$的祖先链到达$x$。
* $idom(x)$支配$sdom(x)$，否则存在一条路径绕过$idom(x)$到$sdom(x)$后跳出$x$的祖先链到达$x$。


一些定义: 

* $a \rightsquigarrow b$表示$a$经过某种路径到达$b$。
* $a \rightarrow b$表示$a$只经过树边到达$b$。

---

假设现在知道$sdom(x)$，那么如何推出$idom(x)$?
因为$sdom(x)$和$idom(x)$都在$x$的祖先链上，所以把那条链抽出来当线段考虑。
在链上区间$(sdom(x),x]$中找到$dfn[sdom(y)]$最小($sdom(y)$最前/浅)的$y$。
因为区间包含$x$，所以$dfn[sdom(y)] \leq dfn[sdom(x)]$。
下面这步建议自己画图思考(比理解解释还快)，思路都是说明$a$是$b$的支配点且没有比$a$更近的支配点。

* 若$dfn[sdom(y)] = dfn[sdom(x)]$，那么$idom(x)=sdom(x)$
	* 这时$sdom(x)$支配$x$，因为不存在路径能绕过$sdom(x)$到达$(sdom(x),x]$。
	* 从半支配点出发保证能绕出$x$的祖先链到达$x$，所以$(sdom(x),x]$中不存在支配$x$的点。
* 若$dfn[sdom(y)] < dfn[sdom(x)]$，那么$idom(x)=idom(y)$
	* 不存在一种不经过$idom(y)$的路径$r \rightsquigarrow z \rightsquigarrow x$($z$为路径越过$idom(y)$后第一个在$x$祖先链上的点)，如果存在：
		* 若$dfn[z] \leq dfn[y]$，那么$idom(y)$不支配$y$
		* 若$dfn[z] > dfn[y]$，那么$y$不是$dfn[sdom(y)]$最小的那个
	* $idom(y)$后面没有支配$x$的点。
		* 对于$(idom(y),y)$上的某个点，总有路径$r \rightarrow idom(y) \rightsquigarrow y \rightarrow x$绕过它。
		* 对于$(y,x)$上的某个点，因为$dfn[sdom(x)]>dfn[y]$，所以总有路径$r \rightarrow sdom(x) \rightsquigarrow x$绕过它。