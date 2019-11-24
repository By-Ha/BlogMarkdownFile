title: Luogu P2396 yyy loves Maths VII
categories: 状态压缩DP
tags: [编程,DP]
date: 2019-05-27 21:59:00
---
- 人生第一个紫题，不看题解真的不会写代码，但是大概思路还是对的。


<!--more-->

- 就是DP了，但是我比较孬不会写，然后去题解区orz了，下面是自己仿写的。
- **卡常预警！！！**

```cpp
#include <iostream>
#include <cstdio>

using namespace std;

#define mod 1000000007

int N,M;
int t;
int b1,b2;
int poss[(1<<24)+5];
int dis[(1<<24)+5];
#define lowbit(x) x&(-x)

int main()
{
    cin>>N;

    for(int i = 1;i<=N;i++){
        scanf("%d",&dis[1<<(i-1)]);
    }
    cin>>M;
    if(M == 1){
        scanf("%d",&b1);
    }else if(M == 2){
        scanf("%d %d",&b1,&b2);
    }
    poss[0] = 1;
    int MAX = (1<<N)-1;
    for(register int i = 1;i<=MAX;i++){
        dis[i] = dis[i^(lowbit(i))] + dis[lowbit(i)];
        if(dis[i] == b1||dis[i] == b2)
            continue;
        for(register int j = i,k=lowbit(j);j;j = j^k,k=lowbit(j)){
            poss[i] += poss[i^k];
            if(poss[i]>mod)
                poss[i] -= mod;
        }
    }
    cout<<poss[MAX];
    return 0;
}
```