---
title: "WinApp VS Code extension"
description: Use the WinApp extension for VS Code to initialize, run, debug, package, and sign WinUI 3 apps without Visual Studio.
ms.topic: overview
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# WinApp VS Code extension

The WinApp extension brings the Windows App Development CLI into VS Code — initialize, run, debug, package, and sign Windows apps without leaving the editor.

> [!NOTE]
> The extension is in prerelease. Features and commands may change. [File feedback](https://github.com/microsoft/WinAppCli/issues).

## Install

```powershell
code --install-extension microsoft-winappcli.winapp
```

Or search **WinApp** in the Extensions panel (**Ctrl+Shift+X**). Requires the [WinApp CLI](setup.md#2-install-winapp-cli) to be installed first.

## Command Palette commands

All commands are available via **Ctrl+Shift+P → WinApp**:

| Command | What it does |
|---------|-------------|
| **WinApp: Initialize Project** | Set up a new project with the Windows SDK and/or Windows App SDK |
| **WinApp: Run Application** | Run your app as a loose-layout package with full package identity |
| **WinApp: Create MSIX Package** | Package your app into an MSIX installer |
| **WinApp: Create Debug Identity** | Add sparse package identity to an existing executable for debugging |
| **WinApp: Unregister Package** | Remove a sideloaded development package |
| **WinApp: Generate Manifest** | Generate an `AppxManifest.xml` from a template |
| **WinApp: Add Manifest Execution Alias** | Add an execution alias to the app manifest |
| **WinApp: Update Manifest Assets** | Generate all required app icon assets from a single source image |
| **WinApp: Generate Certificate** | Create a development signing certificate |
| **WinApp: Certificate Info** | View details about a certificate file |
| **WinApp: Install Certificate** | Install a `.pfx` or `.cer` certificate (requires Administrator) |
| **WinApp: Sign Package** | Sign an MSIX package with a certificate |
| **WinApp: Restore Packages** | Restore project packages and dependencies |
| **WinApp: Update Packages** | Update packages to the latest versions |
| **WinApp: Get WinApp Path** | Show the path to the installed WinApp CLI executable |
| **WinApp: Run SDK Tool** | Run Windows SDK tools directly |

## Workflow

1. `dotnet new winui-navview -n MyApp` — scaffold project
2. `cd MyApp && dotnet run` — build and verify it runs
3. `code .` — open in VS Code
4. **Ctrl+Shift+P → WinApp: Run Application** — run with package identity
5. Edit XAML and C# files with AI assistance
6. **Ctrl+Shift+P → WinApp: Create MSIX Package** — package for distribution
7. `winapp store publish ./*.msix --appId <your-app-id>` — publish to the Store

## Related content

- [Set up your environment](setup.md)
- [Quickstart: Build and publish a Windows app with AI](quickstart.md)
- [WinUI agent plugin](winui-agent-plugin.md)
