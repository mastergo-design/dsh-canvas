# Security policy

## Reporting a vulnerability

Use this repository's private **Report a vulnerability** form. Do not disclose
security findings in a public issue or discussion.

Include only the information needed to reproduce the problem:

- `@mastergo/dsh-canvas` and DeepSeek Harness versions;
- operating system and CPU architecture;
- affected tool or lifecycle stage;
- minimal reproduction steps and sanitized logs; and
- the expected security boundary and observed behavior.

Never include npm tokens, OAuth grants, cookies, local access keys, private
MasterGo document content, enterprise data, or unrelated local files.

If private vulnerability reporting is unavailable, contact MasterGo through an
official support channel and ask for a private security-reporting route before
sharing technical details.

## Supported versions

Security fixes are released on the newest published package version. Users should
upgrade before reporting behavior that has already been corrected in a newer
release.

## Intended boundaries

The bundle is designed around these boundaries:

- the packaged sidecar is the isolated `mgmcp-dsh` edition with authenticated
  loopback transport;
- when a compatible standard sidecar is already owned by MasterGo Client, the
  Bundle reuses that existing loopback service without stopping, replacing, or
  upgrading it, and retains the client's authentication behavior;
- the Canvas bridge exposes a fixed, reviewed MCP tool allowlist;
- accepted workspace paths cannot escape through path traversal or symlinks; and
- `submit_page_to_canvas` accepts inline HTML instead of reading a local HTML
  file path.
