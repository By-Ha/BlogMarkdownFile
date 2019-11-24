title: CF174B File List 附带题解
categories: 模拟
tags: [编程,模拟]
date: 2019-07-13 20:52:00
---
> CF174B File List

- ~~还没有题解,我来水一发~~

> [题面跳转](https://www.luogu.org/problemnew/show/CF174B)
- 题目大体意思是让我们把接下来的字符串分割成很多文件名,使文件名前缀不超过8个字符,文件名后缀不超过3个字符。
- 这题特别水，我们只需要找到每两个`.`之间的字符数,如果大于11或者小于2就输出`NO`,再对开头结尾做一个特判,判断其是否超过3个,8个字符长的限制,这题就能过。
# 我用鲜血写出:模拟题绝对不能不打草稿直接写
- 仅仅我一人就有字符串展开和这道题提交次数爆炸 ~~(吃枣要因为浪费评测资源死在这)~~

![药丸图片](https://typecho-1252071452.cos.ap-beijing.myqcloud.com/img/Solution/CF174B.png)

- 接下来结合代码讲解(分割字符=='.')

```cpp
#include <iostream>
#include <string>
#include <cstdio>//头文件,打死不用stdc++.h，反正我觉得会让代码变慢

using namespace std;

string s; //读入字符串

bool isOK() {//判断函数，用于判断字符串是否可以分割
	int len = 0;//长度，存储两个分割字符之间的字符数量
	int plc = 1;//位于第几块，以'.'区分块
	int i;//循环变量
	for(i = 0; s[i]!='\0'; i++) {//从头读到尾
		if(s[i] == '.') {//如果找到分割字符'.'
			if(plc == 1) {//恰好是第一块,也就是开头
				if(len == 0||len>8)//开头直接是分割字符或者长度超限
					return false;//选择退役
			} else if(len <=1 || len >= 12) {//再中间的几块中字符长度如果太小太大
				return false;//退役
			}
			len = 0;//读到分割字符后记得重置长度
			plc ++;//顺便把分块(不是算法分块)的编号加上
			continue;
		}
		len ++;//不是分割字符只加上该字符的长度1，不做运算
	}
	//如果最后一块有字符,并且长度小于等于3，返回true，否则返回false，这里写得非常随意，其实可以通过len判断，但我懒啊
	return s[i-1] != '.'&&(s[i-2]=='.'||s[i-3]=='.'||s[i-4]=='.');
}

int main() {//伟大的主函数
	cin >> s;//标准方法读入，只有'.'这个字符的话不用getline
	if(isOK())//如果可以分割
		cout << "YES" << endl;//NOI大喊CCF选我 Cu -> Au
	else {
		cout << "NO" <<endl;//选择退役
		return 0;//注意退役退到底
	}
            //开始输出内容
	int i,j;//因为循环变量在之后要用到计算，所以要存下来，不能作为for循环局部变量
	for(i = 0; s[i]!='\0'; i++) {//对于s中的每一个字符
		if(s[i]=='.') {//我们判断是否为分割字符
			putchar(s[i]);//如果是的我们先把他输出了
			for(j = 1; s[i+j]!='\0'; j++)//这里注意是i+j我有好几遍都是j然后WA，RE暴毙，这个主要功能是数有多少个字母在'.'之间
				if(s[i+j] == '.')//如果扫到了'.'，退出循环
					break;
			j--;//由于我们会把最后一个'.'计入答案,所以要减去一个
			if(j>3)//如果j的长度超过一次能输出的上限,也就是3个
				j = 3;//把j赋值3
			else if(s[i+j+1]!='\0') j--;//如果这里不是字符串末尾还要给后面留一个输出的字符，例如aaa.bc.aa 我们会拆成aaa.b 和 c.aa 中间的bc留一个给后面当头用
			for(int k = 1; k<=j; k++) {
				if(!isalpha(s[i+k]))//好像没什么用
					continue;
				putchar(s[i+k]);//输出
			}
			i+=j;//加上已经输出的
			putchar('\n');//注意换行
			continue;//不要再执行putchar了，所以continue
		}
		putchar(s[i]);//如果不是分割的'.'字符，直接输出
	}
	return 0;//告诉CCF   您AK NOI
}
```
# 最后，祝各位NOIp2019 RP++







