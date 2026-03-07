---
title: 双指针与滑动窗口
published: 2026-03-06
description: 双指针找两数之和、最长无重复子序列、子序列判断。
tags: ["算法", "双指针", "滑动窗口"]
category: 编程与技术
draft: false
---

## 双指针：两数之和

两个升序数组 A、B，找 `A[i] + B[j] = x` 的一组解。

**思路**：`i` 从左向右，`j` 从右向左。若 `A[i] + B[j] > x` 则 `j--`，否则 `i++`。

```cpp
// 对应源码：Target sum.cpp
for (int i = 0, j = m - 1; i < n; i ++){
    while (A[i] + B[j] > x && j >= 0) j--;
    if (A[i] + B[j] == x){
        printf("%d %d", i, j);
        break;
    }
}
```

---

## 滑动窗口：最长无重复子序列

求最长连续子序列，使得其中没有重复元素。

**思路**：`i` 为右端点，`j` 为左端点。用 `b[]` 计数，当 `b[a[i]] > 1` 时不断右移 `j` 并减少计数，直到无重复。

```cpp
// 对应源码：longest_unique_subsequence.cpp
for (int i = 0, j = 0; i < n; i++){
    b[a[i]]++;
    while (j < i && b[a[i]] > 1) b[a[j++]]--;
    res = max(res, i - j + 1);
}
```

---

## 双指针：子序列判断

判断数组 a 是否是数组 b 的子序列（不要求连续，但顺序不变）。

**思路**：`i` 指向 a，`j` 指向 b。若 `a[i] == b[j]` 则 `i++`；每次 `j++`。若最后 `i == n` 则是子序列。

```cpp
// 对应源码：SubsequenceChecker.cpp
while (i < n && j < m){
    if (a[i] == b[j]) i++;
    j++;
}
cout << (i == n ? "Yes" : "No") << endl;
```
