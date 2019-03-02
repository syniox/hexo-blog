---
layout: post
title: "Suffix Array - 后缀数组"
category: Note
---

~~震惊！某中学生竟在学了后缀自动机一年后干出这种事情！~~
……学后缀数组。

定义:

* sa[i]表示字典序第i的后缀的开始下标。
* rank[i]表示以下标i开头的后缀排序后的排名。
* height[i]表示[字典序第i-1的后缀]与[字典序第i的后缀]的lcp(最长公共前缀)

可以通过基数排序求出sa和rank。

基数排序可以在$O(m)$的时间内对二元组(x,y)排序，在后缀数组倍增算法这种值域只有排名大小的排序里特别吃香。
方法是先扫一遍，把(x,y)中的每一个x的个数求出来。然后用前缀和求出对于每一个$x$，他在数组里占用的区间在哪里，然后按y的顺序插入。


```
#define 第i个字符串 从下标i开始字符串
#define 字符串i 从下标i开始字符串
```

定理：
$height[rank[i]] \geq height[rank[i-1]]-1$
考虑第$i-1$个字符串在字典序下的前一个字符串，令他开始的下标为$j$。
如果字符串$j$和字符串$i-1$的首字母不同，那么$height[rank[i-1]]$为0，显然成立。
否则可以同时删掉这两个字符串的首字母。
字符串i-1变成字符串i,字符串j变成字符串j+1，此时这两个串的LCP为height[rank[i-1]]-1。
字符串j的字典序是在i-1前面的，他们首字母又相同，所以字符串j+1的字典序总比字符串i前，height[i]最少也有这两个串的LCP(即height[rank[i-1]]-1)。

定理$\times 2$:
两个后缀i,j的LCP等于$\min_ {k=i+1}^ j (height[k])$
感性理解一下就是把后缀按找字典序排成一排，某一位上的字符在前面的字符相同的情况下总是连续的一段。

这样快速搞出height后可以用rmq查询两个后缀的LCP。
(历史：GDSOI2018T3 SA+网络流裸题……)

code:
```cpp
namespace S{
    int sa[N],rank[N];
    //sa[i]: 字典序第i的下标,rank[i]: 起始下标i的字典序
    char ch[N];

    inline int get_rk(int *rank,int x){
        return x>n?0:rank[x];
    }

    inline void qsort(int *sa,int *rank,int *idx){
        static int buk[N];
        const int limit=std::max(n,128);
        memset(buk,0,limit*sizeof(int));
        for(int i=1; i<=n; ++i){
            ++buk[rank[idx[i]]];
        }
        for(int i=1; i<=limit; ++i){
            buk[i]+=buk[i-1];
        }
        for(int i=n; i; --i){
            sa[buk[rank[idx[i]]]--]=idx[i];
        }
    }

    inline void build(){
        static int tmp[N];
        for(int i=1; i<=n; ++i){
            rank[i]=ch[i]-'0'+1;
            tmp[i]=i;
        }
        qsort(sa,rank,tmp);
        for(int w=1,cnt_rk=0; w<=n&&cnt_rk<n; w<<=1){
            int pos=0;
            for(int i=n-w+1; i<=n; ++i){
                tmp[++pos]=i;
            }
            for(int i=1; i<=n; ++i){
                if(sa[i]>w) tmp[++pos]=sa[i]-w;
            }
            assert(pos==n);
            qsort(sa,rank,tmp);
            cnt_rk=0;
            for(int i=1; i<=n; ++i){
                if(rank[sa[i]]!=rank[sa[i-1]]||get_rk(rank,sa[i]+w)!=get_rk(rank,sa[i-1]+w)){
                    ++cnt_rk;
                }
                tmp[sa[i]]=cnt_rk;
            }
            memcpy(rank+1,tmp+1,n*sizeof(int));
        }
    }
}
```