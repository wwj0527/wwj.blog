---
title: 图论与搜索
published: 2026-03-06
description: BFS 与 DFS 基础：迷宫最短路径、全排列。
tags: ["算法", "图论", "BFS", "DFS"]
category: 编程与技术
draft: false
---

## BFS：迷宫最短路径

在网格迷宫中，从起点到终点的最短步数。BFS 保证第一次到达终点时即为最短路径。

**思路**：用队列按层扩展，每次从队首取点，向四个方向探索，未访问且可走的点入队并更新距离。

```cpp
// 对应源码：maze(bfs).cpp
int bfs(){
    queue<PII> q;
    memset(d, -1, sizeof d);
    d[0][0] = 0;
    q.push({0, 0});
    int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, 1, 0, -1};
    
    while (!q.empty()){
        auto t = q.front();
        q.pop();
        for (int i = 0; i < 4; i ++ ){
            int x = t.first + dx[i], y = t.second + dy[i];
            if (x >= 0 && x < n && y >= 0 && y < m && g[x][y] == 0 && d[x][y] == -1){
                d[x][y] = d[t.first][t.second] + 1;
                q.push({x, y});
            }
        }
    }
    return d[n - 1][m - 1];
}
```

---

## DFS：全排列

输出 1～n 的全排列。

**思路**：递归枚举每一位填什么数，用 `st[]` 标记已用，回溯时恢复现场。

```cpp
// 对应源码：full permutation(dfs).cpp
void dfs(int x){
    if (x == n) {
        for (int i = 0; i < n; i ++ ) cout << path[i] << ' ';
        cout << endl;
    }
    for (int i = 1; i <= n; i ++){
        if (!st[i]){
            path[x] = i;
            st[i] = true;
            dfs(x + 1);
            st[i] = false;  // 恢复现场
        }
    }
}
```
