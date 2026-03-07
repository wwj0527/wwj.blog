---
title: 排序与分治
published: 2026-03-06
description: 快速排序、归并排序、快速选择、逆序对。
tags: ["算法", "排序", "分治"]
category: 编程与技术
draft: false
---

## 快速排序

选取基准（如中间元素），划分后递归左右两部分。

```cpp
// 对应源码：QuickSort.cpp
int partition(int q[], int low, int high){
    int i = low - 1, j = high + 1, pivot = q[(low + high) / 2];
    while (i < j){
        do i++; while (q[i] < pivot);
        do j--; while (q[j] > pivot);
        if (i < j) swap(q[i], q[j]);
    }
    return j;
}
void quick_sort(int q[], int low, int high){
    if (low >= high) return;
    int mid = partition(q, low, high);
    quick_sort(q, low, mid);
    quick_sort(q, mid + 1, high);
}
```

---

## 归并排序

分治：先递归左右，再合并两个有序区间。

```cpp
// 对应源码：MergeSort.cpp
void merge_sort(int q[], int low, int high){
    if (low >= high) return;
    int mid = low + high >> 1;
    merge_sort(q, low, mid);
    merge_sort(q, mid + 1, high);
    int i = low, j = mid + 1, k = 0;
    while (i <= mid && j <= high){
        if (q[i] <= q[j]) tmp[k++] = q[i++];
        else tmp[k++] = q[j++];
    }
    while (i <= mid) tmp[k++] = q[i++];
    while (j <= high) tmp[k++] = q[j++];
    for (i = low, j = 0; i <= high; i++, j++) q[i] = tmp[j];
}
```

---

## 快速选择

求第 k 小数，无需完整排序。划分后只在包含 k 的那一侧递归。

```cpp
// 对应源码：QuickSelect.cpp
int quick_select(int q[], int low, int high, int k){
    if (low == high) return q[low];
    int mid = partition(q, low, high);
    if (mid - low + 1 >= k) return quick_select(q, low, mid, k);
    else return quick_select(q, mid + 1, high, k - (mid - low + 1));
}
```

---

## 逆序对

利用归并排序，在合并时统计：当 `q[i] > q[j]` 时，左半部分 `[i, mid]` 都与 `q[j]` 构成逆序对，数量为 `mid - i + 1`。

```cpp
// 对应源码：InversePair.cpp
long long merge_sort(int q[], int low, int high){
    if (low >= high) return 0;
    int mid = low + high >> 1;
    long long res = merge_sort(q, low, mid) + merge_sort(q, mid + 1, high);
    // ... 合并过程 ...
    if (q[i] <= q[j]) tmp[k++] = q[i++];
    else {
        tmp[k++] = q[j++];
        res += mid - i + 1;
    }
    return res;
}
```
