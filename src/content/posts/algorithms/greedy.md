---
title: 贪心与区间
published: 2026-03-06
description: 区间合并。
tags: ["算法", "贪心", "区间"]
category: 编程与技术
draft: false
---

## 区间合并

给定若干区间，合并所有有交集的区间，输出合并后的区间个数。

**思路**：按左端点排序，遍历区间。若当前区间与已合并区间无交集（`ed < item.first`），则保存已合并区间并开始新区间；否则扩展右端点 `ed = max(ed, item.second)`。

```cpp
// 对应源码：range_merge.cpp
void merge(vector<PII> &range){
    vector<PII> res;
    sort(range.begin(), range.end());
    int st = -2e9, ed = -2e9;
    for (auto item : range){
        if (ed < item.first){
            if (st != -2e9) res.push_back({st, ed});
            st = item.first;
            ed = item.second;
        } else {
            ed = max(ed, item.second);
        }
    }
    if (st != -2e9) res.push_back({st, ed});
    range = res;
}
```
