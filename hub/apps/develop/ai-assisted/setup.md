---
title: "Set up your AI development environment"
description: Install and configure the free tools for AI-assisted Windows development — VS Code, WinApp CLI, dotnet new templates, and the WinUI agent plugin.
ms.topic: overview
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# Set up your AI development environment

AI-assisted WinUI 3 development runs entirely from VS Code and the command line — no Visual Studio license required. This page covers the one-time setup so you can follow the [quickstart](quickstart.md) or start migrating an existing app.

## Prerequisites

- Windows 10 version 1809 or later
- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Git](https://git-scm.com/)
- A GitHub Copilot subscription, or another AI agent with tool-calling support

## Install the tools

### 1. Install VS Code

```powershell
winget install Microsoft.VisualStudioCode
```

### 2. Install WinApp CLI

```powershell
winget install Microsoft.winappcli --source winget
```

### 3. Install the WinApp VS Code extension

```powershell
code --install-extension microsoft-winappcli.winapp
```

Or search **WinApp** in the VS Code Extensions panel (Ctrl+Shift+X).

### 4. Install the WinUI agent plugin

```powershell
gh copilot plugin install winui@awesome-copilot
```

The plugin gives your AI agent live WinUI 3 API knowledge so it generates correct `Microsoft.UI.Xaml.*` code. See [WinUI agent plugin](winui-agent-plugin.md) for details.

## Verify your setup

```powershell
winapp --version
```

`winapp --version` confirms the CLI is installed and shows the current version.

## Configure your AI agent for live API data

For best results, connect your AI agent to the Microsoft Learn MCP server so it fetches current WinUI 3 API docs at query time rather than relying on training data alone. See [Microsoft Learn MCP server](mcp-server.md) for configuration steps.

## Next steps

- [Quickstart: Build and publish a Windows app with AI](quickstart.md)
- [WinUI agent plugin](winui-agent-plugin.md)
- [Microsoft Learn MCP server](mcp-server.md)
