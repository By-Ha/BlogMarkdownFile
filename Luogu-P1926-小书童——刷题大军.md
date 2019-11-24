title: Luogu P1926 小书童——刷题大军
categories: 0/1背包
tags: [编程,DP]
date: 2019-07-01 18:10:00
---
- 背包

<!--more-->

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

#define N 500

int task[N],val[N],like[N];
int n,m,k,r;
int ans[N];

int main()
{
    scanf("%d%d%d%d",&n,&m,&k,&r);
    for(int i = 1;i<=n;i++){
        scanf("%d",&like[i]);
    }
    for(int i = 1;i<=m;i++){
        scanf("%d",&task[i]);
    }
    for(int i = 1;i<=m;i++){
        scanf("%d",&val[i]);
    }
    for(int i = 1;i<=m;i++){
        for(int j = r;j>=task[i];j--){
            ans[j] = max(ans[j],ans[j-task[i]]+val[i]);
        }
    }
    for(int i = 1;i<=r;i++){
        if(ans[i]>=k){
            r -= i;
            break;
        }
    }
    memset(ans,0,sizeof(ans));
    for(int i = 1;i<=n;i++){
        for(int j = r;j>=like[i];j--){
            ans[j] = max(ans[j],ans[j-like[i]]+1);
        }
    }
    cout << ans[r];
    return 0;
}

```