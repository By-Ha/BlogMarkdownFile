title:  P2024 [NOI2001]食物链
categories: 并查集
tags: [并查集]
date: 2019-09-11 15:14:00
---
[链接](https://www.luogu.org/problem/P2024)


<!--more-->

- 很精妙的一个小题.

- 显然是建立并查集,我们一个动物拥有三个集合,第一个是他被谁(哪种动物)吃的并查集,第二个是他自己(自己这种动物)的并查集,第三个是他吃谁(哪种动物的并查集).

- 我们知道如果两个动物是同类的话,那么他们拥有共同的天敌和共同的食物,我们可以将他们的这几个集合合并(可以理解为把这两个动物看成一个个体),如果他们互相吃,即A吃B,那么B的敌人就是A,同类就是A的食物,食物就是A的敌人.A的食物就是B,A的敌人就是B的食物,A的同类就是B的敌人.

- 我们只需要在更改前判断是否经过这两种操作导致出现错误就可行.

```cpp

#include <cstdio>
#include <iostream>
using namespace std;

int qr(){int ret=0,f=1;char ch = getchar();while(!isdigit(ch))f=ch=='-'?-1:1,ch=getchar();while(isdigit(ch))ret=ret*10+ch-'0',ch=getchar();return ret*f;}

#define maxN 50005
#define Rint register int

struct UFS{
    int f[maxN<<2];
    void init (){for(int i = 1;i<=(maxN<<2);i++)f[i] = i;}
    int gf(int x){if(f[x] == x) return x;else return f[x] = gf(f[x]);}
    void merge(int x,int y){f[gf(x)] = gf(y);}
    bool query(int x,int y){return gf(x) == gf(y);}
    int section(int x){if(x < maxN)return 1;if(x < maxN*2)return 2;else return 3;}
}ufs;
int N,K;
int main(){
    ufs.init();
    N = qr(),K = qr();
    Rint cnt = 0;
    for(Rint i = 1,seg,x,y;i<=K;i++){
        seg = qr(),x = qr(),y = qr();
        if(x>N||y>N){cnt++;continue;}
        x += maxN , y += maxN;
        if(seg == 1){
            if(ufs.gf(x+maxN) == ufs.gf(y)||ufs.gf(x-maxN) == ufs.gf(y))
            {cnt++;continue;}
            ufs.merge(x,y),ufs.merge(x+maxN,y+maxN),ufs.merge(x-maxN,y-maxN);
        }
        else {
            if(ufs.gf(x) == ufs.gf(y)||ufs.gf(x-maxN) == ufs.gf(y))
            {cnt++;continue;}
            ufs.merge(x+maxN,y),ufs.merge(y-maxN,x),ufs.merge(x-maxN,y+maxN);
        }
    }
    printf("%d",cnt);
    return 0;
}

```