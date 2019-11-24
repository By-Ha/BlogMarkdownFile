title: Luogu P2014 选课
categories: 树形背包
tags: [编程,DP,树形DP]
date: 2019-06-07 23:33:00
---
- 这个树形背包咋和前面的不太一样，好歹算是了结了更多关于树形背包的东西。

<!--more-->

```cpp
#include <iostream>
#include <bitset>

using namespace std;

#define maxn 302
#define maxm 302
int N,M,id[maxn],di[maxn],ri[maxn];
int w[maxn],f[maxn][maxm];
bitset <maxn> E[maxn];



void dfs(int nd){
    static int cnt = 0;
    id[nd] = cnt;
    di[cnt] = nd;
    cnt++;
    for(int i = 1;i<=N;i++){
        if(E[nd][i])
            dfs(i);
    }
    ri[id[nd]] = cnt;
}

int main()
{
    cin>>N>>M;
    int k;
    for(int i = 1;i<=N;i++){
        cin>>k>>w[i];
        E[k][i] = 1;
    }
    dfs(0);
    for(int i = N;i>=0;i--){
        for(int j = 0;j<=M;j++){
            if(N == 0){
                f[i][j] = max(f[ri[i]][j],f[i+1][j]+w[di[i]]);
            }else
                f[i][j] = max(f[ri[i]][j],f[i+1][j-1]+w[di[i]]);
        }
    }
    cout<<f[0][M];
    return 0;
}

```