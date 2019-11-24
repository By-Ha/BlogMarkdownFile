title: Luogu P1447 [NOI2010]能量采集
categories: 欧拉函数
tags: [数论]
date: 2019-07-03 21:37:00
---
- 然而并不会
<!--more-->
> 千万不要上课不听讲不然和我一样现在看不懂答案是什么意思

- 首先我有答案，但是并不知道是怎么做的

```latex

a + b

$ a + b $

```

```cpp
#include <iostream>
#include <algorithm>
#include <cmath>

using namespace std;
#define re register
long long N,M,ph[1000005];
long long phi(int n){
    long long  Ans = n;
    for(int i = 2;i<=sqrt(n);i++){
        if(n%i == 0){
            Ans = Ans / i * (i-1);
            while(n%i==0)
                n = n / i;
        }
    }

    if(n>1)
        Ans = Ans / n * (n-1);
    return Ans;
}
int main()
{
    cin>>N>>M;
    long long ans = 0;
    if(N>M)
        swap(N,M);
    for(int i = 1;i<=N;i++){
        ph[i] = phi((long long)i);
    }
    for(int i = 2;i<=N;i++){
        ans += (ph[i]*(N/i)*(M/i))<<1;
    }
    cout<<ans+N*M;
    return 0;
}
```
- 简单分析一下发现，这一题答案先求出了 $1-min(n,m)$ 中的欧拉函数值。
- 然后从 $2-min(n,m)$ 做了一遍欧拉函数和鬼东西`(N/i)*(M/i)`相乘的运算???
- 于是开始探究`(N/i)*(M/i)`是毛线了。

> 写了个简单的小程序打表
```cpp
#include<bits/stdc++.h>
using namespace std;
int main(){
	int n,m;
	cin >> n >> m;
	for(int i = 1;i<=n;i++){
		cout << n/i << ' ' << m/i << ' ' << (n/i)*(m/i)<<endl;
	}
	return 0;
}
```
- 当输入$4\ 5$时输出为
>4 5 20
>2 2 4
>1 1 1
>1 1 1
- 一看，，emmm为什么最开始没有反应过来???
- $\lfloor{\frac{n}{i}}\rfloor$就是$n$以内的数有$i$这个公因子的数的数量吗!
- 所以$\lfloor{\frac{n}{i}}\rfloor\times\lfloor{\frac{m}{i}}\rfloor$不就是在$m\times n$的数内$m$和$n$被$i$整除的数的多少吗!!!
- 如果还是不懂,请看图
![m,n,i][1]
- 图中红线代表单个的$\lfloor{\frac{n}{i}}\rfloor$或$\lfloor{\frac{m}{i}}\rfloor$由数轴上的几个点扩展成的二维线。
- 我们可以看到，红线交点(黑点)的数目就是$\lfloor{\frac{n}{i}}\rfloor\times\lfloor{\frac{m}{i}}\rfloor$。
- 那么$\varphi(2)\times\lfloor{\frac{n}{i}}\rfloor\times\lfloor{\frac{m}{i}}\rfloor$就是
- 剩下的我也不会了


  [1]: https://typecho-1252071452.cos.ap-beijing.myqcloud.com/img/cid/106_1.png