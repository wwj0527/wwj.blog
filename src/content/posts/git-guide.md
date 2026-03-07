---
title: Git 常用命令详解
published: 2026-03-05
description: Git 是程序员必备的版本控制工具。本文详细讲解日常开发中每一步 Git 操作的含义、用法和常见场景。
tags: ["Git", "版本控制", "命令行"]
category: 编程与技术
draft: false
pinned: true
---

## 什么是 Git？

Git 是分布式版本控制系统，由 Linus Torvalds 在 2005 年创建。它可以记录代码的每次修改、支持多人协作、方便回滚和分支管理，是程序员日常开发的核心工具之一。

---

## 第一步：安装与基础配置

### 1.1 安装 Git

- **Windows**：从 [git-scm.com](https://git-scm.com/download/win) 下载安装包，按默认选项安装即可
- **macOS**：终端执行 `xcode-select --install`，或使用 `brew install git`
- **Linux**：`sudo apt install git`（Ubuntu）或 `sudo yum install git`（CentOS）

安装后，在终端输入 `git --version` 检查是否成功。

### 1.2 配置用户名和邮箱（首次使用必做）

Git 每次提交都会记录「谁」提交的，需要先配置身份：

```bash
# 设置全局用户名（会显示在提交记录里）
git config --global user.name "你的名字"

# 设置全局邮箱（建议用 GitHub 绑定的邮箱）
git config --global user.email "你的邮箱@example.com"
```

- `--global` 表示对所有项目生效；若只想对当前项目生效，去掉 `--global`
- 邮箱建议使用 GitHub/Gitee 账号绑定的邮箱，便于关联提交记录

### 1.3 查看当前配置

```bash
git config --list
```

会列出所有已配置项，包括 `user.name`、`user.email` 等。

---

## 第二步：创建或获取仓库

### 2.1 方式一：本地新建仓库

在项目文件夹内打开终端，执行：

```bash
git init
```

- 会在当前目录创建隐藏的 `.git` 文件夹，表示这里是一个 Git 仓库
- 之后就可以在这个目录里进行 `add`、`commit` 等操作

### 2.2 方式二：从远程克隆已有仓库

```bash
git clone https://github.com/用户名/仓库名.git
```

- 会下载整个仓库到当前目录，并自动创建同名文件夹
- 若想克隆到当前目录（不新建文件夹），在末尾加空格和 `.`：`git clone 地址 .`
- 克隆后会自动配置 `origin` 远程地址，可直接 `push`、`pull`

---

## 第三步：日常提交流程（add → commit → push）

### 3.1 查看当前状态

```bash
git status
```

会显示：
- **Untracked files**：新文件，尚未被 Git 跟踪
- **Changes not staged for commit**：已修改但未添加到暂存区
- **Changes to be committed**：已添加到暂存区，等待提交

建议每次操作前先 `git status`，确认当前状态。

### 3.2 添加文件到暂存区（Stage）

```bash
# 添加所有修改过的文件
git add .

# 只添加指定文件
git add src/index.ts
git add src/utils.ts

# 添加某个目录下的所有文件
git add src/
```

- `git add` 把文件放入「暂存区」，相当于「选中要提交的内容」
- 可以多次 `add`，最后一次性 `commit`
- 若误加了不想提交的文件，用 `git reset HEAD 文件名` 取消暂存

### 3.3 提交到本地仓库

```bash
git commit -m "提交说明"
```

- `-m` 后面是本次提交的说明，建议写清楚做了什么
- 提交只存在于本地，尚未推送到远程
- 好的提交信息示例：`"修复登录页面的样式错位"`、`"新增用户注册接口"`

### 3.4 推送到远程仓库

```bash
# 首次推送需要指定上游分支
git push -u origin main

# 之后直接推送即可
git push
```

- `origin` 是远程仓库的默认名称，`main` 是分支名（旧版可能是 `master`）
- `-u` 表示设置上游分支，之后 `git push`、`git pull` 可省略分支名
- 若推送失败，可能是远程有更新，需先 `git pull` 再 `git push`

---

## 第四步：拉取远程更新

### 4.1 拉取并合并远程最新代码

```bash
git pull
```

等价于 `git fetch` + `git merge`，即：先拉取远程更新，再合并到当前分支。

### 4.2 拉取指定分支

```bash
git pull origin main
```

从 `origin` 的 `main` 分支拉取并合并到当前分支。

### 4.3 若出现冲突

当本地和远程修改了同一处代码时，`git pull` 可能提示冲突。解决步骤：

1. 打开冲突文件，会看到 `<<<<<<<`、`=======`、`>>>>>>>` 标记
2. 手动编辑，保留需要的代码，删除冲突标记
3. 保存后执行：`git add 冲突文件`，再 `git commit -m "解决合并冲突"`
4. 最后 `git push`

---

## 第五步：分支操作

### 5.1 查看分支

```bash
# 查看本地分支，当前分支前有 * 号
git branch

# 查看所有分支（含远程）
git branch -a
```

### 5.2 创建新分支

```bash
# 创建分支但不切换
git branch 新分支名

# 创建并立即切换到新分支（常用）
git checkout -b 新分支名
```

### 5.3 切换分支

```bash
git checkout 分支名
```

切换前若有未提交的修改，Git 会提示先 `commit` 或 `stash`。

### 5.4 合并分支

```bash
# 先切换到要接收合并的目标分支（如 main）
git checkout main

# 合并指定分支到当前分支
git merge 新分支名
```

合并后，`新分支名` 的修改会并入 `main`，可再 `git push` 推送。

### 5.5 删除分支

```bash
# 删除本地分支（需先切换到其他分支）
git branch -d 分支名

# 强制删除
git branch -D 分支名
```

---

## 第六步：撤销与回退

### 6.1 撤销工作区的修改（未 add）

```bash
git checkout -- 文件名
```

- 将文件恢复为最后一次 `commit` 时的状态
- 未 `add` 的修改会全部丢失，慎用

### 6.2 取消暂存（已 add 未 commit）

```bash
git reset HEAD 文件名
```

- 把文件从暂存区移出，修改仍保留在工作区
- 之后可重新 `add` 或继续修改

### 6.3 回退提交（保留修改）

```bash
git reset --soft HEAD~1
```

- `HEAD~1` 表示上一个提交
- `--soft`：回退提交，但修改保留在暂存区，可重新 `commit`

### 6.4 回退提交（丢弃修改）

```bash
git reset --hard HEAD~1
```

- 回退到上一个提交，**工作区和暂存区的修改都会丢失**
- 仅用于确定要放弃当前修改时使用

---

## 第七步：远程仓库管理

### 7.1 查看远程仓库

```bash
git remote -v
```

会显示 `origin` 对应的 fetch 和 push 地址。

### 7.2 添加远程仓库

```bash
git remote add origin https://github.com/用户名/仓库名.git
```

- `origin` 是远程的默认名称，可自定义
- 本地 `git init` 后，需要先添加远程才能 `push`

### 7.3 修改远程地址

```bash
git remote set-url origin https://新地址
```

适用于更换 GitHub/Gitee 仓库、改用 SSH 等情况。

### 7.4 移除远程

```bash
git remote remove origin
```

---

## 完整流程示例：从零到推送

```bash
# 1. 进入项目目录
cd D:\my-project

# 2. 初始化仓库
git init

# 3. 配置身份（若已配置可跳过）
git config user.name "王伟捷"
git config user.email "wwj040527@gmail.com"

# 4. 添加所有文件
git add .

# 5. 首次提交
git commit -m "Initial commit: 项目初始化"

# 6. 设置主分支名为 main
git branch -M main

# 7. 添加远程仓库
git remote add origin https://github.com/wwj0527/my-repo.git

# 8. 推送到远程
git push -u origin main
```

---

## 日常更新流程

```bash
# 1. 拉取最新代码（避免冲突）
git pull

# 2. 修改文件后，添加并提交
git add .
git commit -m "更新：具体做了什么"

# 3. 推送到远程
git push
```

---

## 小贴士

- **提交信息**：尽量写清楚做了什么，方便以后回溯，如 `"修复登录 bug"` 而非 `"修改"`
- **频繁提交**：小步提交比一次大改更安全，出问题也容易回滚
- **分支开发**：新功能用新分支，合并前先 `pull` 最新代码
- **推送前先拉取**：`git pull` 再 `git push`，减少冲突
