---
title: 字符串：KMP
published: 2026-03-06
description: KMP 字符串匹配算法，next 数组的求解与匹配过程。
tags: ["算法", "字符串", "KMP"]
category: 编程与技术
draft: false
---

## KMP 字符串匹配

在文本串 `s` 中查找模式串 `p` 的所有出现位置。

**核心**：`ne[i]` 表示模式串前 i 个字符中，最长相等前后缀的长度。匹配失败时，模式串指针 `j` 回退到 `ne[j]`，而不是从头开始。

**i 与 j 的关系**：`i` 是当前对比的文本位置，`j` 是已匹配的前缀长度。比较的是 `s[i]` 与 `p[j+1]`。

```cpp
// 对应源码：kmp.cpp
// 1. 求解 next 数组
for (int i = 2, j = 0; i <= n; i ++ ){
    while (j && p[i] != p[j + 1]) j = ne[j];
    if (p[i] == p[j + 1]) j ++ ;
    ne[i] = j;
}

// 2. KMP 匹配
for (int i = 1, j = 0; i <= m; i ++ ){
    while (j && s[i] != p[j + 1]) j = ne[j];
    if (s[i] == p[j + 1]) j ++ ;
    if (j == n){
        printf("%d ", i - n);  // 匹配成功，输出起始位置
        j = ne[j];
    }
}
```
