---
title: Markdown 简单用法
published: 2026-03-04
description: Markdown 语法简单、专注内容，几分钟就能上手。本文简要总结博客写作最常用的几招，并附实例。
tags: ["Markdown", "博客", "写作"]
category: 编程与技术
draft: false
---

## 为什么用 Markdown 写博客？

Markdown 是 2004 年诞生的轻量级标记语言，用少量符号代替复杂排版，语法简单、兼容性强，几乎所有博客平台都支持。写博客用它，可以专注内容，不用反复调格式，文本也干净好迁移。

## 最常用的几招（附实例）

### 标题

`#` 数量越多，级别越低（最多 6 级）：

```markdown
# 一级标题
## 二级标题
### 三级标题
```

效果：

# 一级标题
## 二级标题
### 三级标题

### 文本格式

```markdown
**加粗**  *斜体*  ***加粗+斜体***  ~~删除线~~
```

效果：**加粗** *斜体* ***加粗+斜体*** ~~删除线~~

### 列表

无序用 `-`，有序用 `1.`，子项缩进：

```markdown
- 列表项1
- 列表项2
  1. 子步骤
```

效果：

- 列表项1
- 列表项2
  1. 子步骤

### 链接与图片

```markdown
[显示文字](https://example.com)

和链接类似，只是前面多了个 !
格式：![图片alt文字](图片地址 "可选标题")
![图片说明](图片地址)
```

效果：[点击访问示例链接](https://www.bilibili.com/bangumi/play/ss38958?spm_id_from=333.337.0.0)（悬停可看标题）

### 引用

```markdown

换行加 > 即可
> 生活就像海洋，只有意志坚强的人才能到达彼岸。
>
> this is an apple, i like apples, apples are good for our health.
```

效果：

> 生活就像海洋，只有意志坚强的人才能到达彼岸。
>
> this is an apple, i like apples, apples are good for our health.

### 代码块

三个反引号包裹，可加语言名做高亮。若要显示反引号本身，用更多反引号包裹：

````
```python
def hello():
    print("Hello, Markdown!")
```
````


效果（带语法高亮）：
```python
def hello():
    print("Hello, Markdown!")
```

掌握这些，日常写博客就够用了。更复杂的表格、脚注等，用到再查就行。
