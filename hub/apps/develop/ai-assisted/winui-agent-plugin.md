---
title: WinUI agent plugin for GitHub Copilot and Claude Code
description: Use the winui@awesome-copilot plugin to give GitHub Copilot or Claude Code accurate WinUI 3 knowledge — including 8 specialized skills and a dedicated winui-dev agent for end-to-end Windows app development.
ms.topic: how-to
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# WinUI agent plugin for GitHub Copilot and Claude Code

The `winui@awesome-copilot` plugin gives GitHub Copilot and Claude Code accurate, up-to-date knowledge of WinUI 3 and the Windows App SDK. It includes 8 specialized skills and a dedicated `winui-dev` agent that guides AI through the full development loop — scaffold, build, run, test, package, and migrate — using up to 70% fewer tokens than unguided agents.

## Why do I need this plugin?

Without the plugin, AI coding agents frequently suggest outdated UWP patterns for Windows development. UWP has far more training data (Stack Overflow answers, GitHub samples, tutorials) than WinUI 3, so agents default to deprecated APIs:

| Without plugin | With plugin |
|---|---|
| `Windows.UI.Xaml.Controls` | `Microsoft.UI.Xaml.Controls` |
| `CoreDispatcher` | `DispatcherQueue` |
| `MessageDialog` | `ContentDialog` |
| `Windows.UI.Xaml.Window` | `Microsoft.UI.Xaml.Window` |

The plugin fixes this by injecting explicit WinUI 3 rules as custom instructions that override the agent's training data defaults.

## Install the plugin

**Requires:** GitHub Copilot CLI or Claude Code, and the [Windows App Development CLI](../dev-tools/winapp-cli/index.md) (`winget install Microsoft.WinAppCLI`).

```bash
gh copilot plugin install winui@awesome-copilot
```

This copies the plugin's agents, skills, and custom instructions into your project's `.github/` directory, where Copilot and Claude Code pick them up automatically.

## The winui-dev agent

The `winui-dev` agent orchestrates the full development loop. It knows how to drive each stage, recognize common failure patterns that get generic agents stuck in loops, and steer toward successful WinUI 3 patterns.

To use the agent in GitHub Copilot chat, switch to agent mode and ask in natural language:

```
@winui-dev Build me a WinUI app that shows a list of files in a folder
```

## The 8 skills

Each skill is a focused slash command optimized for a specific stage of development:

| Skill | Command | What it does |
|---|---|---|
| **winui-setup** | `/winui-setup` | Validates your development environment and fixes common configuration issues |
| **winui-dev-workflow** | `/winui-dev-workflow` | Guides the scaffold → build → run → iterate loop |
| **winui-design** | `/winui-design` | Generates XAML layouts using WinUI 3 controls and Fluent Design |
| **winui-code-review** | `/winui-code-review` | Reviews your code for WinUI 3 correctness and common anti-patterns |
| **winui-ui-testing** | `/winui-ui-testing` | Generates UI tests using Windows UI Automation |
| **winui-packaging** | `/winui-packaging` | Guides MSIX packaging, signing, and Store submission |
| **winui-wpf-migration** | `/winui-wpf-migration` | Migrates WPF code to WinUI 3 with API-level mappings |
| **winui-session-report** | `/winui-session-report` | Summarizes what was built in a session and suggests next steps |

## Works with GitHub Copilot and Claude Code

The plugin works with both GitHub Copilot (via GitHub Copilot CLI or VS Code) and Claude Code. The `.github/` directory format is supported by both agents.

## Related content

- [Quickstart: Build and publish a Windows app with AI](quickstart.md)
- [AI-assisted testing](testing.md) — using the `winui-ui-testing` skill
- [Migrate from WPF with AI](migrate/wpf-to-winui.md) — using the `winui-wpf-migration` skill
- [Migrate from UWP with AI](migrate/uwp-to-winui.md)
- [Microsoft Learn MCP Server](mcp-server.md) — give your agent live docs access
