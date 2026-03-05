# 我的自留地 · 博客

基于 [Mizuki](https://github.com/matsuzaka-yuki/mizuki) 主题的 Astro 静态博客，部署于野草云香港服务器。

---

## 一、技术栈与项目结构

### 1.1 技术栈

| 技术 | 用途 |
|------|------|
| **Astro** | 静态站点生成框架 |
| **Svelte** | 交互组件（如音乐播放器） |
| **Tailwind CSS** | 样式 |
| **TypeScript** | 类型安全 |
| **Markdown** | 文章内容 |
| **Pagefind** | 站内搜索 |
| **Nginx** | 服务器静态文件托管 |

### 1.2 构建输出

- **静态站点**：`pnpm build` 后生成 `dist/` 目录
- **无后端**：纯 HTML/CSS/JS，无需数据库、无需 Node 运行时

### 1.3 项目结构

```
Mizuki-master/
├── src/
│   ├── config.ts          # 站点核心配置（标题、横幅、音乐、侧边栏等）
│   ├── types/config.ts    # 配置类型定义
│   ├── content/           # 内容源
│   │   ├── posts/         # 文章（Markdown）
│   │   └── spec/          # 关于页等
│   ├── pages/             # 页面路由
│   │   ├── [...page].astro    # 首页
│   │   ├── posts/[...slug].astro  # 文章页
│   │   ├── tech.astro     # 技术分类
│   │   ├── archive.astro  # 归档
│   │   └── ...
│   ├── layouts/           # 布局
│   ├── components/        # 组件
│   ├── data/              # 友链、时间线、技能等数据
│   ├── i18n/              # 国际化
│   ├── utils/              # 工具函数
│   └── styles/            # 样式
├── public/                # 静态资源（直接复制到 dist）
│   └── assets/
├── dist/                  # 构建输出（由 Nginx 托管）
├── astro.config.mjs       # Astro 配置
└── package.json
```

---

## 二、本地与服务器的交互

### 2.1 整体流程

```
┌─────────────────┐     git push      ┌─────────────────┐
│   本地电脑       │ ───────────────► │   GitHub/Gitee   │
│  (编辑、构建)    │                   │   (代码仓库)     │
└─────────────────┘                   └────────┬────────┘
                                               │ git pull
                                               ▼
┌─────────────────┐     git pull       ┌─────────────────┐
│  野草云服务器    │ ◄────────────────  │   代码仓库       │
│  (香港 VPS)      │     pnpm build     │                 │
│  Nginx 托管 dist │                    └─────────────────┘
└─────────────────┘
        │
        │ 用户访问
        ▼
┌─────────────────┐
│  20040527.xyz   │
│  (访客浏览器)   │
└─────────────────┘
```

### 2.2 本地职责

- 编辑文章、修改配置
- 运行 `pnpm dev` 预览
- 运行 `pnpm build` 本地构建（可选，服务器也会构建）
- 通过 `git push` 把代码推送到 GitHub

### 2.3 服务器职责

- 从 GitHub 拉取最新代码
- 运行 `pnpm build` 生成 `dist/`
- Nginx 将 `dist/` 作为网站根目录对外提供

### 2.4 部署架构

| 角色 | 位置 | 说明 |
|------|------|------|
| 域名 | Spaceship | 20040527.xyz，DNS 解析到服务器 IP |
| 服务器 | 野草云香港 | Debian 12，Nginx + Node.js + pnpm |
| 代码仓库 | GitHub | wwj0527/wwj.blog |
| 网站根目录 | /www/wwwroot/20040527.xyz/dist | Nginx 指向此处 |

---

## 三、日常更新流程

### 3.1 本地修改并推送

```bash
# 1. 编辑文章或配置
# 2. 提交并推送
git add .
git commit -m "更新说明"
git push
```

### 3.2 服务器拉取并构建

```bash
# SSH 连接服务器
ssh -p 40449 root@38.207.178.103

# 进入项目目录
cd /www/wwwroot/20040527.xyz

# 拉取最新代码并构建
git pull
pnpm install   # 如有新依赖
pnpm build
```

构建完成后，Nginx 自动使用新的 `dist/` 内容，无需重启。

---

## 四、关键配置文件

| 文件 | 作用 |
|------|------|
| `src/config.ts` | 站点标题、URL、横幅、音乐、侧边栏、导航等 |
| `astro.config.mjs` | Astro 构建配置、插件 |
| `public/assets/` | Logo、横幅等静态资源 |

### 新增文章

在 `src/content/posts/` 下新建 `.md` 文件，或使用：

```bash
pnpm new-post
```

---

## 五、常用命令

| 命令 | 说明 |
|------|------|
| `pnpm dev` | 本地开发预览 |
| `pnpm build` | 构建静态站点到 dist |
| `pnpm preview` | 预览构建结果 |
| `pnpm new-post` | 新建文章 |

---

## 六、相关文档

- [迁移到野草云指南](docs/迁移到野草云指南.md) - 服务器部署步骤
- [新域名备案方案](docs/新域名备案方案.md) - 国内备案方案
- [域名转入腾讯云指南](docs/域名转入腾讯云指南.md) - 域名转移流程

---

## 七、学习要点

1. **静态站点**：构建时生成 HTML，运行时无需后端，适合 Nginx 直接托管。
2. **Git 工作流**：本地改代码 → 推送到 GitHub → 服务器拉取 → 构建 → 生效。
3. **配置驱动**：大部分修改集中在 `src/config.ts`，无需改组件代码。
4. **内容管理**：文章用 Markdown 写在 `src/content/posts/`，按 frontmatter 分类。
