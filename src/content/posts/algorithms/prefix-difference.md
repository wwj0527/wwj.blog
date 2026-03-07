---
title: 前缀和与差分
published: 2026-03-06
description: 一维/二维前缀和、一维/二维差分、离散化区间和。
tags: ["算法", "前缀和", "差分", "离散化"]
category: 编程与技术
draft: false
---

## 一维前缀和

区间 `[l, r]` 的和：`s[r] - s[l-1]`，其中 `s[i] = a[1] + ... + a[i]`。

```cpp
// 对应源码：Prefix Sum.cpp
for (int i = 1; i <= n; i++) s[i] = q[i] + s[i-1];
// 查询 [l, r]
cout << s[r] - s[l-1] << endl;
```

---

## 二维前缀和

子矩阵 `(x1,y1)-(x2,y2)` 的和：

`s[x2][y2] - s[x2][y1-1] - s[x1-1][y2] + s[x1-1][y1-1]`

```cpp
// 对应源码：Submatrix.cpp
s[i][j] = a[i][j] + s[i-1][j] + s[i][j-1] - s[i-1][j-1];
// 查询
cout << s[x2][y2] - s[x2][y1-1] - s[x1-1][y2] + s[x1-1][y1-1] << endl;
```

---

## 一维差分

对 `[l, r]` 区间加 c：`d[l] += c`, `d[r+1] -= c`。差分数组的前缀和即为原数组。

```cpp
// 对应源码：Difference.cpp
void insert(int l, int r, int c){
    d[l] += c;
    d[r + 1] -= c;
}
```

---

## 二维差分

对子矩阵 `(x1,y1)-(x2,y2)` 加 c：

```cpp
// 对应源码：Difference matrix.cpp
void insert(int x1, int y1, int x2, int y2, int c){
    b[x1][y1] += c;
    b[x2+1][y1] -= c;
    b[x1][y2+1] -= c;
    b[x2+1][y2+1] += c;
}
```

---

## 离散化 + 区间和

坐标范围很大但实际用到的点很少时，将坐标映射到连续小区间。

```cpp
// 对应源码：range_sum.cpp
// 1. 收集所有用到的坐标，排序去重
sort(alls.begin(), alls.end());
alls.erase(unique(alls.begin(), alls.end()), alls.end());
// 2. 二分找映射位置
int find(int x) {
    int l = 0, r = alls.size() - 1;
    while (l < r) {
        int mid = l + r >> 1;
        if (alls[mid] >= x) r = mid;
        else l = mid + 1;
    }
    return r + 1;
}
// 3. 在映射后的下标上做前缀和
```
