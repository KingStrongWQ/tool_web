# AGENTS.md

## 项目概述

`tool_web` 是一个纯静态的「小工具 + 小游戏」合集网站（品牌名 KingStrong），全部页面为**自包含单文件 HTML**，无构建工具、无包管理器、无外部依赖，直接双击或通过任意静态服务器打开即可运行。

- 入口页：`index.html`（工具/游戏卡片导航）
- 工具页：`timestamp-converter.html`（时间戳转换）、`unit-converter.html`（单位换算）、`compound-interest.html`（复利计算器）
- 小游戏：`aim-trainer.html`（FPS 打靶训练）、`minesweeper.html`（扫雷）、`sudoku.html`（数独）、`match-three.html`（消消乐）、`snake.html`（贪吃蛇）

## 技术规范

- 语言与编码：HTML/CSS/JS 均为纯原生实现，页面 `<html lang="zh-CN">`，文件编码 **UTF-8 无 BOM**，界面文案使用简体中文。
- 单文件结构：每个页面一个 `.html` 文件，CSS 内嵌于 `<style>`，JS 内嵌于 `<script>`，新增页面必须保持该模式，不要引入外部资源或拆分文件。
- 样式风格：主页采用「多彩卡片风」—— 纯白 `#fafafa` 背景，每张卡片使用独立柔和渐变配色 + 左上角大号 Emoji 图标 + 匹配色调的按钮。卡片悬停上浮 `6px` 并显示对应色调的彩色阴影。配色没有固定模板，每张卡片根据功能/游戏的主题风格特别设计，从配色到 Emoji 都要贴合内容气质。以下为当前已有卡片的配色方案，供参考和保持整体协调：

  | 卡片 | Emoji | Class | 渐变底色 | 按钮色 |
  |------|-------|-------|---------|--------|
  | 时间戳 | ⏰ | `.card-blue` | `#e0f2fe → #bae6fd` | `#3b82f6` |
  | 单位换算 | 📐 | `.card-green` | `#d1fae5 → #a7f3d0` | `#10b981` |
  | 复利计算 | 💰 | `.card-amber` | `#fef3c7 → #fde68a` | `#f59e0b` |
  | FPS 打靶 | 🎯 | `.card-red` | `#ffe4e6 → #fecdd3` | `#ef4444` |
  | 数独 | 🧩 | `.card-purple` | `#f3e8ff → #e9d5ff` | `#8b5cf6` |
  | 扫雷 | 💣 | `.card-slate` | `#f1f5f9 → #e2e8f0` | `#64748b` |
  | 消消乐 | 🍬 | `.card-pink` | `#fce7f3 → #fbcfe8` | `#ec4899` |
  | 贪吃蛇 | 🐍 | `.card-teal` | `#ccfbf1 → #99f6e4` | `#14b8a6` |

  卡片 HTML 结构模板：
  ```html
  <div class="tool-card card-xxx">
      <div class="tool-icon">📌</div>
      <h2>卡片标题</h2>
      <p>功能描述文字</p>
      <a href="path/to/page.html" class="tool-btn">使用工具</a>
  </div>
  ```

  子页面（工具/游戏详情页）仍然沿用各自独立的视觉风格，主页面与子页面无需统一。
- 返回主页：每个页面底部必须包含「返回主页」按钮（`.back-link` 样式），链接指向根目录 `index.html`；位于子目录的页面使用 `../index.html`，根目录页面使用 `index.html`。
- JS 风格：数独使用 ES6 `class` 封装；贪吃蛇等使用过程式 + `Canvas 2D`；事件监听用箭头函数；注释使用中文。
- 游戏实现：逻辑游戏（数独/扫雷/三消）用 DOM 渲染，动作游戏（贪吃蛇/下100层）用 Canvas；优先复用现有文件内的成熟逻辑模式。

## 提交与验证

- Git 提交信息使用中文，风格如「新增××」「修复××bug」「××优化」。
- 页面相互独立，改动一个页面后直接在浏览器中打开该 HTML 验证；涉及 `index.html` 的改动需核对卡片标题、描述与链接一致性。
- 新增工具或小游戏时，记得在 `index.html` 的工具网格中添加对应卡片（标题 + 描述 + 链接），保持 footer 版权信息为「© KingStrong」。

## 注意事项

- 项目无自动化测试与 lint 配置，不要新增构建系统或测试框架。
- 各页面无共享代码，改动时只影响目标文件；不要在页面间引入耦合。
- 文件必须以 UTF-8 无 BOM 保存，避免中文乱码。

## 目录结构

```
tool_web/
├── index.html                    # 入口导航页（多彩卡片风）
├── AGENTS.md
├── .git/
├── tools/                        # 工具类页面
│   ├── timestamp-converter.html  # 时间戳转换
│   ├── unit-converter.html       # 单位换算
│   └── compound-interest.html    # 复利计算器
└── games/                        # 游戏类页面
    ├── aim-trainer.html          # FPS 打靶训练
    ├── minesweeper.html          # 扫雷
    ├── sudoku.html               # 数独
    ├── match-three.html          # 消消乐
    └── snake.html                # 贪吃蛇
```