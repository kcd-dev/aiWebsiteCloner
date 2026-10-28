<div align="center">

# AI Website Cloner

把公开可访问的网页交给编程 Agent，重建成可编辑的 Next.js 项目。

它会按页面上的内容、资源和交互，在本模板里落地页面。

[![MIT](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)

</div>

---

## 这是什么

这是一个网站逆向模板。Next.js、shadcn/ui、Tailwind CSS v4 已经搭好。在支持的编程 Agent 里运行：

```text
/clone-website https://example.com
```

可以一次传入多个网址：`/clone-website <url1> [<url2> ...]`。

先按目标站 1:1 还原间距、颜色、字体和交互，再按你的要求改。克隆阶段使用页面上的真实文案和资源，不用占位图。

MIT 只许可本模板代码。被克隆页面的文案、图片、字体和商标仍归原权利人。只克隆你有权复制的站点，或仅在本地学习、对照。

本仓库基于 [JCodesMore/ai-website-cloner-template](https://github.com/JCodesMore/ai-website-cloner-template)（MIT）。版权与许可见 [LICENSE](./LICENSE)。

## 环境

- [Node.js](https://nodejs.org/) 24 及以上（见 `.nvmrc`）
- 一个带浏览器能力的编程 Agent

| Agent | 状态 |
| --- | --- |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | 推荐 |
| [Codex CLI](https://github.com/openai/codex) | 支持 |
| [OpenCode](https://opencode.ai/) | 支持 |
| [Cursor](https://cursor.com/) | 支持 |

## 快速开始

```bash
git clone git@github.com:kcd-dev/aiWebsiteCloner.git
cd aiWebsiteCloner
npm install
npm run check
npm run dev
```

`npm run dev` 启动开发服务器。`npm run check` 依次执行 lint、类型检查和生产构建。

## 克隆网站

在项目里对 Agent 说：

```text
/clone-website https://example.com
```

把网址换成要重建的站点。构建完成后，直接让 Agent 改你要动的部分。

流程固定四步：

1. **映射** — 把源站 URL 对应到本地路由，保留已有页面。
2. **观察** — 看桌面和移动端，提取真实资源与字体，并走一遍关键状态。
3. **实现** — 写成可编辑组件和可用交互。
4. **对照** — 按相同视口和状态比较源站与本地页，修可见差异，再跑生产检查。

技能正文在 `.agents/skills/clone-website/`。Codex、Cursor、OpenCode 直接读它。Claude Code 通过 `.claude/commands/clone-website.md` 调用同一套流程，不要在桥接文件里再写一份。

## 技术栈

- **Next.js 16**：App Router、React 19、TypeScript strict
- **shadcn/ui**：Base UI 原语，`cn()` 工具
- **Tailwind CSS v4**：oklch 设计令牌
- **Lucide React**：默认图标；克隆时会换成从源站提取的 SVG
- **部署**：面向 Vercel

## 命令

```bash
npm run dev        # 开发服务器
npm run build      # 生产构建
npm run start      # 启动生产服务
npm run lint       # ESLint
npm run typecheck  # TypeScript 检查
npm run check      # lint + typecheck + build
```

Docker：

```bash
docker compose up app --build   # 构建并运行
docker compose up dev --build   # 开发模式，端口 3001
```

## 代码约定

- TypeScript 严格模式，不用 `any`
- 具名导出；组件 PascalCase，工具函数 camelCase
- 样式用 Tailwind 或局部 CSS；只有动态值才写内联样式
- 缩进 2 空格，移动端优先

## 目录

```text
src/
  app/                 # Next.js 路由
  components/
    ui/                # shadcn/ui 基础组件
    sites/<site>/      # 某个源站的组件和提取出的 SVG
  lib/utils.ts         # cn()
  types/               # 类型
  hooks/               # 自定义 Hook
public/sites/<site>/   # 图片、字体、视频等资源
docs/
  research/<site>/     # 页面简报、资源映射、检查记录
  design-references/   # 截图
.agents/skills/clone-website/   # 克隆流程（唯一正文）
.claude/commands/clone-website.md
AGENTS.md              # Agent 说明
```

## 适用与边界

适用：把你拥有的站点从 WordPress、Webflow、Squarespace 迁到 Next.js；源码丢失后按线上页面找回可维护代码；对照真实站点学习布局和动效。

不要用于钓鱼、冒充他人品牌，或把别人的标志、品牌资源和原创文案当成自己的。源站服务条款禁止抓取或复刻时，先确认再做。

## 许可

[MIT](./LICENSE)。Copyright (c) 2025 JCodesMore。
