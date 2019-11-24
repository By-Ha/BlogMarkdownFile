title:  P3398 仓鼠找sugar
categories: 树链剖分LCA
tags: [ret,int,define,getchar,unsigned,include]
date: 1970-01-01 08:00:00
---
- 恶心死我了,把俩int压成一个卡空间。。。
- 使用的思想:https://www.luogu.org/blog/user21719/solution-p3398

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>

using namespace std;

#define il inline
#define Rint register int
#define pii pair<int,int>
typedef long long ll;
il int qr(){Rint ret=0,f=1;register char ch = getchar();while(!isdigit(ch)) f=ch=='-'?-1:1,ch=getchar();while(isdigit(ch)) ret=ret*10+ch-'0',ch=getchar();return ret*f;}
#define maxN 100005
#define maxM 100005

unsigned tot;
#define int unsigned
int N,M;
struct CTMD_MLE{
    unsigned f[66675];
    unsigned get(int x){
        if(x == 0) return 0;
        int a,b;
        a = x % 3,b = (x-1) / 3 + 1;
        if(a == 1){
            return f[b<<1] & 0b00000000000111111111111111111111;
        }else if(a == 2){
            unsigned t = f[b<<1] & 0b11111111111000000000000000000000;
            t >>= 21;t += (f[b<<1|1] & 0b11111111110000000000000000000000) >> 11;
            return t;
        }else {
            return f[b<<1|1] & 0b00000000000111111111111111111111;
        }
    }
    void put(int x,unsigned val){
        int a,b;
        a = x % 3,b = (x-1) / 3 + 1;
        val &= 0b00000000000111111111111111111111;
        if(a == 1){
            f[b<<1] &= 0b11111111111000000000000000000000;
            f[b<<1] |= val;
        }else if(a==2){
            f[b<<1] &= 0b00000000000111111111111111111111;
            f[b<<1|1] &= 0b00000000000111111111111111111111;
            int t = val & 0b00000000000000000000011111111111;
            t <<= 21;f[b<<1] |= t;
            t = val & 0b00000000000111111111100000000000;
            t <<= 11;
            f[b<<1|1] |= t;
        }else {
            f[b<<1|1] &= 0b11111111111000000000000000000000;
            f[b<<1|1] |= val;
        }
    };
}f,deep,son,size,fir;

struct CTMD_MLE_{
    unsigned f[133350];
    unsigned get(int x){
        int a,b;
        a = x % 3,b = (x-1) / 3 + 1;
        if(a == 1){
            return f[b<<1] & 0b00000000000111111111111111111111;
        }else if(a == 2){
            unsigned t = f[b<<1] & 0b11111111111000000000000000000000;
            t >>= 21;t += (f[b<<1|1] & 0b11111111110000000000000000000000) >> 11;
            return t;
        }else {
            return f[b<<1|1] & 0b00000000000111111111111111111111;
        }
    }
    void put(int x,unsigned val){
        int a,b;
        a = x % 3,b = (x-1) / 3 + 1;
        val &= 0b00000000000111111111111111111111;
        if(a == 1){
            f[b<<1] &= 0b11111111111000000000000000000000;
            f[b<<1] |= val;
        }else if(a==2){
            f[b<<1] &= 0b00000000000111111111111111111111;
            f[b<<1|1] &= 0b00000000000111111111111111111111;
            int t = val & 0b00000000000000000000011111111111;
            t <<= 21;f[b<<1] |= t;
            t = val & 0b00000000000111111111100000000000;
            t <<= 11;
            f[b<<1|1] |= t;
        }else {
            f[b<<1|1] &= 0b11111111111000000000000000000000;
            f[b<<1|1] |= val;
        }
    };
}ver,nxt;

void read(unsigned u,unsigned v){
    nxt.put(++tot,fir.get(u));
    fir.put(u,tot);
    ver.put(tot,v);
}
#define v ver.get(i)
void dfs1(unsigned u,unsigned fa){
    deep.put(u,deep.get(fa)+1);f.put(u,fa);
    unsigned MAX=0;size.put(u,1);
    for(Rint i = fir.get(u);i;i=nxt.get(i)){
        if(v == fa) continue;
        dfs1(v,u);
        size.put(u,size.get(u)+size.get(v));
        if(size.get(v) > MAX)
            MAX=size.get(v),son.put(u,v);
    }
}

void dfs2(int u,int chainRoot){
    register unsigned s = son.get(u);
    son.put(u,chainRoot);
    if(!s) return ;
    dfs2(s,chainRoot);
    for(Rint i = fir.get(u);i;i=nxt.get(i)){
        if(v == f.get(u) || v == s) continue;
        dfs2(v,v);
    }
}
#undef v
int LCA(int a,int b){
    while(son.get(a) != son.get(b))
        deep.get(son.get(a)) > deep.get(son.get(b)) ? a=f.get(son.get(a)) : b=f.get(son.get(b));
    return deep.get(a) < deep.get(b) ? a : b;
}
signed main(){
    freopen("C:/bigdata.in","r",stdin);
    freopen("C:/ans.out","w",stdout);
    N = qr(),M = qr();
    unsigned t1,t2;
    for(unsigned i = 1;i<N;++i){
        t1 = qr(),t2 = qr();
        read(t1,t2);
        read(t2,t1);
    }
    dfs1(1,0);
    dfs2(1,1);
    for(Rint i = 1,t1,t2,t3,t4,t5,t6;i<=M;++i){
        t1 = qr(),t2 = qr(),t3 = qr(),t4 = qr();
        t5 = LCA(t1,t2);t6 = LCA(t3,t4);
        if(deep.get(t5) < deep.get(t6)) swap(t5,t6),swap(t1,t3),swap(t2,t4);
        if(LCA(t5,t3) == t5 || LCA(t5,t4) == t5){putchar('Y'),putchar('\n');}
        else {putchar('N'),putchar('\n');}
    }
    return 0;
}

```