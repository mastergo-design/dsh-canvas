# MasterGo Canvas for DeepSeek Harness

[English](./README.md)

`@mastergo/dsh-canvas` 将 DeepSeek Harness 连接到当前打开的 MasterGo Web
画布。插件自带并管理 DSH 专用 MCP 二进制，用户不需要额外安装 MasterGo
客户端或手动下载 MCP 服务。

## 安装

DeepSeek Harness 与本插件要求 Node.js 22.19 或更高版本。

```bash
corepack enable
npx @deepseek-ai/dsh plugin --profile web add @mastergo/dsh-canvas
npx @deepseek-ai/dsh web
```

在同一台电脑上打开一个 MasterGo 设计文件，并选中希望操作的画布内容，
随后即可让 Agent 检查 Canvas 连接并调用插件提供的 MasterGo 工具。

升级或卸载：

```bash
npx @deepseek-ai/dsh plugin --profile web update @mastergo/dsh-canvas
npx @deepseek-ai/dsh plugin --profile web remove @mastergo/dsh-canvas
```

## 能力

- 在 DeepSeek Harness 中使用 MasterGo Canvas MCP 工具。
- 自动完成独立 `mgmcp-dsh` 的安装、校验、启动、复用和生命周期管理。
- 支持 macOS、Windows、Linux，以及 x64、arm64 架构。
- Canvas 连接失败时只降级画布能力，不影响其他 Harness 插件。
- 可将原图和分离后的图片图层导入同一个紧凑、可编辑的 MasterGo 画布区块。

插件默认使用用户在 Harness 中选择的模型。可选的 MasterGo 模型 Provider
默认关闭，Canvas MCP 不依赖它。

## 开箱即用

npm 包已经包含全部受支持平台的 DSH 专用 `mgmcp-dsh`。首次使用时，插件
会选择当前平台对应的二进制、校验发布摘要、安装到用户应用数据目录，并启动
或复用兼容的 DSH 进程。

MasterGo 客户端原有启动方式仍然兼容，但不再是插件运行的前置条件。

## 安全与数据边界

- `mgmcp-dsh` 使用自动生成的本地访问密钥和仅回环地址传输。
- Sidecar 校验 MasterGo 与本地回环 Origin。
- 本地路径能力限制在当前 Harness workspace 内，并防止符号链接越界。
- 远程图片导入拒绝重定向以及私有、保留网段目标。
- 画布通信发生在本地；模型可见上下文由用户在 Harness 中选择的 Provider 处理。
- 导入画布本身不扣减 MasterGo 积分；单独启用的 MasterGo 模型 Provider 可能
  适用其自身计费规则。

安全问题请先阅读 [SECURITY.md](./SECURITY.md)，不要在公开 Issue 中提交漏洞
细节、Token、文档内容或企业数据。

## 兼容性与反馈

DeepSeek Harness 当前仍处于 Developer Preview，插件 API 可能发生不兼容变化。
提交兼容性问题时，请提供 Harness 版本、插件版本、操作系统和 CPU 架构，以及
去除凭证和私有文档数据后的 Canvas 状态信息。

- npm：[查看 `@mastergo/dsh-canvas`](https://www.npmjs.com/package/@mastergo/dsh-canvas)
- 社区发布：[DeepSeek Harness — Show Your Plugins!](https://github.com/deepseek-ai/deepseek-harness/discussions/4762)
- 反馈：[GitHub Issues](https://github.com/mastergo-design/dsh-canvas/issues)
- 更新记录：[CHANGELOG.md](./CHANGELOG.md)
- DeepSeek Harness：[官方仓库](https://github.com/deepseek-ai/deepseek-harness)

本仓库是插件的公开文档、版本信息与支持入口，不镜像内部构建基础设施和私有
开发历史。
