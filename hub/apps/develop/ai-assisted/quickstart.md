---
title: "Quickstart: Build and publish a Windows app with AI"
description: Go from zero to a published Windows app in under 30 minutes using free tools — VS Code, the WinUI agent plugin for GitHub Copilot, dotnet new templates, and the Windows App Development CLI.
ms.topic: quickstart
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# Quickstart: Build and publish a Windows app with AI

In this quickstart, you use free tools to go from an empty folder to a working Windows app — scaffolded, built, run, tested, and ready to publish — using AI assistance throughout.

> [!div class="checklist"]
> * Install the required free tools (~5 minutes)
> * Scaffold a WinUI app from the command line
> * Use the `winui-dev` AI agent to add features
> * Run and test the app in VS Code
> * Package and publish to the Microsoft Store

**Time to complete:** approximately 30 minutes  
**Cost:** free (GitHub Copilot free tier is sufficient)  
**Visual Studio required:** no

---

## Prerequisites

Before you start, install the following free tools:

**1. .NET SDK 10 or later**

```powershell
winget install Microsoft.DotNet.SDK.10
```

**2. Windows App Development CLI (winapp CLI)**

```powershell
winget install Microsoft.WinAppCLI
```

**3. WinUI dotnet new templates**

```powershell
dotnet new install Microsoft.WindowsAppSDK.WinUI.CSharp.Templates
```

**4. GitHub Copilot CLI** (requires a [GitHub Copilot subscription](https://github.com/features/copilot) — free tier available)

```powershell
winget install GitHub.cli
gh extension install github/gh-copilot
```

**5. WinUI agent plugin for GitHub Copilot**

```powershell
gh copilot plugin install winui@awesome-copilot
```

**6. WinApp VS Code extension**  
Install the [WinApp Tools extension](https://marketplace.visualstudio.com/items?itemName=microsoft.winapp-tools) from the VS Code Marketplace.

> [!NOTE]
> You don't need Visual Studio for this quickstart. Everything runs in VS Code and the terminal.

---

## Step 1: Scaffold a new WinUI app

Create a new folder and scaffold a WinUI app with a NavigationView layout — a good starting point for most apps:

```powershell
mkdir MyFirstApp
cd MyFirstApp
dotnet new winui-navview
```

Open the folder in VS Code:

```powershell
code .
```

---

## Step 2: Run the app

Use the WinApp VS Code extension or the CLI to run your app:

**In VS Code:** Press **F5** or click **Run** in the WinApp extension panel.

**From the terminal:**

```powershell
winapp run
```

---

## Step 3: Use the AI agent to add a feature

Now use the `winui-dev` agent to add a feature using natural language. Open GitHub Copilot chat in VS Code and switch to agent mode, or use the Copilot CLI:

```powershell
gh copilot suggest "Add a settings page to my WinUI NavView app with a toggle for dark mode"
```

Apply the suggested changes, then run again:

```powershell
winapp run
```

---

## Step 4: Run UI tests

Use `winapp ui` to inspect your running app and verify the settings page was added correctly:

```powershell
# Start the app in the background (PowerShell 7+)
Start-Process -FilePath winapp -ArgumentList "run" -NoNewWindow

# Inspect the UI tree
winapp ui inspect -a MyFirstApp

# Check the settings button is present
winapp ui search "Settings" -a MyFirstApp

# Take a screenshot
winapp ui screenshot -a MyFirstApp --output screenshot.png
```

---

## Step 5: Package the app

Package your app for distribution:

```powershell
winapp package
```

---

## Step 6: Publish to the Microsoft Store

Use `winapp store` to submit your app directly from the command line. The `winapp store` command wraps the [Microsoft Store Developer CLI](https://aka.ms/msstoredevcli) and downloads it automatically if needed.

```powershell
winapp store publish --package ./bin/MyFirstApp.msix
```

> [!NOTE]
> Publishing requires a [Partner Center account](https://partner.microsoft.com/dashboard). Registration is free to create; a one-time $19 developer fee applies. App certification typically takes 1–3 business days.

---

## Next steps

You've built and published a Windows app using only free, command-line tools and AI assistance. Here's where to go next:

- **Go deeper on AI**: [WinUI agent plugin](winui-agent-plugin.md) — learn all 8 skills and when to use each
- **Use VS Code fully**: [WinApp VS Code extension](vs-code-extension.md) — run, debug, and package without the terminal
- **Have an existing app?**: [Migrate from WPF](migrate/wpf-to-winui.md) or [migrate from UWP](migrate/uwp-to-winui.md) with AI assistance
- **Write better tests**: [AI-assisted testing](testing.md) — generate and automate UI tests
- **Understand the risks**: [Security considerations](security.md) — what to review before shipping AI-generated code
