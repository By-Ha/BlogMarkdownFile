title: Luogu P1017 进制转换
categories: 基本算法
tags: [编程]
date: 2019-06-06 17:28:00
---
- 我讨厌数学

<!--more-->

```cpp
#include <iostream>

using namespace std;

int a,base;
char ch[] = {'0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F','G','H','I','J'};
char ans[200005];
int End = 200000;
void calc(int num){
    if(num == 0)
        return ;
    int mod = num % base;
    if(mod < 0){
        mod -= base;
        num+=base;
    }
    ans[End--] = ch[mod];
    calc(num/base);
}
int main()
{
    ans[End+1] = '\0';
    cin>>a>>base;
    cout<<a<<'=';
    calc(a);
    cout<<ans+End+1;
    cout<<"(base"<<base<<')';
    return 0;
}

```