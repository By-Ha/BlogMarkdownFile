title:  P1896 [SCOI2005]互不侵犯
categories: 状态压缩DP
tags: [状态压缩DP]
date: 2019-09-11 15:27:00
---
[链接](https://www.luogu.org/problem/P1896) 


<!--more-->


> 在N×N的棋盘里面放K个国王，使他们互不攻击，共有多少种摆放方案。国王能攻击到它上下左右，以及左上左下右上右下八个方向上附近的各一个格子，共8个格子。

- 典型的`状态压缩DP`,(看数据范围识算法),我们考虑如何解决.

- 首先肯定要确保一行内不能互相攻击,考虑左移运算符`(0b010)<<1` == `(0b100)`,假设等式左边的1是人,那么等式右边的1就是人向左攻击,右移运算符同理可以模拟向右攻击.想到`&`运算符没有,假设人是`0b01011`,想左攻击的范围就是`0b10110`,重合的地方就是人在那能被向左的攻击弄死的地方,`&`运算符仅在一个地方只有人或者只有攻击时才或者全都没有时才为0,所以我们可以根据左右移加上与原数字`&`的方式判断是否成立.

- 隔行,隔行左上右上打和单行一样,主要考虑向上,显然我们不需要让攻击偏移,只用把两排人物代表的数字一`&`就知道了.向下,左下,右下同理.

- 记得开ll

```cpp

#include <cstdio>
#include <iostream>
#include <algorithm>
using namespace std;

#define Rint register int

int qr(){int ret=0,f=1;char ch = getchar();while(!isdigit(ch))f=ch=='-'?-1:1,ch = getchar();while(isdigit(ch))ret=ret*10+ch-'0',ch=getchar();return ret*f;}

long long f[10][520][85];
int cnt[512];

int main(){
    // freopen("input.in","r",stdin);
    // freopen("ans.out","w",stdout);
    Rint N,K;
    N = qr(),K = qr();
    for(Rint i = 0;i<512;i++){
        Rint j = i;
        while(j>0){if(j&1)cnt[i]++;j>>=1;}
    }
    for(Rint i = 1;i<=N;i++){
        for(Rint j = 0;j<(1<<N);j++){
            if( (!(j&(j<<1))) && (!(j&(j>>1))) )
            for(Rint j_=0;j_<(1<<N);j_++){
                if( (!(j_&(j_<<1))) && (!(j_&(j_>>1))) )
                if( (!(j&j_)) && (!((j_<<1)&j)) && (!((j_>>1)&j)) ){
                    f[i][j][cnt[j]] = 1;
                    for(Rint k = cnt[j]+1;k<=K;k++){
                        f[i][j][k] += f[i-1][j_][k-cnt[j]];
                    }
                }

            }
        }
    }
    long long ans = 0;
    for(int i = 0;i<=511;i++)
        ans+=f[N][i][K];
    printf("%lld",ans);
	return 0;
}

```