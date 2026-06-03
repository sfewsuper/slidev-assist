---
name: slidev-assist
description: "接受主题或任何原材料（研究报告、数据、文案、PPTX等），由AI解析后生成Markdown再调用Slidev输出可演示的HTML幻灯片"
metadata:
  kanji_name: "幻灯制作"
  emoji: "📽️"
---

# Slidev Assist

使用 [Slidev](https://sli.dev)（Presentation Slides for Developers）从 Markdown 生成 PPT。**你给任何原材料——一个主题、一份研究报告、一堆数据、一段文案、一个现成的PPTX——我来解析、提炼、结构化成 slides.md，一键生成可演示的 HTML 幻灯片。**

## 快速开始

```
# 给我任何原材料，我都能做成PPT：
- 一个主题：   "帮我做一个AI Agent入门的PPT"
- 研究报告：   "读了这份PDF，帮我提炼成10页PPT"
- 数据报表：   "这份Excel数据，做成汇报PPT"
- 文案稿件：   "这段文字帮我做成演示"
- 已有PPTX：   "这个PPTX帮我转成Slidev版"
```

我会自动：
1. **解析原材料** — 读文件、提取关键信息、结构化
2. **编写 `slides.md`** — 加入合适的布局和动效
3. **安装并启动 Slidev** — 浏览器预览
4. **导出** — PDF / PPTX / PNG

## 一页 Slide 的 Markdown 模板

```markdown
---
# 全局配置（headmatter）— 只有第一页前面可以写
theme: default
title: 标题
---

# 第一页标题

内容正文

---

# 第二页标题

更多内容
```

- `---` 分隔每一页
- 每页开头可加 `---` 包裹的 frontmatter 设置该页布局

## 常用 Frontmatter 配置

| 字段 | 示例 | 说明 |
|------|------|------|
| `theme` | `default` / `seriph` / `unocss` | 主题 |
| `layout` | `center` / `cover` / `two-cols` / `image-right` / `image-left` | 页面布局 |
| `background` | `/bg.png` | 背景图 |
| `class` | `text-white p-10` | UnoCSS 类 |
| `preload` | `false` | 预加载 |
| `transition` | `slide-left` / `fade` | 切换动画 |
| `colorSchema` | `light` / `dark` / `auto` | 配色方案 |
| `fonts` | `{ sans: "Inter", mono: "Fira Code" }` | 字体配置 |
| `lineNumbers` | `true` / `false` | 代码行号 |
| `title` | `"我的演示"` | 全局标题 |

### 常用布局说明

- `cover` — 封面页，适合大标题居中
- `center` — 内容居中
- `two-cols` — 左右两栏（用 `::right::` 分隔）
- `image-right` — 左文右图（需设 `image` 字段）
- `image-left` — 左图右文
- `section` — 章节过渡页
- `statement` — 引语/强调页
- `default` — 默认页，标题在左上角

## 语法特性

### 分隔内容
```markdown
---
layout: two-cols
---

# 左栏

左边内容

::right::

# 右栏

右边内容
```

### 代码高亮

````markdown
```ts {2-3}
function hello() {
  console.log('Hello')  // 第2-3行高亮
  console.log('Slidev')
}
```
````

### 代码行号
```markdown
```ts {*|1-2|3}{lines:true}
```
```

### 注释（演讲者备注）
```markdown
<!-- 这里写的不会显示在幻灯片上，只在演讲者模式可见 -->
```

### 图标
```
<carbon:logo-github />  — 使用 Iconify 任意图标
<carbon:book />
```

### 数学公式
```markdown
$E = mc^2$

$$
\frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$
```

### Mermaid 图表
```markdown
```mermaid
graph TD
    A[开始] --> B{判断}
    B -->|是| C[执行]
    B -->|否| D[结束]
```
```

### 内嵌 Vue 组件（高级）
```markdown
<Counter :start="5" />
<v-click> 点下一步才出现 </v-click>
<v-clicks> 每次点下一步出现一项 </v-clicks>
```

点击动画需要用 `v-click` / `v-clicks` 包裹。

## 完整示例（10页）

```markdown
---
theme: default
title: 我的演示
fonts:
  sans: Inter
---

# AI Agent 入门指南

从概念到实战 🚀

---

## 什么是 AI Agent？

- 能自主感知环境、做出决策并执行行动的智能实体
- 核心能力：推理、规划、工具调用、记忆

---

## 技术栈对比

| 特性 | 传统 AI | AI Agent |
|------|---------|----------|
| 交互方式 | 一问一答 | 自主执行 |
| 工具调用 | ❌ | ✅ |
| 长任务 | ❌ | ✅ |
| 记忆 | ❌ | ✅ |

---

## 总结

> AI Agent = 大模型 + 工具 + 记忆 + 规划
```

## 工作流程

1. **你**：提供原材料（主题/文件/数据/文案...）
2. **我**：解析原材料 → 提炼要点 → 结构化成 slides.md
3. **你**：确认/修改内容
4. **我**：自动运行 `npx @slidev/cli --remote` 启动预览
5. **你**：浏览器打开链接即可查看/演示

## 支持解析的原材料类型

| 原材料 | 解析方式 | 输出效果 |
|:-------|:---------|:---------|
| 💬 **主题/想法** | AI 直接构思内容大纲 | 完整 PPT |
| 📄 **PDF 研究报告** | 读文件 → 提取关键论点 → 结构化 | 要点清晰的演示 |
| 📊 **Excel 数据** | 读取数据表格 → 提炼结论 → 图表化 | 数据汇报 PPT |
| 📝 **文案稿件** | 分段 → 提炼小标题 → 配图建议 | 美化排版 |
| 🎞️ **PPTX 文件** | python-pptx 解析 → AI 重建 | 带动效的 Slidev 版 |
| 🔗 **网页链接** | 抓取内容 → 摘要 → 结构化 | 知识整理演示 |
| 📚 **多源混搭** | 综合以上多种方式 | 跨材料整合汇报 |

## 导出

```bash
# PDF
npx slidev export slides.md

# PPTX（实验性）
npx slidev export slides.md --format pptx

# PNG 图片
npx slidev export slides.md --format png
```

## 注意事项

- 首次运行会自动安装依赖，需要一些时间
- 预览默认在 `http://localhost:3030`
- 用 `--remote` 可以让手机上控制翻页
- 主题可以 npm 安装：`npm i slidev-theme-xxx`
- 文件类原材料需要你先上传/发给我，我来读取解析
