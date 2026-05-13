---
title: AI-assisted Windows development
description: Build Windows apps faster using AI agents, GitHub Copilot, Claude Code, and the Windows AI development toolkit — with tools that are free, work in VS Code, and require no prior Windows experience.
ms.topic: overview
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# AI-assisted Windows development

Windows has a complete set of free, AI-ready tools that take you from idea to published app — entirely from the command line or VS Code, without needing Visual Studio. Whether you're building a new app from scratch or modernizing one you wrote years ago, AI agents can do the heavy lifting.

> [!TIP]
> New to Windows development? Start with the [Quickstart: Build and publish a Windows app with AI](quickstart.md) — you can have a working app in under 30 minutes using only free tools.

---

## What path are you on?

:::row:::
    :::column:::
        ### I'm starting fresh
        Use the `winui-dev` agent and `dotnet new` templates to scaffold, build, run, and publish a new Windows app — no Windows experience required.

        → [Quickstart](quickstart.md)
        → [Set up your environment](setup.md)
        → [WinUI agent plugin](winui-agent-plugin.md)
    :::column-end:::
    :::column:::
        ### I have an existing app
        AI tools can help you migrate WPF, WinForms, or UWP apps to modern WinUI 3, or add Windows capabilities to apps built with Electron, Flutter, Tauri, or Rust.

        → [Migrate from WPF](migrate/wpf-to-winui.md)
        → [Migrate from UWP](migrate/uwp-to-winui.md)
        → [Cross-framework apps](migrate/cross-framework.md)
    :::column-end:::
:::row-end:::

---

## Tools in this section

:::row:::
    :::column:::
        [![WinUI agent plugin icon](images/tile-ai-plugin.png)](winui-agent-plugin.md)
        **[WinUI agent plugin](winui-agent-plugin.md)**
        8 skills for end-to-end WinUI development in GitHub Copilot or Claude Code.
    :::column-end:::
    :::column:::
        [![VS Code extension icon](images/tile-vscode.png)](vs-code-extension.md)
        **[WinApp VS Code extension](vs-code-extension.md)**
        Run, debug, package, and sign Windows apps from any framework in VS Code.
    :::column-end:::
    :::column:::
        [![dotnet new templates icon](images/tile-templates.png)](dotnet-templates.md)
        **[dotnet new WinUI templates](dotnet-templates.md)**
        Create WinUI apps from the command line — no Visual Studio required.
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [![MCP Server icon](images/tile-mcp.png)](mcp-server.md)
        **[Microsoft Learn MCP Server](mcp-server.md)**
        Give your AI agent live access to official Windows documentation.
    :::column-end:::
    :::column:::
        [![Testing icon](images/tile-testing.png)](testing.md)
        **[AI-assisted testing](testing.md)**
        Generate and run UI tests using Windows UI Automation and the `winui-ui-testing` skill.
    :::column-end:::
    :::column:::
        [![Store icon](images/tile-store.png)](store-publishing.md)
        **[Publish to the Store](store-publishing.md)**
        Publish your app to the Microsoft Store from the command line using `winapp store`.
    :::column-end:::
:::row-end:::

---

## Frequently asked questions

### Can I build a WinUI 3 app without Visual Studio?

Yes. Three commands are all you need to go from nothing to a running WinUI 3 app:

```bash
dotnet new winui-navview -n MyApp   # scaffold
cd MyApp
winapp run                           # build and run
```

You can build, run, debug, package, and publish entirely from VS Code or the terminal using the [WinApp VS Code extension](vs-code-extension.md), [`dotnet new` WinUI templates](dotnet-templates.md), and the [Windows App Development CLI](../dev-tools/winapp-cli/index.md). Visual Studio is still the best experience for complex XAML debugging and designer tooling, but it's no longer required to get started. See the [Quickstart](quickstart.md) for a complete walkthrough.

### Are these tools free?

Yes. The [WinApp VS Code extension](vs-code-extension.md), [WinApp CLI](../dev-tools/winapp-cli/index.md), and [`dotnet new` WinUI templates](dotnet-templates.md) are all free and open source. GitHub Copilot requires a [GitHub Copilot subscription](https://github.com/features/copilot) (a free tier is available). The [Microsoft Learn MCP Server](mcp-server.md) is free with no authentication required.

### Will Copilot give me outdated UWP code instead of WinUI 3?

By default, yes — Copilot's training data contains far more UWP samples than WinUI 3, so it tends to suggest deprecated patterns like `Windows.UI.Xaml` namespaces, `CoreDispatcher`, and `MessageDialog`. The [WinUI agent plugin](winui-agent-plugin.md) fixes this directly: its custom instructions explicitly override those patterns with correct WinUI 3 equivalents, and the [Microsoft Learn MCP Server](mcp-server.md) gives your agent live access to current documentation.

### Does this work with Claude Code as well as GitHub Copilot?

Yes. The [`winui@awesome-copilot` plugin](winui-agent-plugin.md) works with both GitHub Copilot and Claude Code. The [Microsoft Learn MCP Server](mcp-server.md) works with any MCP-compatible client.

### How long does it take to go from idea to a published app?

With the tools in this section, you can scaffold, run, and test a basic WinUI app in under 30 minutes. Publishing to the Microsoft Store requires a [Partner Center account](https://partner.microsoft.com/dashboard) (free to create, $19 one-time registration fee) and app certification, which typically takes 1–3 business days. See the [Quickstart](quickstart.md) for a complete walkthrough.

---

## Starter prompts

Copy and adapt these prompts to steer your AI assistant toward current WinUI 3 tools and away from outdated UWP or WPF patterns.

### Building a new app

Use this prompt when starting from scratch. It anchors Copilot to the correct toolchain and prevents it from suggesting Visual Studio or UWP-era scaffolding:

```
Create a new WinUI 3 Windows app using the `dotnet new winui-navview` template (from the
Microsoft.WindowsAppSDK.WinUI.CSharp.Templates package). Use the winapp CLI to build and run
it — not Visual Studio. Use VS Code as the editor.

Use Microsoft.UI.Xaml for all controls and layouts — never Windows.UI.Xaml.
Use DispatcherQueue, not CoreDispatcher.
Use AppWindow and OverlappedPresenter for window management, not ApplicationView.
Use ContentDialog, not MessageDialog.
```

### Migrating an existing UWP or WPF app

Use this prompt when modernising an existing app. It explicitly lists the namespace substitutions that AI assistants most commonly get wrong:

```
I'm migrating a [UWP / WPF] app to WinUI 3 using the Windows App SDK.

Apply these substitutions throughout:
- Windows.UI.Xaml.* → Microsoft.UI.Xaml.*
- CoreDispatcher / Dispatcher.RunAsync → DispatcherQueue.TryEnqueue
- ApplicationView → AppWindow + OverlappedPresenter
- MessageDialog → ContentDialog
- Windows.UI.Notifications → Microsoft.Windows.AppNotifications (AppNotificationManager)
- Frame.Navigate with UWP page types → WinUI 3 Frame + Page

Do not introduce any Windows.UI.* APIs. Flag any APIs that don't have a direct WinUI 3
equivalent so I can decide how to handle them.
```

### Adding a feature to an existing WinUI 3 app

Use this when asking Copilot to extend an app that's already on WinUI 3. It reinforces correct patterns even when the existing codebase has mixed signals:

```
This is a WinUI 3 app using the Windows App SDK. When adding new code:
- Use Microsoft.UI.Xaml.* namespaces only
- Use DispatcherQueue for any thread marshalling
- Use the Community Toolkit (CommunityToolkit.Mvvm) for MVVM patterns
- Use winapp run to test changes — do not open or require Visual Studio
```

> [!TIP]
> For the best results with the least prompt engineering, install the [WinUI agent plugin](winui-agent-plugin.md) — it applies these constraints automatically for every response.

---

## Related content

- [Windows App Development CLI](../dev-tools/winapp-cli/index.md)
- [Security considerations for AI-generated code](security.md)
- [Responsible AI in Windows development](responsible-ai.md)
