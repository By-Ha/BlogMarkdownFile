title: 雅礼集训|game
categories: 线段树
tags: [雅礼]
date: 2019-10-21 16:22:00
---
```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 100000;

int S[N << 2];
int L[N << 2], R[N << 2];

void push_up(int u, int l, int r) {
    int d = min(L[r], R[l]);
    //L树是我们出牌,取我们拥有的面值在r~inf的牌和对面拥有的面值在1~r-1的牌对打肯定是我们赢,\
      将胜利个数计入答案并且在我们和对手的牌树中删去这些(上一层不更新即-d).\
      批注:好生精妙
    S[u] = S[l] + S[r] + d;
    L[u] = L[l] + L[r] - d;
    R[u] = R[l] + R[r] - d;
}

void modify(int u, int l, int r, int p, int x, int y) {//线段树(两棵)
    if (l == r) { L[u] += x; R[u] += y; return; }

    int mid = (l + r) >> 1;
    if (p <= mid) 
        modify(u << 1, l, mid, p, x, y);
    else 
        modify(u << 1 | 1, mid+1, r, p, x, y);

    push_up(u, u << 1, u << 1 | 1);
}


int n;
multiset<int> B;
int a[N + 5], b[N + 5];

int main() {
	// freopen("game.in","r",stdin);
	// freopen("game.out","w",stdout);
    scanf("%d", &n);
    for (int i = 0; i < n; ++i) scanf("%d", a + i), modify(1, 1, N, a[i], 0, 1);
    for (int i = 0; i < n; ++i) scanf("%d", b + i), modify(1, 1, N, b[i], 1, 0), B.insert(b[i]);
    // modify(1, 1, N, a[i], x, y) => 在线段树l的a[i]位置加上x,b[i]位置加上y.

    int ans = S[1];
    for (int i = 0; i < n; ++i) {//对第i位的答案进行二分
        modify(1, 1, N, a[i], 0, -1);//删去a[i](对手出牌)

        int l = a[i] + 1, r = *B.rbegin();//确定范围,只能出比对手大1~手上最大牌面值的牌
        while (l < r) {
            int mid = (l + r + 1) >> 1;
            modify(1, 1, N, mid, -1, 0);//对mid尝试进行删除操作

            if (1 + S[1] == ans) l = mid; else r = mid - 1;//如果答案恰好减少1,说明可以出这张牌,否则只能出更少的牌
            modify(1, 1, N, mid, +1, 0);//恢复mid,以进行下一步二分
        }

        modify(1, 1, N, l, -1, 0);//将操作写入
        if (l <= r && 1 + S[1] == ans) { -- ans; printf("%d ", l); B.erase(B.find(l)); }
        //得出了第一位答案(打掉对面的情况),进行相关操作
        else {//不能打掉对面的情况
            modify(1, 1, N, l, +1, 0);//将modify(1, 1, N, l, -1, 0);操作撤销

            l = 1, r = a[i];//重新在自己牌库1~a[i]范围内牌值二分
            while (l < r) {
                int mid = (l + r + 1) >> 1;
                modify(1, 1, N, mid, -1, 0);

                if (S[1] == ans) l = mid; else r = mid - 1; //这一步不对答案造成影响
                modify(1, 1, N, mid, +1, 0);
            }
            modify(1, 1, N, l, -1, 0);//写入

            printf("%d ", l); //输出
            B.erase(B.find(l));
        }
    }
    return 0;
}
```