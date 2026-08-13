# AGENTS.md

## 项目概述

`tool_web` 是一个纯静态的「小工具 + 小游戏」合集网站（品牌名 KingStrong），全部页面为**自包含单文件 HTML**，无构建工具、无包管理器、无外部依赖，直接双击或通过任意静态服务器打开即可运行。

- 入口页：`index.html`（工具/游戏卡片导航）
- 工具页：`timestamp-converter.html`（时间戳转换）、`unit-converter.html`（单位换算）、`work-timeline.html`（工作时间轴）
- 小游戏：`minesweeper.html`（扫雷）、`sudoku.html`（数独）、`match-three.html`（消消乐）、`snake.html`（贪吃蛇）、`100floors.html`（是男人就下100层）

## 技术规范

- 语言与编码：HTML/CSS/JS 均为纯原生实现，页面 `<html lang="zh-CN">`，文件编码 **UTF-8 无 BOM**，界面文案使用简体中文。
- 单文件结构：每个页面一个 `.html` 文件，CSS 内嵌于 `<style>`，JS 内嵌于 `<script>`，新增页面必须保持该模式，不要引入外部资源或拆分文件。
- 样式风格：沿用统一的视觉体系 —— `linear-gradient(135deg, #667eea 0%, #764ba2 100%)` 渐变背景/标题、白色圆角卡片 `.container`、`.section`/`.tool-card` 卡片、`backdrop-filter`、悬停上浮动画；新增页面应保持一致。
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

``
tool_web/
├── index.html          # 入口导航页
├── AGENTS.md
├── .git/
├── tools/              # 工具类页面
│   ├── timestamp-converter.html
│   ├── unit-converter.html
│   └── work-timeline.html
└── games/              # 游戏类页面
    ├── minesweeper.html
    ├── sudoku.html
    ├── match-three.html
    ├── snake.html
    └── 100floors.html
``