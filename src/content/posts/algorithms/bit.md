---
title: 位运算
published: 2026-03-06
description: lowbit 与二进制中 1 的个数。
tags: ["算法", "位运算"]
category: 编程与技术
draft: false
---

## lowbit

`lowbit(x)` 返回 x 二进制中最后一个 1 及其后面的 0 所表示的数。

利用补码：`x & (-x)`。`-x` 为 x 按位取反加 1，故 `x & (-x)` 恰好得到最低位的 1。

---

## 二进制中 1 的个数

每次减去 `lowbit(x)`，直到为 0，统计次数即为 1 的个数。

```cpp
// 对应源码：number_of_1.cpp
int lowbit(int x) { return x & (-x); }
int count = 0;
while (x) {
    x -= lowbit(x);
    count++;
}
```
