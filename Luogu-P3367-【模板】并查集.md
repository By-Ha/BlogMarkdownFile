title: Luogu P3367 【模板】并查集
categories: 并查集
tags: [编程,并查集]
date: 2019-06-09 10:17:00
---
- 这次使用结构体写，速度差不多


<!--more-->

```cpp
#include <iostream>
#include <cstdio>

using namespace std;

#define maxn 10002
int N,M;
struct nd{
    int u,v,w;
};
struct dset{
    int f[maxn];
    int gf(int x){
        if(x == this->f[x])
            return x;
        else return this->f[x] = gf(this->f[x]);
    }
    void init(){
        for(int i = 1;i<=N;i++){
            this->f[i] = i;
        }
    }
    void add(int x,int y){
        f[this->gf(x)] = this->gf(y);
    }
    bool Find(int x,int y){
        if(this->gf(x) == this->gf(y))
            return true;
        else return false;
    }
}a;
int main()
{
    scanf("%d%d",&N,&M);
    a.init();
    int t1,t2,t3;
    for(int i = 1;i<=M;i++){
        scanf("%d%d%d",&t1,&t2,&t3);
        if(t1 == 1){
            a.add(t2,t3);
        }else {
            if(a.Find(t2,t3)) printf("Y\n");
            else printf("N\n");
        }
    }
    return 0;
}

```