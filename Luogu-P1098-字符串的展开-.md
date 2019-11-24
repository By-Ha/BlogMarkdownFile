title: Luogu P1098 字符串的展开 
categories: 模拟
tags: [编程]
date: 2019-06-06 17:30:00
---
- CCF虐我千百遍，我。。。

<!--more-->

- [评测记录][1]

- 我语文真的那么差么？？？
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

int p1,p2,p3;
string s;
char output[500000];
int End = 0;

char format(char ch){
    if(p1 == 3){
        return '*';
    }else if(p1 == 1){
        if(isalpha(ch))
            if('A'<=ch&&ch<='Z')
                return ch - 'A' + 'a';
            else return ch;
    }else if(p1 == 2){
        if(isalpha(ch))
            if('a'<=ch&&ch<='z')
                return ch - 'a' + 'A';
            else return ch;
    }
    return ch;
}
void char2out(char ch){
    output[End++] = ch;
}
void Fill(char c1,char c2){
    char2out(c1);
    char tmp;
    if(p1 == 3){
        for(char ch = c1+1;ch<c2;ch++){
            memset(output+End,int('*'),p2);
            End+=p2;
        }
        return ;
    }
    if(p3 == 1){//顺序
        tmp = format(c1+1);
        for(char ch = c1+1;ch<c2;ch++){
            memset(output+End,tmp++,p2);
            End+=p2;
            /*
            for(int i = 1;i<=p2;i++){
                char2out(format(ch));
            }*/
        }
    }else if(p3 == 2){//逆序
        tmp = format(c2-1);
        for(char ch = c2-1;ch>c1;ch--){
            memset(output+End,tmp--,p2);
            End+=p2;
            /*
            for(int i = 1;i<=p2;i++){
                char2out(format(ch));
            }*/
        }
    }
}
void calc(){
    for(int i = 0;;i++){
        if(s[i] == '+')
            continue;
        if(s[i] == '\0'){
            output[End] = '\0';
            break;
        }
        else if(s[i+1] == '-'&&s[i]<s[i+2]){
            if(s[i] == s[i+2] - 1){
                char2out(s[i]);
                s[i+1] = '+';
            }
            else if(isdigit(s[i])&&isdigit(s[i+2])){
                Fill(s[i],s[i+2]);
                s[i+1] = '+';
            }else if(isalpha(s[i])&&isalpha(s[i+2])){
                Fill(s[i],s[i+2]);
                s[i+1] = '+';
            }
            else char2out(s[i]);

        }
        else char2out(s[i]);
    }
}

int main()
{
    scanf("%d %d %d\n",&p1,&p2,&p3);
    getline(cin,s);
    calc();
    cout<<output;
    return 0;
}

```


  [1]: https://www.luogu.org/recordnew/lists?uid=166274&pid=1098&status=&sort=0