title: Luogu P5315 头像上传
categories: 基本算法
tags: [编程]
date: 2019-06-01 20:49:00
---
- 丢脸丢到家了


<!--more-->

- 这是一道模拟题，只要读题，十分水。
- 但是，我就是没好好读题
- 。。。。
- 第一遍 > -> >=    90
- 第二遍 nonfreopen -> freopen 0
- 第三遍 100
- 手残啊
```cpp
#include <iostream>
#include <cstdlib>
#include <cstdio>

using namespace std;

int N,L,G;

int main()
{
    cin>>N>>L>>G;
    int t1,t2;
    for(int i = 1;i<=N;i++){
        cin>>t1>>t2;
        while(t1>G||t2>G)
            t1 /= 2,t2 /= 2;
        if(t1<L||t2<L){
            cout<<"Too Young\n";
            continue;
        }
        if(t1 == t2){
            cout<<"Sometimes Naive\n";
            continue;
        }else {
            cout<<"Too Simple\n";
            continue;
        }
    }
    return 0;
}

```