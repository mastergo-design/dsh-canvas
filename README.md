# MasterGo Canvas for DeepSeek Harness

[![npm version](https://img.shields.io/npm/v/@mastergo/dsh-canvas.svg)](https://www.npmjs.com/package/@mastergo/dsh-canvas)
[![DeepSeek Harness plugin](https://img.shields.io/badge/DeepSeek%20Harness-plugin-4f46e5)](https://github.com/topics/dsh-plugin)

## 中文

`@mastergo/dsh-canvas` 将 DeepSeek Harness 连接到同一台电脑上打开的
MasterGo Web 画布。插件包内包含 DSH 专用的 `mgmcp-dsh`，不要求用户安装
MasterGo 客户端，也不需要手动下载二进制或配置端口。

### 当前版本能力

- 读取当前选中的画布节点、节点截图和前端代码。
- 查询 MasterGo 组件库、组件详情、素材、变量和字体。
- 基于设计要求生成页面方案并提交内联 HTML 到画布。
- 创建组件，更新、替换或删除节点，更新或删除变量。
- 对生成结果进行检查，并获取设计差异。
- 检查本地 Canvas MCP 运行状态。
- 支持 macOS、Windows 和 Linux，以及 x64、arm64 架构。

### 安装

需要 Node.js 22.19 或更高版本。

```bash
corepack enable
npx @deepseek-ai/dsh plugin --profile web add @mastergo/dsh-canvas
npx @deepseek-ai/dsh web
```

安装后，在同一台电脑上打开目标 MasterGo Web 文件。只有需要读取或修改
当前选择内容时才需要预先选中节点；提交新页面内容通常不要求先选中节点。

升级或卸载：

```bash
npx @deepseek-ai/dsh plugin --profile web update @mastergo/dsh-canvas
npx @deepseek-ai/dsh plugin --profile web remove @mastergo/dsh-canvas
```

DSH 的插件列表只显示已经安装到本机的 Bundle；当前不是从社区页面搜索后
直接安装的应用商店模式。

### 使用方法

日常使用只需要三步：

1. 在同一台电脑上打开目标 MasterGo Web 文件。
2. 如果任务针对现有内容，先在画布中选中对应节点；创建新内容时可以不选。
3. 在 Harness 会话中直接说明目标、限制和是否允许修改。

不需要记住插件名或工具名。下面这些话可以直接使用。

#### 确认当前文件是否可操作

> 我已经在这台电脑上打开了 MasterGo 文件。先确认你能否读取当前画布；
> 如果不能，请告诉我需要打开或刷新什么。

这个请求不要求预先选中节点。它适合放在新会话的第一句话。

#### 理解当前选中的设计

先在 MasterGo 中选中页面、Frame 或一组节点，然后说：

> 我选中了订单详情页。请读取它，按照页面层级、布局、间距、颜色、字体和
> 组件复用情况做一份总结。先分析，不要修改画布。

#### 检查视觉和规范问题

> 检查我选中区域的对齐、间距、字号层级和颜色使用，列出明显问题并给出
> 修改建议。先不要改，等我确认。

如果希望检查结果带上画面依据，可以补一句：“同时截取当前选中区域供我核对。”

#### 查询可以复用的组件和样式

> 查看当前文件可用的组件库、颜色变量、字号和字体。我要搭建一个 B2B
> 表单页，请告诉我应该优先复用哪些内容，并说明原因。

这个场景通常不要求预先选中节点。

#### 在画布中创建新页面

> 在当前画布中做一个 1440 像素宽的 B2B 数据看板，包含顶部导航、四张
> 指标卡、趋势图区域和订单表格。使用浅色背景、8 像素间距体系，并优先
> 复用当前文件已有的组件和变量。先说明页面结构，再创建到画布中。

把页面用途、尺寸、必须包含的区域、视觉要求和复用要求写清楚，结果会更稳定。

#### 修改当前选中的内容

先选中需要修改的节点，然后说：

> 我已经选中顶部导航。保持整体尺寸和现有文案不变，增强当前菜单项的状态，
> 统一左右间距，并让操作按钮更突出。完成后告诉我改了哪些内容。

如果只想先看方案，请明确补充“先给修改方案，不要直接改画布”。

#### 获取前端实现参考

> 读取我选中的区域，整理一份 React 实现参考。说明主要布局、组件拆分、
> 样式变量和响应式注意点，不需要修改画布。

#### 复查刚完成的结果

> 检查刚刚完成的页面是否满足前面的要求，重点看层级、间距、组件复用和
> 视觉一致性。先列出差异；明确的小问题可以直接修复，涉及内容取舍时先问我。

一个完整的实际流程可以是：打开文件并确认连接 → 选中旧页面让其先分析 →
确认修改方向 → 执行修改 → 再做一次截图和差异检查。

### 开发者参考：底层能力范围

普通用户不需要使用下面的名称。它们用于排查兼容性或确认当前版本边界。

| 范围 | 工具 |
| --- | --- |
| 指引与版本 | `get_guidelines`、`get_version` |
| 页面设计与提交 | `design_page`、`submit_page_to_canvas`、`agent_create_component` |
| 组件库与设计系统 | `get_library_list`、`get_component_info`、`get_component_catalog`、`get_component_details`、`get_library_assets`、`get_variables`、`get_fonts` |
| 读取与检查 | `get_selection_node`、`get_frontend_code`、`get_screenshot`、`review_generated_page`、`get_design_diff` |
| 画布编辑 | `agent_update_node`、`agent_replace_node`、`agent_remove_node`、`agent_update_variables`、`agent_remove_variable` |

其中 `submit_page_to_canvas` 只接受 `code` 参数中的内联 HTML，
不读取本地 HTML 文件路径。

### 本地运行方式

首次使用时，插件会检查本地 Canvas 服务。MasterGo 客户端已经启动兼容服务时
直接复用；没有兼容服务时，插件会校验、安装并启动当前平台对应的
`mgmcp-dsh`。

- 复用 MasterGo 客户端的 protocol 10+ 标准 `mgmcp`，兼容客户端与 DSH
  同时运行的场景。
- 两种实例同时存在时，每次画布操作前都会重新发现本机运行时：优先选择已经
  连接画布的实例；都未连接时优先选择客户端实例。
- 端口只用于发现，不用于判断实例身份；端口被占用或自动变化无需用户配置。
- 明确返回“没有在线画布”时，只读操作会安全切换实例并重试一次；写操作只
  刷新路由，不自动重放，避免重复修改。
- 插件自行管理的 `mgmcp-dsh` 仍要求 protocol 11+ 和本地访问密钥。
- 插件不会停止、替换或升级 MasterGo 客户端启动的 `mgmcp`。
- 多个 DSH 进程同时启动时，通过启动锁避免重复拉起 Sidecar。
- Harness 退出后，`mgmcp-dsh` 会保留运行，供后续 DSH 进程复用。
- Sidecar 启动失败只会停用 Canvas 工具，不影响其他 Harness 能力。

普通用户不需要配置二进制路径、本地 URL 或端口。

### 状态检查与排障

`mastergo_canvas_status` 会实时报告当前选中的运行时、实际端口、版本和画布
连接状态，并明确区分 MasterGo 客户端实例与 DSH 管理的实例。

- **插件列表中没有显示：** 重新执行安装命令，然后重启 web profile。
- **Canvas 状态不可用：** 升级或重新安装插件，确保二进制与当前平台匹配。
- **提示没有活动画布：** 在同一台电脑上打开或刷新目标 MasterGo Web 文件。
- **选择内容为空：** 在 MasterGo 中选中目标节点后，再执行依赖当前选择的操作。

安全问题请先阅读 [SECURITY.md](./SECURITY.md)，不要在公开 Issue 中提交
Token、私有文档内容或企业数据。

### 社区与支持

- npm：[查看 `@mastergo/dsh-canvas`](https://www.npmjs.com/package/@mastergo/dsh-canvas)
- 社区发布：[DeepSeek Harness — Show Your Plugins!](https://github.com/deepseek-ai/deepseek-harness/discussions/4762)
- 反馈：[GitHub Issues](https://github.com/mastergo-design/dsh-canvas/issues)
- 更新记录：[CHANGELOG.md](./CHANGELOG.md)
- DeepSeek Harness：[官方仓库](https://github.com/deepseek-ai/deepseek-harness)

---

## English

`@mastergo/dsh-canvas` connects DeepSeek Harness to a MasterGo Web canvas open
on the same computer. The package includes and manages a DSH-specific
`mgmcp-dsh`; users do not need the MasterGo desktop client, a separate binary
download, or manual port configuration.

### Capabilities in this release

- Read selected canvas nodes, screenshots, and frontend code.
- Inspect MasterGo libraries, component details, assets, variables, and fonts.
- Produce page designs and submit inline HTML to the canvas.
- Create components; update, replace, or remove nodes; and update or remove
  variables.
- Review generated results and inspect design differences.
- Check the local Canvas MCP runtime status.
- Run on macOS, Windows, and Linux on x64 and arm64.

### Install

Node.js 22.19 or newer is required.

```bash
corepack enable
npx @deepseek-ai/dsh plugin --profile web add @mastergo/dsh-canvas
npx @deepseek-ai/dsh web
```

After installation, open the target MasterGo Web file on the same computer.
Preselect nodes only for operations that should read or modify the current
selection. Submitting new page content normally does not require a selection.

Update or remove the Bundle through the same profile:

```bash
npx @deepseek-ai/dsh plugin --profile web update @mastergo/dsh-canvas
npx @deepseek-ai/dsh plugin --profile web remove @mastergo/dsh-canvas
```

The DSH plugin list shows Bundles already installed on the local machine. It is
not currently an app-store flow that installs directly from a community search.

### Usage

Day-to-day use takes three steps:

1. Open the target MasterGo Web file on the same computer.
2. If the task concerns existing content, select the relevant nodes in MasterGo.
   Leave the selection empty when creating new content.
3. In the Harness conversation, state the goal, constraints, and whether changes
   may be applied immediately.

You do not need to remember a plugin or tool name. The following prompts can be
used directly.

#### Confirm that the current file is reachable

> I have opened the MasterGo file on this computer. First confirm whether you can
> read the current canvas. If not, tell me what I need to open or refresh.

No selection is required. This is a useful first message in a new conversation.

#### Understand the selected design

Select a page, frame, or group of nodes in MasterGo, then say:

> I selected the order-details page. Summarize its hierarchy, layout, spacing,
> colors, typography, and component reuse. Analyze it first and do not change the
> canvas.

#### Check visual and design-system issues

> Check the selected area for alignment, spacing, type hierarchy, and color usage.
> List clear issues and suggest fixes, but wait for my confirmation before editing.

Add “capture the selected area so I can verify the findings” when a screenshot is
useful.

#### Find reusable components and styles

> Inspect the libraries, color variables, type styles, and fonts available in this
> file. I am building a B2B form page; tell me what I should reuse and why.

This usually does not require a selection.

#### Create a new page on the canvas

> Create a 1440-pixel-wide B2B analytics dashboard on the current canvas. Include
> a top navigation bar, four metric cards, a trend area, and an orders table. Use a
> light background and an 8-pixel spacing system, and reuse existing components and
> variables where possible. Explain the structure first, then create it.

Results are more predictable when the request states the purpose, size, required
sections, visual constraints, and reuse expectations.

#### Modify the current selection

Select the nodes to change, then say:

> I selected the top navigation. Keep its overall size and copy, strengthen the
> active-item state, make the horizontal spacing consistent, and give the action
> button more emphasis. Tell me what changed when you finish.

Add “propose the changes first; do not edit the canvas yet” when you want approval
before execution.

#### Get frontend implementation guidance

> Read the selected area and prepare a React implementation reference. Explain the
> main layout, component breakdown, style variables, and responsive considerations.
> Do not change the canvas.

#### Review the completed result

> Check whether the page we just completed meets the earlier requirements. Focus
> on hierarchy, spacing, component reuse, and visual consistency. List differences
> first. Fix unambiguous small issues, but ask me before making content tradeoffs.

A practical end-to-end flow is: open the file and confirm access → select an old
page and ask for analysis → approve a direction → apply the change → run a final
screenshot and difference review.

### Developer reference: underlying capability scope

Regular users do not need the names below. They are provided for compatibility
debugging and for confirming the current release boundary.

| Area | Tools |
| --- | --- |
| Guidance and version | `get_guidelines`, `get_version` |
| Design and submission | `design_page`, `submit_page_to_canvas`, `agent_create_component` |
| Libraries and design system | `get_library_list`, `get_component_info`, `get_component_catalog`, `get_component_details`, `get_library_assets`, `get_variables`, `get_fonts` |
| Read and review | `get_selection_node`, `get_frontend_code`, `get_screenshot`, `review_generated_page`, `get_design_diff` |
| Canvas edits | `agent_update_node`, `agent_replace_node`, `agent_remove_node`, `agent_update_variables`, `agent_remove_variable` |

`submit_page_to_canvas` accepts inline HTML through its `code`
argument and does not read a local HTML file path.

### Local runtime behavior

On first use, the Bundle checks for a compatible local Canvas service. It reuses
one already started by MasterGo Client; otherwise it verifies, installs, and
starts the packaged `mgmcp-dsh` for the current platform.

- A protocol 10+ standard `mgmcp` started by MasterGo Client is reused so the
  client and DSH can run together.
- When client and DSH runtimes coexist, the Bundle rediscovers them before canvas
  operations and follows the runtime that already owns an online canvas. If
  neither is connected, the client runtime wins.
- Ports are discovery inputs rather than runtime identities, so automatic port
  changes require no user configuration.
- A definitive no-online-canvas response safely retries read-only operations once
  on another runtime. Mutations only refresh routing and are never replayed.
- A plugin-managed `mgmcp-dsh` still requires protocol 11+ and a local access key.
- The Bundle never stops, replaces, or upgrades the `mgmcp` process owned by
  MasterGo Client.
- A startup lock prevents concurrent DSH processes from launching duplicate
  sidecars.
- `mgmcp-dsh` remains running after Harness exits so later DSH processes can
  reuse it.
- A sidecar startup failure disables Canvas tools without disabling unrelated
  Harness capabilities.

Normal users do not configure a binary path, local URL, or port.

### Status and troubleshooting

`mastergo_canvas_status` reports the selected runtime, actual endpoint, version,
and live canvas connection state, and distinguishes MasterGo Client from the
DSH-managed runtime.

- **The Bundle is not listed:** run the install command again and restart the
  web profile.
- **Canvas status is unavailable:** update or reinstall the Bundle so its binary
  matches the current platform.
- **No active canvas/document:** open or refresh the target MasterGo Web file on
  the same computer.
- **Selection is empty:** select the intended nodes in MasterGo before running a
  selection-based operation.

See [SECURITY.md](./SECURITY.md) before reporting a vulnerability. Do not put
tokens, private document contents, or enterprise data in a public issue.

### Community and support

- Package: [npm — `@mastergo/dsh-canvas`](https://www.npmjs.com/package/@mastergo/dsh-canvas)
- Community post: [DeepSeek Harness — Show Your Plugins!](https://github.com/deepseek-ai/deepseek-harness/discussions/4762)
- Issues: [GitHub Issues](https://github.com/mastergo-design/dsh-canvas/issues)
- Changes: [CHANGELOG.md](./CHANGELOG.md)
- DeepSeek Harness: [official repository](https://github.com/deepseek-ai/deepseek-harness)

This repository is the public documentation, release-information, and support
home for the package. Internal build infrastructure and private development
history are intentionally not mirrored here.
