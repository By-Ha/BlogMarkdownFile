title: Luogu P1064 金明的预算方案
categories: 树形背包
tags: [编程,DP,树形DP]
date: 2019-06-07 22:56:00
---
- 树状背包模板
- 迷，所以有一点注释。


<!--more-->


```cpp
/*
testcase :
1000 5
800 2 0
400 5 1
300 5 1
400 3 0
500 2 0
*/
#include <algorithm>
#include <iostream>
#include <bitset>
using namespace std;

#define maxn 65
#define maxm 32005

bitset <maxn> E[maxn];
int id[maxn],di[maxn],cnt,ri[maxn];
int N,M,w[maxn],val[maxn];
int f[maxn][maxm];

void dfs(int nd){
    id[nd] = cnt;
    di[cnt] = nd;
    cnt ++;
    for(int i = 1;i<=N;i++){
        if(E[nd][i])
            dfs(i);
    }
    ri[id[nd]] = cnt;
}

int main(){
    cin>>M>>N;
    int p,q;
    for(int i = 1;i<=N;i++){
        cin>>w[i]>>p>>q;
        val[i] = w[i] * p;
        E[q][i] = 1;
    }
    dfs(0);
    for(int i = N;i>=0;i--){
        for(int j = 1;j<=M;j++){
            int k = di[i];
            if(j>=w[k])
                /*已经完成从最后一个到i , i号物品的价格可以是上一棵树的价格(即不选这一棵子树)或者自己和所有
                儿子子树(这是已完成的)的价格最大值。
                好迷啊，看了半天才看懂
                */
                f[i][j] = max(f[ri[i]][j],f[i+1][j-w[k]]+val[k]);
            else f[i][j] = f[ri[i]][j];
        }
    }
    cout<<f[0][M];
    return 0;
}

```