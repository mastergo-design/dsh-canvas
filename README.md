# MasterGo Canvas for DeepSeek Harness

[简体中文](./README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@mastergo/dsh-canvas.svg)](https://www.npmjs.com/package/@mastergo/dsh-canvas)
[![DeepSeek Harness plugin](https://img.shields.io/badge/DeepSeek%20Harness-plugin-4f46e5)](https://github.com/topics/dsh-plugin)

`@mastergo/dsh-canvas` connects DeepSeek Harness to a live MasterGo Web canvas.
It packages and manages its own DSH-specific MCP sidecar, so users do not need
to install the MasterGo desktop client or a separate MCP binary.

## Install

DeepSeek Harness and this bundle require Node.js 22.19 or newer.

```bash
corepack enable
npx @deepseek-ai/dsh plugin --profile web add @mastergo/dsh-canvas
npx @deepseek-ai/dsh web
```

Open a MasterGo design file in the same desktop session and select the canvas
content you want to work with. The agent can then check the Canvas connection
and use the MasterGo tools exposed by the bundle.

Update or remove the bundle through the same profile:

```bash
npx @deepseek-ai/dsh plugin --profile web update @mastergo/dsh-canvas
npx @deepseek-ai/dsh plugin --profile web remove @mastergo/dsh-canvas
```

## What it provides

- MasterGo Canvas MCP tools inside DeepSeek Harness.
- Automatic installation, checksum verification, startup, reuse, and shutdown
  handling for the isolated `mgmcp-dsh` sidecar.
- macOS, Windows, and Linux builds for x64 and arm64.
- Graceful degradation: a Canvas connection failure does not disable unrelated
  Harness plugins.
- An image-layer import tool that places an original image and its separated
  layers into one compact, editable MasterGo canvas block.

The bundle uses the model provider selected by the user in Harness. Its optional
MasterGo model provider is disabled by default and is not required for Canvas
MCP operations.

## No extra client or binary setup

The npm package contains a dedicated `mgmcp-dsh` build for every supported
platform. On first use, the bundle selects the matching binary, verifies its
release checksum, installs it under the user's application-data directory, and
starts or reuses the compatible DSH process.

The normal MasterGo client remains compatible, but it is not a prerequisite.

## Security and data boundaries

- `mgmcp-dsh` uses a generated local access key and loopback-only transport.
- MasterGo and loopback Origin checks are enforced by the sidecar.
- Local path tools are restricted to the active Harness workspace and checked
  against symlink escapes.
- Remote image imports reject redirects and private or reserved network targets.
- Canvas transport is local. Model-visible context is handled by the model
  provider the user selected in Harness.
- Canvas import itself does not consume MasterGo credits. A separately enabled
  MasterGo model provider may be subject to its own billing policy.

See [SECURITY.md](./SECURITY.md) before reporting a vulnerability.

## Compatibility

DeepSeek Harness is currently a developer preview and may introduce breaking
plugin API changes. Releases of this bundle pin and test the supported runtime
contract. When reporting a compatibility issue, include the Harness version,
bundle version, operating system, architecture, and the output of the Canvas
status check without credentials or private document data.

## Support and releases

- Package: [npm — `@mastergo/dsh-canvas`](https://www.npmjs.com/package/@mastergo/dsh-canvas)
- Issues: [GitHub Issues](https://github.com/mastergo-design/dsh-canvas/issues)
- Changes: [CHANGELOG.md](./CHANGELOG.md)
- DeepSeek Harness: [official repository](https://github.com/deepseek-ai/deepseek-harness)

This repository is the public documentation, release-information, and support
home for the package. Internal build infrastructure and private development
history are intentionally not mirrored here.
