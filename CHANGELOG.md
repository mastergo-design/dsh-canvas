# Changelog

All notable public releases of `@mastergo/dsh-canvas` are recorded here.

## 0.1.3 — 2026-08-27

- Added concrete, copy-ready prompts for reading, reviewing, creating, editing,
  and implementing MasterGo canvas content.
- Added the real user actions required before each prompt, including when a
  MasterGo selection is or is not needed.
- Reorganized technical tool names as developer reference instead of presenting
  them as the primary user workflow.
- Documentation-only update; Canvas runtime behavior is unchanged.

## 0.1.2 — 2026-08-27

- Rewrote the package documentation around the currently supported Canvas MCP
  capabilities and actual installation flow.
- Put the Chinese guide before the matching English guide in the main README.
- Clarified the separation between the DSH-specific `mgmcp-dsh` runtime and the
  standard `mgmcp` process used by the MasterGo client.
- Clarified that Canvas runtime status does not by itself prove that a MasterGo
  document is connected.
- Documentation and package-metadata update only; Canvas runtime behavior is
  unchanged.

## 0.1.1 — 2026-08-27

- Added the public GitHub repository, homepage, issue tracker, and DSH community
  discovery keywords to the npm package metadata.
- Linked the package README to the public support repository and the DeepSeek
  Harness community launch discussion.
- No Canvas, MCP, sidecar, security-boundary, or billing behavior changed.

## 0.1.0 — 2026-08-27

- First public npm release.
- Added the MasterGo Canvas MCP bundle for DeepSeek Harness.
- Bundled isolated `mgmcp-dsh` sidecars for macOS, Windows, and Linux on x64
  and arm64.
- Added automatic sidecar checksum verification, installation, startup, reuse,
  and failure isolation.
- Added authenticated loopback transport and workspace path controls.
