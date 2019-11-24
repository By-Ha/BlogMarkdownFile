title: Luogu P1833 樱花
categories: 分组背包
tags: [编程,DP,背包,分组背包]
date: 2019-06-07 20:44:00
---
- 好惨，把value 和 time 打反了，还过了样例，然后0分。。。
- 注意下这题用cin会暴毙(不是时间而是格式)

<!--more-->

> 19.9.11 upd:我这个程序写快读干嘛啊

```cpp
#include <iostream>
#include <cstdio>

using namespace std;

#define maxt 1005
#define maxn 10005
int N;
int f[maxt];
int tsh,tsm,teh,tem;
int T,ti,va,pi;

int qr(){
    char ch=getchar();
    int ret=0;
    while(!isdigit(ch))
        ch = getchar();
    while(isdigit(ch)){
        ret = ret * 10 +ch - '0';
        ch = getchar();
    }
    return ret;
}

int main()
{
    tsh=qr();
    tsm=qr();
    teh=qr();
    tem=qr();
    N = qr();
    //cin>>tsh>>tsm>>teh>>tem>>N;
    T = teh * 60 + tem - tsh * 60 - tsm;
    for(int i = 1;i<=N;i++){
        cin>>ti>>va>>pi;
        if(pi == 0)
            for(int i = ti;i<=T;i++){
                f[i] = max(f[i-ti]+va,f[i]);
            }
        else {
            int base = 0;
            for(int j = pi;j>=1;){
                if(base == 0){
                    base = 1;
                    j -= base;
                }else if(j - (base <<1)<0){
                    base = j;
                    j = 0;
                }else {
                    base <<= 1;
                    j -= base;
                }
                for(int k = T;k>=base*ti;k--){
                    f[k] = max(f[k],f[k - ti * base]+va * base);
                }
            }
        }
    }
    cout<<f[T];
    return 0;
}

```