title: Luogu P1196 [NOI2002]银河英雄传说 
categories: 并查集
tags: [编程,并查集]
date: 2019-06-16 19:40:00
---
```cpp
#include <iostream>
#include <cstdio>
#include <cmath>

using namespace std;
#define maxn 30005
int N,M;
struct Dset{
    int fa[maxn];
    int d[maxn];
    int size[maxn];
    inline void init(){
        for(int i = 1;i<=N;i++){
            fa[i] = i;
            size[i] = 1;
            //d[i] = 1;
        }
        return ;
    }
    int gf(int x){
        if(this->fa[x]==x)
            return x;
        int root = gf(fa[x]);
        this->d[x] += this->d[fa[x]];
        return this->fa[x] = root;
    }
    void add(int x,int y){
        x = gf(x);
        y = gf(y);
        fa[x] = y;
        d[x] = size[y];
        size[y] += size[x];
        return ;
    }
}a;

int main()
{
    int T,t1,t2;
    char ch;
    N = maxn-1;
    cin>>T;
    a.init();
    for(int i = 1;i<=T;i++){
        scanf("\n%c%d%d",&ch,&t1,&t2);
        if(ch == 'M'){
            a.add(t1,t2);
        }else {
            if(a.gf(t1) == a.gf(t2))
                printf("%d",(int)abs(a.d[t2]-a.d[t1])-1),putchar('\n');
            else {
                putchar('-');
                putchar('1');
                putchar('\n');
            }
        }
    }
    return 0;
}

```