title: Luogu P1226 【模板】快速幂||取余运算
categories: 快速幂
tags: [编程]
date: 2019-06-01 21:18:00
---
- 我可以退役了


<!--more-->

- 这题坑死我了
- 第一遍学完后自己写，爆了longlong，，，，
- 第二遍`#define int long long`，爆了MOD1
- 第三遍特判，忘记开define。。。
- 第四遍，终于过了
- (x_x)
```cpp
#include <iostream>
#include <bitset>


using namespace std;



int main()
{
    #define int long long
    int a;int b;int mod;
    cin>>a;cin>>b;int tb = b;cin>>mod;
    long long ans = 1;
    int base = a;
    if(mod == 1){
        cout<<a<<'^'<<tb<<" mod "<<mod<<'='<<0;
        return 0;
    }
    while(b>0){
        if(b&1){
            ans *= base;
            ans %= mod;
        }
        base *= base;
        base %= mod;
        b>>=1;
    }
    cout<<a<<'^'<<tb<<" mod "<<mod<<'='<<ans;
    return 0;
}

```