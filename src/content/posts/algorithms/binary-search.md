---
title: 二分
published: 2026-03-06
description: 整数二分查找边界、浮点数二分求三次方根。
tags: ["算法", "二分"]
category: 编程与技术
draft: false
---

## 整数二分：查找边界

在有序数组中查找元素 k 的**起始位置**和**终止位置**。

**左边界**（第一个 >= k 的位置）：`mid = l + r >> 1`，`a[mid] >= k` 时 `r = mid`，否则 `l = mid + 1`。

**右边界**（最后一个 <= k 的位置）：`mid = l + r + 1 >> 1`（避免死循环），`a[mid] <= k` 时 `l = mid`，否则 `r = mid - 1`。

```cpp
// 对应源码：range of number.cpp
// 左边界
int l = 0, r = n - 1;
while (l < r){
    int mid = l + r >> 1;
    if (a[mid] >= k) r = mid;
    else l = mid + 1;
}
// 右边界
l = 0, r = n - 1;
while (l < r){
    int mid = l + r + 1 >> 1;
    if (a[mid] <= k) l = mid;
    else r = mid - 1;
}
```

---

## 浮点数二分：三次方根

求 n 的三次方根，保留 6 位小数。

**思路**：在 `[-100, 100]` 上二分，`mid³ >= n` 则 `r = mid`，否则 `l = mid`。精度用 `r - l > 1e-8` 控制。

```cpp
// 对应源码：Cube root.cpp
double l = -100, r = 100;
while (r - l > 1e-8){
    double mid = (l + r) / 2;
    if (mid * mid * mid >= n) r = mid;
    else l = mid;
}
printf("%.6lf", l);
```
