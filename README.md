# Agent Shepherd — Releases

Latest release: v0.2.25 — 2026-08-31T17:20:41Z

Signed release artifacts for the [Agent Shepherd](https://agentshepherd.dev) CLI and MCP server.
The product source is proprietary; this repository hosts downloadable binaries only.

Each release ships `shepherd` (the CLI) and `shepherd-mcp` (the MCP stdio server your
coding agent talks to) for macOS, Linux, and Windows, plus SBOMs and a keyless
cosign signature over `checksums.txt`.

## Install (macOS / Linux)

```sh
OS=$(uname -s | tr '[:upper:]' '[:lower:]')
ARCH=$(uname -m | sed 's/x86_64/amd64/; s/aarch64/arm64/')
gh release download --repo blackknight467/agentshepherd-releases \
  --pattern "agent-shepherd_*_${OS}_${ARCH}.tar.gz"
tar -xzf agent-shepherd_*.tar.gz
install -m 0755 shepherd shepherd-mcp ~/.local/bin/
```

Windows: download the `windows_amd64.zip` asset and put both `.exe` files on your `PATH`.

## Verify

```sh
cosign verify-blob checksums.txt \
  --signature checksums.txt.sig --certificate checksums.txt.pem \
  --certificate-identity-regexp '^https://github.com/blackknight467/agentshepherd' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
shasum -a 256 -c checksums.txt --ignore-missing
```

## Get started

Docs, signup, and agent setup: **https://agentshepherd.dev/docs**
