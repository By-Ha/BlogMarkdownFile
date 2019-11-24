title: Luogu P1616 疯狂的采药
categories: 完全背包
tags: [编程,完全背包]
date: 2019-06-07 20:21:00
---
- 完全背包 ~~(血流成河)~~


<!--more-->

```cpp
#include <iostream>

using namespace std;

#define maxm 10005
#define maxt 100005

int f[maxt];
int M,T;

int main()
{
    cin>>T>>M;
    int v,t;
    for(int i = 1;i<=M;i++){
        cin>>t>>v;
        for(int i = t;i<=T;i++){
            f[i] = max(f[i],f[i-t]+v);
        }
    }
    cout<<f[T];
    return 0;
}

```