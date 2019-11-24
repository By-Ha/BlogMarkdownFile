title: Luogu P1004 方格取数
categories: 多维DP
tags: [编程]
date: 2019-05-21 17:09:00
---
> 我承认我模仿着题解写的


<!--more-->

- 做这个的时候只想到贪心，但是没有证明，于是凉凉
- 没想到真的要使用`四维数组`求解...
- 希望下次能想明白吧

```cpp
//DP++
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

int E[12][12][12][12];
int e[12][12];
int N;


int main() {
    scanf("%d",&N);
    int t1=1,t2,t3;
    while(t1 != 0) {
        scanf("%d %d %d",&t1,&t2,&t3);
        e[t1][t2]=t3;
    }
    for(int i = 1; i<=N; i++) {
        for(int j = 1; j<=N; j++) {
            for(int k = 1;k<=N;k++){
                for(int l = 1;l<=N;l++){
                    E[i][j][k][l] = e[i][j]+e[k][l]+max(max(E[i-1][j][k][l-1],E[i-1][j][k-1][l]),max(E[i][j-1][k-1][l],E[i][j-1][k][l-1]));
                    if(i == k && j == l)
                        E[i][j][k][l] -= e[i][j];
                }
            }
        }
    }
    cout<<E[N][N][N][N];
    return 0;
}
```