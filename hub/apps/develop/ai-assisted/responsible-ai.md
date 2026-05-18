---
title: "Responsible AI in Windows development"
description: Guidance on responsible use of AI tools in Windows app development, including transparency, fairness, and safety considerations.
ms.topic: overview
ms.date: 05/13/2026
ms.author: jken
author: GrantMeStrength
---

# Responsible AI in Windows development

AI tools can dramatically accelerate Windows app development — but speed doesn't remove responsibility. The code your AI agent generates is code you ship, and you are accountable for everything in your app regardless of how it was written.

This page covers responsible practices for *using* AI tools to build apps, and for *building* apps that incorporate AI features.

## You own the code

When an AI agent generates a function, a layout, or an API call, it becomes your code the moment you commit it. The same standards apply whether code was written by hand or generated:

- Read and understand every change before accepting it
- Test AI-generated code at least as thoroughly as hand-written code — models can generate plausible-looking code that is subtly wrong
- Don't use "the AI wrote it" as an explanation for a bug or a security issue in production

This also means AI tools don't remove the need for code review. They change what you're reviewing, not whether you review.

## What not to send to AI tools

Be deliberate about what you include in prompts and context windows:

- **Secrets and credentials** — Never paste API keys, passwords, or connection strings into a prompt. Even in a private chat session, credentials in prompts are a security risk and may appear in logs.
- **Customer data and PII** — Don't use real customer names, emails, or usage data as example inputs, even to explain a bug. Use synthetic data.
- **Proprietary business logic** — Understand your organisation's policy on what source code can be sent to external AI services before sharing internal systems code.

The [security page](security.md) covers what to do instead for secrets and credentials.

## AI models have stale knowledge

The AI tools you use today were trained on data with a cutoff date. For Windows development, this means models have seen far more UWP samples than WinUI 3 samples — which is exactly why this documentation section exists.

Don't treat AI output as authoritative for:

- Current API names and namespaces (verify against [WinUI 3 API reference](https://learn.microsoft.com/windows/windows-app-sdk/api/winrt/))
- Current SDK versions and package names
- Store policies and submission requirements (these change frequently)
- Security guidance (models may reproduce outdated cryptography or auth patterns)

The [Microsoft Learn MCP server](mcp-server.md) and [WinUI agent plugin](winui-agent-plugin.md) mitigate stale knowledge by grounding your agent in current documentation — but always verify anything security-critical against primary sources.

## Accessibility

AI-generated UI frequently omits accessibility support. A model trained on millions of XAML samples will reproduce the average quality of those samples — and the average historically skips `AutomationProperties`, keyboard navigation, and sufficient contrast.

When accepting AI-generated XAML or controls code:

- Check that interactive elements have `AutomationProperties.AutomationId` and `AutomationProperties.Name` set
- Verify focus order is logical — tab stops should follow reading order
- Test with Narrator or another screen reader before shipping
- Use the [Accessibility Insights for Windows](https://accessibilityinsights.io/docs/windows/overview/) tool to catch gaps automatically

Ask your agent explicitly: *"Add accessibility properties to all interactive elements in this XAML."* Don't assume it was done.

## If your app uses AI features

If you're building AI capabilities *into* your app — not just using AI to write the app — additional responsibilities apply.

**Be transparent with users.** Tell users:
- What data your app sends to AI services
- Whether AI is making decisions that affect them
- How to opt out if appropriate

**Keep humans in the loop for consequential actions.** Don't let AI autonomously delete data, make purchases, send messages on behalf of the user, or take other irreversible actions without explicit confirmation.

**Test for bias and unexpected outputs.** AI models can produce outputs that are biased, offensive, or factually wrong. Test your app's AI features with diverse inputs and edge cases before shipping.

**Use content safety tools.** If your app generates or processes user-facing text, images, or other content using AI, use [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview) or equivalent filtering to catch harmful outputs before they reach users.

## Licensing and attribution

AI tools may generate code that resembles existing open-source code. Before using AI-generated code in a commercial app:

- Know your organisation's policy on AI-generated code contributions
- Review Microsoft's [guidance on Copilot and intellectual property](https://learn.microsoft.com/legal/cognitive-services/openai/transparency-note)
- Apply the same open-source license compliance checks you would to any third-party code

## Microsoft's Responsible AI principles

Microsoft designs AI products and features guided by six principles: fairness, reliability and safety, privacy and security, inclusiveness, transparency, and accountability.

Learn more at [microsoft.com/ai/responsible-ai](https://www.microsoft.com/en-us/ai/responsible-ai).

## Related content

- [Security considerations for AI-generated code](security.md)
- [Microsoft Responsible AI principles](https://www.microsoft.com/en-us/ai/responsible-ai)
- [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview)
- [Accessibility Insights for Windows](https://accessibilityinsights.io/docs/windows/overview/)
- [Microsoft Copilot transparency note](https://learn.microsoft.com/legal/cognitive-services/openai/transparency-note)
