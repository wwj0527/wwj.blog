# Mizuki 主题技术解析 · 大纲

> 原作者：matsuzaka-yuki | [GitHub](https://github.com/matsuzaka-yuki/Mizuki) | [演示站](https://mizuki.mysqil.com/)

---

## 文档列表（已完成）

所有文档位于 `docs/Mizuki技术解析/` 目录。

| 序号 | 文档名 | 内容概要 |
|------|--------|----------|
| 1 | [01-技术栈总览](Mizuki技术解析/01-技术栈总览.md) | 框架、语言、核心依赖一览 |
| 2 | [02-构建与渲染流程](Mizuki技术解析/02-构建与渲染流程.md) | 从源码到静态 HTML 的完整流程 |
| 3 | [03-Markdown与内容处理](Mizuki技术解析/03-Markdown与内容处理.md) | remark/rehype 插件链、数学公式、Mermaid、自定义组件 |
| 4 | [04-前端交互与体验](Mizuki技术解析/04-前端交互与体验.md) | Swup 页面切换、主题色、壁纸、音乐播放器等 |
| 5 | [05-配置与扩展体系](Mizuki技术解析/05-配置与扩展体系.md) | config.ts 结构、i18n、侧边栏、导航配置 |

---

## 一、01-技术栈总览.md

- 1.1 核心框架：Astro + Svelte
- 1.2 样式：Tailwind CSS 4、Stylus、CSS 变量
- 1.3 内容：Markdown、remark/rehype 生态
- 1.4 功能库：Swup、Expressive Code、Pagefind、PhotoSwipe 等
- 1.5 依赖关系简图

---

## 二、02-构建与渲染流程.md

- 2.1 构建命令解析（`pnpm build` 各步骤）
- 2.2 Astro 静态输出模式
- 2.3 页面路由与文件结构
- 2.4 资源处理（图片、字体、JS 分包）

---

## 三、03-Markdown与内容处理.md

- 3.1 remark 插件链（数学、Mermaid、自定义指令等）
- 3.2 rehype 插件链（KaTeX、表格、组件）
- 3.3 自定义 Markdown 组件（note、tip、github 卡片等）
- 3.4 内容集合（Content Collections）与 frontmatter

---

## 四、04-前端交互与体验.md

- 4.1 Swup 无刷新页面切换
- 4.2 主题色与暗色模式
- 4.3 壁纸模式（横幅/全屏）
- 4.4 音乐播放器（Meting/本地/Spotify）
- 4.5 Pagefind 站内搜索
- 4.6 相册与图片展示（PhotoSwipe、Fancybox）

---

## 五、05-配置与扩展体系.md

- 5.1 `config.ts` 模块划分
- 5.2 国际化（i18n）结构
- 5.3 侧边栏与导航配置
- 5.4 数据源（友链、时间线、技能、番剧等）
- 5.5 如何添加新页面/新功能

---

## 待你确认

1. 这个大纲是否符合你的预期？需要增删哪些部分？
2. 每篇文档的深度：偏「概念+用法」还是「源码级解析」？
3. 确认后我再按大纲逐篇写成完整 md。
