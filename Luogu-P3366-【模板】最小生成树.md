title: Luogu P3366 【模板】最小生成树
categories: Kruscal
tags: [编程,图论,最小生成树]
date: 2019-06-09 10:29:00
---
- 比较简单吧.


<!--more-->

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>

using namespace std;

#define maxn 5002
#define maxm 200002
int N,M;
struct nd{
    int u,v,w;
    inline bool operator <(const struct nd &a){
        return this->w<a.w;
    }
}s[maxm];
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
    int ans = 0,line = 0;
    scanf("%d%d",&N,&M);
    for(int i = 1;i<=M;i++){
        scanf("%d%d%d",&s[i].u,&s[i].v,&s[i].w);
    }
    sort(s+1,s+M+1);
    a.init();
    for(int i = 1;i<=M&&line<=N-1;i++){
        if(a.Find(s[i].u,s[i].v))
            continue;
        else {
            line++;
            a.add(s[i].u,s[i].v);
            ans += s[i].w;
        }
    }
    if(line == N - 1)
        cout<<ans;
    else{
        cout<<"orz";
    }
    return 0;
}

```