---
title: "Microsoft Learn MCP Server"
description: Connect your AI agent to live Microsoft documentation using the Microsoft Learn Model Context Protocol (MCP) server — so it always retrieves current WinUI 3 and Windows App SDK guidance instead of relying on potentially outdated training data.
ms.topic: how-to
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# Microsoft Learn MCP Server

AI models are trained on a snapshot of the web. For Windows development, that means your agent may have learned from WPF and UWP samples written years before WinUI 3 existed — and it can't tell the difference. The Microsoft Learn MCP Server fixes this by giving your agent a tool it can call to retrieve **current, authoritative documentation** at the moment it needs it.

## What is MCP?

The [Model Context Protocol (MCP)](https://modelcontextprotocol.io) is an open standard that lets AI agents call external tools and data sources during a conversation. Instead of relying entirely on training data, an MCP-connected agent can search and read live content — including Microsoft Learn — before generating a response.

## Add the Microsoft Learn MCP Server

The server is hosted by Microsoft and requires no installation or sign-in.

### VS Code (GitHub Copilot)

Add the following to `.vscode/mcp.json` in your project:

```json
{
  "servers": {
    "microsoft-learn": {
      "type": "http",
      "url": "https://learn.microsoft.com/api/mcp"
    }
  }
}
```

VS Code will prompt you to enable the server the first time you open a Copilot chat session.

### Claude Code

Add the server to your Claude Code configuration (`~/.claude/mcp_servers.json`):

```json
{
  "microsoft-learn": {
    "type": "http",
    "url": "https://learn.microsoft.com/api/mcp"
  }
}
```

### Other MCP clients

Any client that supports the MCP HTTP transport can connect using:

```
https://learn.microsoft.com/api/mcp
```

No API key or authentication required.

## What the server can do

Once connected, your agent can search and retrieve pages from Microsoft Learn. For Windows development, this means it can look up:

- Current WinUI 3 control APIs and usage patterns
- Windows App SDK release notes and migration guides  
- `winapp` CLI command reference
- Store submission requirements and certification criteria

## Example

Without the MCP server, asking Copilot to add a file picker may produce code using the deprecated UWP `FileOpenPicker` pattern:

```csharp
// ❌ UWP pattern — may be generated without MCP context
var picker = new FileOpenPicker();
picker.SuggestedStartLocation = PickerLocationId.DocumentsLibrary;
```

With the MCP server connected, the agent retrieves the current WinUI 3 guidance and generates the correct pattern:

```csharp
// ✅ WinUI 3 pattern — retrieved from current docs
var picker = new FileOpenPicker();
var hwnd = WinRT.Interop.WindowNative.GetWindowHandle(this);
WinRT.Interop.InitializeWithWindow.Initialize(picker, hwnd);
picker.SuggestedStartLocation = PickerLocationId.DocumentsLibrary;
var file = await picker.PickSingleFileAsync();
```

> [!TIP]
> For deeper WinUI-specific guidance, combine the MCP server with the [WinUI agent plugin](winui-agent-plugin.md). The plugin handles coding patterns; the MCP server handles documentation retrieval.

## Related content

- [WinUI agent plugin](winui-agent-plugin.md)
- [Quickstart: Build and publish a Windows app with AI](quickstart.md)
- [Model Context Protocol specification](https://modelcontextprotocol.io)
- [GitHub Copilot MCP documentation](https://docs.github.com/copilot/customizing-copilot/extending-copilot-with-mcp)
