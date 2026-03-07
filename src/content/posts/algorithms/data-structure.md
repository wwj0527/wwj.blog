---
title: 数据结构：栈、单调结构、字典树、链表
published: 2026-03-06
description: 栈、单调栈、单调队列、字典树、单链表的实现与典型应用。
tags: ["算法", "数据结构", "栈", "单调栈", "字典树"]
category: 编程与技术
draft: false
---

## 栈（模拟）

用数组模拟栈，支持 push、pop、empty、query。

```cpp
// 对应源码：stack.cpp
int stk[N], tt;
void push(int x) { stk[tt++] = x; }
void pop() { tt--; }
int query() { return stk[tt - 1]; }
```

---

## 单调栈

求每个数左边/右边第一个比它小（或大）的数。

**思路**：维护单调递增栈。新元素入栈前，弹出所有比它大（或小）的栈顶，此时栈顶即为「左边第一个满足条件的数」。

```cpp
// 对应源码：monotonous-stack.cpp
// 求每个数左边第一个比它小的数
while (n --){
    int x; cin >> x;
    while (tt && stk[tt - 1] >= x) pop();
    cout << (tt ? stk[tt - 1] : -1) << " ";
    push(x);
}
```

---

## 单调队列

求滑动窗口内的最小值/最大值。

**思路**：用双端队列维护下标，保证队内元素单调。队头超出窗口则出队；新元素入队前，从队尾弹出比它大（求最小值）或小（求最大值）的元素。

```cpp
// 对应源码：monotonous-list.cpp
// 滑动窗口最小值
for (int i = 0; i < n; i ++ ){
    if (hh <= tt && i - k + 1 > q[hh]) hh ++ ;
    while (hh <= tt && a[q[tt]] >= a[i]) tt -- ;
    q[ ++ tt] = i;
    if (i >= k - 1) printf("%d ", a[q[hh]]);
}
```

---

## 字典树（Trie）

支持插入字符串、查询字符串出现次数。

```cpp
// 对应源码：trie.cpp
int son[N][26], cnt[N], idx;
void insert(char str[]){
    int p = 0;
    for (int i = 0; str[i]; i ++ ){
        int u = str[i] - 'a';
        if (!son[p][u]) son[p][u] = ++ idx;
        p = son[p][u];
    }
    cnt[p] ++;
}
int query(char str[]){
    int p = 0;
    for (int i = 0; str[i]; i ++ ){
        int u = str[i] - 'a';
        if (!son[p][u]) return 0;
        p = son[p][u];
    }
    return cnt[p];
}
```

---

## 单链表（数组模拟）

用 `e[]` 存值，`ne[]` 存 next 指针，`idx` 分配新结点。

```cpp
// 对应源码：Singly Linked List.cpp
int head, e[N], ne[N], idx;
void add_to_head(int x){
    e[idx] = x; ne[idx] = head; head = idx++;
}
void add_to_k(int k, int x){
    e[idx] = x; ne[idx] = ne[k]; ne[k] = idx++;
}
void delete_k(int k) { ne[k] = ne[ne[k]]; }
```
