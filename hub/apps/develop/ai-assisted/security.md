---
title: "Security considerations for AI-generated code"
description: Review AI-generated Windows app code for security risks, including input validation, credential handling, and package integrity.
ms.topic: overview
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# Security considerations for AI-generated code

AI code generation is fast but not inherently secure — models may reproduce insecure patterns from training data. Apply the same security review to AI-generated code as you would to any other code, with particular attention to the areas below.

## Input validation

AI tends to generate permissive input handling. Always validate lengths, types, and ranges before acting on user input.

- Never pass raw `TextBox.Text` values to shell commands, file paths, or database queries.
- Validate string lengths before writing to storage or sending over the network.
- Use an allow-list approach for file paths — check that resolved paths stay within expected directories.

Add this to your prompt: *"Add input validation and length limits to all user-facing fields."*

## Credential and secret handling

Never hardcode API keys, passwords, or connection strings. AI often generates placeholder strings like `"your-api-key-here"` — treat these as bugs.

- Store credentials in `Windows.Security.Credentials.PasswordVault`:

  ```csharp
  var vault = new PasswordVault();
  vault.Add(new PasswordCredential("MyApp", username, password));
  ```

- Retrieve them at runtime:

  ```csharp
  var credential = vault.Retrieve("MyApp", username);
  credential.RetrievePassword();
  ```

- Use environment variables or Azure Key Vault for service credentials in server-side or CI scenarios.

## Package and dependency integrity

Review every NuGet package an AI agent suggests before adding it to your project.

- Verify the publisher on [nuget.org](https://www.nuget.org/) — look for the blue shield (Microsoft) or a known publisher.
- Scan for known vulnerabilities:
  ```powershell
  dotnet list package --vulnerable
  ```
- Prefer packages with recent updates and active maintenance.

## App capabilities and permissions

AI-generated `Package.appxmanifest` files often include broad capabilities. Review the `<Capabilities>` section and remove anything your app doesn't need.

Common over-broad capabilities to watch for:
- `broadFileSystemAccess` — only needed if your app genuinely reads arbitrary file system paths
- `documentsLibrary` — requires Store special approval; avoid unless necessary
- `userAccountInformation` — only if you need the user's name or photo

## Code review checklist

Before shipping AI-generated code, verify:

- No hardcoded secrets or credentials
- User input validated before use
- File paths checked against allowed directories
- Minimum necessary capabilities declared in the manifest
- NuGet packages scanned for vulnerabilities (`dotnet list package --vulnerable`)
- Sensitive data stored in `PasswordVault`, not `ApplicationData.LocalSettings`
- All network calls use HTTPS
- Exception messages don't expose internal paths or stack traces to users

## Related content

- [Responsible AI for Windows development](responsible-ai.md)
- [Microsoft Security Response Center](https://msrc.microsoft.com/)

