# dsh-whale-avatar

给 DSH Web UI 的助手消息加上头像与名字：**App 图标 + 吃白饭的蓝色大肥鱼**。纯 CSS 注入（`::before`），React 重渲染不会丢，跟随日间/夜间主题令牌。

Adds an avatar (the app icon) and the name to every assistant message in the DSH Web UI. Pure CSS injection — survives React re-renders, theme-aware.

## 实现

- 目标元素：`[data-chat-flow-kind="assistant-step"]`（官方 web 应用的助手消息节点）。
- 注入方式：`style` 标签内一条 CSS 规则，`::before` 伪元素渲染「头像 + 名字」，无 DOM 改动。
- 头像：56px PNG 包进 28×28 SVG 的 data URI（Retina 清晰）。

## 安装

通过 Oh-DSH Desktop 插件市场安装（或 `dsh plugin --profile <name> add github:lhjlol/dsh-whale-avatar`）。安装后运行时自动重启生效。

## 卸载

从市场的插件列表卸载即可；CSS 随之移除。

## 结构

- `lib/client.js` — 浏览器半（`__ModuleLoader__` 格式），全部逻辑在此。
- `lib/index.mjs` — Node 半，空 apply（纯 client 插件）。
- `cordis.patch.yml` — bundle patch：向组合插入本插件行。
