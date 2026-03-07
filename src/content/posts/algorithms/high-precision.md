---
title: 高精度运算
published: 2026-03-06
description: 大整数加减乘除，用 vector 逆序存储每一位。
tags: ["算法", "高精度"]
category: 编程与技术
draft: false
---

大整数超出 `long long` 范围时，用 `vector<int>` 逆序存每一位（个位在前）。

---

## 高精度加法

从低位到高位逐位相加，处理进位。

```cpp
// 对应源码：HighAccuracy+.cpp
vector<int> Add(vector<int> &A, vector<int> &B){
    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size() || i < B.size(); i++){
        if (i < A.size()) t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }
    if (t) C.push_back(1);
    return C;
}
```

---

## 高精度减法

先比较大小保证 `A >= B`，从低位逐位相减，借位用 `t` 记录。

```cpp
// 对应源码：HighAccuracy-.cpp
vector<int> sub(vector<int> &A, vector<int> &B){
    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i++){
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        t = (t < 0) ? 1 : 0;
    }
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}
```

---

## 高精度乘法（大数 × 小数）

`A` 的每一位乘以 `b`，加上进位。

```cpp
// 对应源码：HighAccuracymultiplication.cpp
vector<int> mul(vector<int> &A, int b){
    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i++){
        t = A[i] * b + t;
        C.push_back(t % 10);
        t /= 10;
    }
    if (t) C.push_back(t);
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}
```

---

## 高精度除法（大数 ÷ 小数）

从高位到低位除，余数传给下一位。

```cpp
// 对应源码：HighAccuracyDivision.cpp
vector<int> div(vector<int> A, int b, int &r){
    vector<int> C;
    r = 0;
    for (int i = A.size() - 1; i >= 0; i--){
        r = r * 10 + A[i];
        C.push_back(r / b);
        r %= b;
    }
    reverse(C.begin(), C.end());
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}
```
