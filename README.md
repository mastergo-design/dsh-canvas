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

在 Harness 会话中直接用自然语言描述操作，例如：

- “检查 MasterGo Canvas 是否已经连接。”
- “读取我在 MasterGo 中选中的节点，总结它们的结构。”
- “截取当前选中内容的画布截图。”
- “按照这些要求修改当前选中的节点：……”
- “把下面这段 HTML 提交到 MasterGo 画布：……”

通常不需要手动输入工具名。Harness 中显示的工具名可能带有
`mcp__mastergo_canvas__` 前缀。

### Canvas MCP 工具范围

| 范围 | 工具 |
| --- | --- |
| 指引与版本 | `get_guidelines`、`get_version` |
| 页面设计与提交 | `design_page`、`submit_page_to_canvas`、`agent_create_component` |
| 组件库与设计系统 | `get_library_list`、`get_component_info`、`get_component_catalog`、`get_component_details`、`get_library_assets`、`get_variables`、`get_fonts` |
| 读取与检查 | `get_selection_node`、`get_frontend_code`、`get_screenshot`、`review_generated_page`、`get_design_diff` |
| 画布编辑 | `agent_update_node`、`agent_replace_node`、`agent_remove_node`、`agent_update_variables`、`agent_remove_variable` |

本 Bundle 中的 `submit_page_to_canvas` 只接受 `code` 参数中的内联 HTML，
不读取本地 HTML 文件路径。

### 本地运行方式

首次使用时，插件会校验当前平台对应的 `mgmcp-dsh`，安装到带版本号的用户
数据目录，并在没有兼容 DSH 进程时自动启动。

- 只会复用兼容的 `mgmcp-dsh`。
- MasterGo 客户端启动的标准 `mgmcp` 不会被本插件复用、停止或替换。
- 多个 DSH 进程同时启动时，通过启动锁避免重复拉起 Sidecar。
- Harness 退出后，`mgmcp-dsh` 会保留运行，供后续 DSH 进程复用。
- Sidecar 启动失败只会停用 Canvas 工具，不影响其他 Harness 能力。

普通用户不需要配置二进制路径、本地 URL 或端口。

### 状态检查与排障

`mastergo_canvas_status` 只检查本地 `mgmcp-dsh` 是否就绪，以及它由当前插件
启动还是由其他 DSH 进程复用；它不能证明某个 MasterGo 文件或节点已经连接。

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

Describe the operation in normal language in a Harness conversation, for example:

- “Check whether MasterGo Canvas is connected.”
- “Read the nodes I selected in MasterGo and summarize their structure.”
- “Capture a screenshot of my current MasterGo selection.”
- “Update the selected node using these requirements: …”
- “Submit this inline HTML to the MasterGo canvas: …”

Users normally do not need to type tool names. Harness may display them with an
MCP server prefix such as `mcp__mastergo_canvas__`.

### Canvas MCP tool scope

| Area | Tools |
| --- | --- |
| Guidance and version | `get_guidelines`, `get_version` |
| Design and submission | `design_page`, `submit_page_to_canvas`, `agent_create_component` |
| Libraries and design system | `get_library_list`, `get_component_info`, `get_component_catalog`, `get_component_details`, `get_library_assets`, `get_variables`, `get_fonts` |
| Read and review | `get_selection_node`, `get_frontend_code`, `get_screenshot`, `review_generated_page`, `get_design_diff` |
| Canvas edits | `agent_update_node`, `agent_replace_node`, `agent_remove_node`, `agent_update_variables`, `agent_remove_variable` |

In this Bundle, `submit_page_to_canvas` accepts inline HTML through its `code`
argument and does not read a local HTML file path.

### Local runtime behavior

On first use, the Bundle verifies the `mgmcp-dsh` binary for the current target,
installs it into a versioned per-user data directory, and starts it when no
compatible DSH runtime is available.

- Only a compatible `mgmcp-dsh` process is reused.
- A standard `mgmcp` process started by the MasterGo client is not reused,
  stopped, or replaced by this Bundle.
- A startup lock prevents concurrent DSH processes from launching duplicate
  sidecars.
- `mgmcp-dsh` remains running after Harness exits so later DSH processes can
  reuse it.
- A sidecar startup failure disables Canvas tools without disabling unrelated
  Harness capabilities.

Normal users do not configure a binary path, local URL, or port.

### Status and troubleshooting

`mastergo_canvas_status` reports whether the local `mgmcp-dsh` runtime is ready
and whether this plugin started it or reused another DSH process. It does not
prove that a particular MasterGo file or node is connected.

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
