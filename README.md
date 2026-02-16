# ArgusTest

**iOS Device Monitoring for AI Development**

ArgusTest gives AI coding assistants real-time access to your physical iOS device — screenshots, crash logs, device state, and Sentry integration — via the [Model Context Protocol (MCP)](https://modelcontextprotocol.io).

Connect your iPhone via USB. Your AI assistant sees what your app is doing. That's it.

---

## Install

```bash
npm i -g @argustest/argus
```

The installer automatically downloads the correct binary for your Mac:

| Architecture | Binary |
|---|---|
| Apple Silicon (M1/M2/M3/M4) | `argus-macos-arm64` |
| Intel | `argus-macos-x86_64` |

After install, add to your Claude Code MCP config:

```json
{
  "mcpServers": {
    "argus": {
      "command": "argus-mcp"
    }
  }
}
```

## How It Works

```
┌─────────────┐    USB     ┌─────────────┐    MCP     ┌─────────────┐
│   iPhone    │───────────▶│   ArgusTest  │───────────▶│  Claude /   │
│  (physical) │            │  MCP Server  │            │  AI Agent   │
└─────────────┘            └─────────────┘            └─────────────┘
                                 │
                                 ▼
                          ┌─────────────┐
                          │   Sentry    │
                          │  Fallback   │
                          └─────────────┘
```

| Device State | Monitoring Mode | What AI Can Access |
|---|---|---|
| USB connected | **USB Primary** | Screenshots, crash logs, real-time errors, device info, Sentry |
| USB disconnected | **Sentry Fallback** | Sentry issues, error trends, release health |

Monitoring mode switches automatically when you connect or disconnect your device.

## MCP Tools Available

When connected via MCP, your AI assistant gets access to these tools:

| Tool | Description |
|---|---|
| `get_device_info` | Device model, iOS version, battery, storage |
| `take_screenshot` | Capture the current screen |
| `get_crash_logs` | Recent crash reports with stack traces |
| `get_device_errors` | Real-time error stream |
| `get_sentry_issues` | Sentry issues for your project |
| `get_device_status` | Connection state and monitoring mode |
| `health_check` | Full system diagnostics |

## Requirements

- macOS 12.0+
- Physical iOS device connected via USB
- Xcode Command Line Tools
- Node.js 18+ (for npm install)

## Links

- **Website**: [argustest.dev](https://argustest.dev)
- **npm**: [@argustest/argus](https://www.npmjs.com/package/@argustest/argus)
- **Releases**: [Binary downloads](https://github.com/AbleVarghese/homebrew-tap/releases)

## About This Repository

This repository hosts the CI build infrastructure and binary releases for ArgusTest. Both `arm64` (Apple Silicon) and `x86_64` (Intel) binaries are built automatically in CI and attached to each [GitHub Release](https://github.com/AbleVarghese/homebrew-tap/releases).

When you run `npm i -g @argustest/argus`, the postinstall script downloads the correct binary for your Mac from the latest release here.

## License

Proprietary software. See [argustest.dev/terms](https://argustest.dev/terms) for license terms.

Copyright (c) 2026 Able Varghese. All Rights Reserved.
