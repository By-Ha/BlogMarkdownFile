title: Luogu P3954 成绩
categories: 基本算法
tags: [编程]
date: 2019-05-21 17:20:00
---
> 这题这么水，一看就知道是我用来水的

```cpp
#include<bits/stdc++.h>
using namespace std;
int main(){
	int t1,t2,t3;
	cin>>t1>>t2>>t3;
	cout<<t1*2/10+t2*3/10+t3*5/10;
	return 0;
}
```