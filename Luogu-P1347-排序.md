title: Luogu P1347 排序
categories: 拓扑排序
tags: [编程]
date: 2019-06-04 16:59:00
---
- 目前照着题解学了一遍拓扑排序，下次自己写再交付评测
<!--more-->


```cpp
#include <bits/stdc++.h>

using namespace std;
int N,M;
char c1,c2,c3;
vector <int> ve[29];
int ru[29],ru1[29],ru2[29];
int sum,ans,k,have;
set <int> s1;

void make(){
    queue <int> q;
    memset(ru1,0,sizeof(ru1));
    for(int i = 0;i<26;i++){
        for(int j = 0;j<(int)ve[i].size();j++){
            ru1[ve[i][j]]++;
        }
    }
    for(int i=0; i<26; i++){
        if(ru1[i]==0&&s1.count(i)){
            q.push(i);
            cout<<char(i+'A');
        }
    }
    while(!q.empty()){
        int u=q.front();
        q.pop();
        for(int i=0; i<ve[u].size(); i++){
            int v=ve[u][i];
            ru1[v]--;
            if(ru1[v]==0){
                q.push(v);
                cout<<char(v+'A');
            }
        }
    }
}
void topu(){
    queue<pair<int,int> > q;
    for(int i = 0;i<26;i++){
        if(ru[i] == 0&&s1.count(i)){
            q.push(make_pair(i,1));
            sum++;
        }
    }
    while(!q.empty()){
        int u = q.front().first;
        int va = q.front().second;
        q.pop();
        for(int i = 0;i<ve[u].size();i++){
            int v = ve[u][i];
            ru[v]--;
            if(ru[v] == 0){
                sum++;
                q.push(make_pair(u,va+1));
                ans = max(ans,va+1);
            }
        }
    }
    if(ans == N){
        printf("Sorted sequence determined after %d relations: ",k);
        make();
        printf(".");
    }
    if(sum != have) {
        printf("Inconsistency found after %d relations.",k);
    }
    return ;
    End:
        exit(0);
}
int main()
{
    cin>>N>>M;
    for(int i = 1;i<=M;i++){
        c1 = getchar();
        while(!isalpha(c1))
            c1 = getchar();
        c2 = getchar();
        c3 = getchar();
        k = i;
        ve[c1 - 'A'].push_back(c3-'A');
        s1.insert(c1-'A');
        s1.insert(c3-'A');
        have = s1.size();
        ru2[c3-'A'] ++ ;
        sum = 0;
        ans = 0;
        memcpy(ru,ru2,sizeof(ru2));
        topu();
    }
    printf("Sorted sequence cannot be determined.");
    return 0;
}
```