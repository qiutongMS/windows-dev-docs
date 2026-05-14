---
title: Migrate an iOS app to WinUI 3
description: Use AI assistance to port an iOS app to WinUI 3 and the Windows App SDK — mapping UIKit concepts, Swift patterns, and iOS lifecycle events to their WinUI equivalents.
ms.topic: how-to
ms.date: 05/14/2026
ms.author: jken
author: GrantMeStrength
---

# Migrate an iOS app to WinUI 3

If you have an iOS app and want to bring it to Windows, AI tools can do most of the mapping work. This page covers the key concept translations from UIKit/SwiftUI to WinUI 3, and how to use the iOS migration skill to automate the conversion.

## Install the migration skill

> [!NOTE]
> The `winui-ios-migration` skill is coming soon. *(Link to come.)*

Once available, install it alongside the WinUI agent plugin:

```powershell
gh copilot plugin install winui@awesome-copilot
```

## Concept mapping

| iOS (UIKit / SwiftUI) | WinUI 3 equivalent | Notes |
|---|---|---|
| `UIViewController` | `Page` | WinUI pages are navigated via `Frame` |
| `UINavigationController` | `Frame` + `NavigationView` | Use `Frame.Navigate()` for page transitions |
| `UITabBarController` | `NavigationView` (top or left tabs) | |
| `UITableView` | `ListView` | Use `ObservableCollection<T>` for data binding |
| `UICollectionView` | `GridView` | |
| `UIAlertController` | `ContentDialog` | Must be parented to the current `XamlRoot` |
| `UILabel` | `TextBlock` | |
| `UITextField` | `TextBox` | |
| `UIButton` | `Button` | |
| `UIImageView` | `Image` | |
| `UIStackView` | `StackPanel` | Set `Orientation` to `Horizontal` or `Vertical` |
| `Auto Layout` | `Grid` / `StackPanel` / `RelativePanel` | XAML layout is row/column based |
| `@State` / `@Binding` (SwiftUI) | `INotifyPropertyChanged` / `ObservableProperty` (CommunityToolkit.Mvvm) | |
| `NSUserDefaults` | `ApplicationData.Current.LocalSettings` | |
| `URLSession` | `HttpClient` | Use `System.Net.Http.HttpClient` |
| `NotificationCenter` | Events or `WeakReferenceMessenger` (CommunityToolkit.Mvvm) | |
| `DispatchQueue.main.async` | `DispatcherQueue.TryEnqueue` | |
| `AppDelegate.applicationDidFinishLaunching` | `App.OnLaunched` | |
| `SceneDelegate` / `windowScene` | `MainWindow` / `AppWindow` | |
| `FileManager` | `StorageFolder` / `StorageFile` | |
| `UserNotifications` | `AppNotificationManager` (Microsoft.Windows.AppNotifications) | |

## Starter prompt

Use this prompt to give your AI agent the context it needs before starting a migration:

```
I'm migrating an iOS app to WinUI 3 using the Windows App SDK.

The app is written in [Swift / Objective-C] using [UIKit / SwiftUI].

Apply these mappings:
- UIViewController → Page, navigated via Frame
- UINavigationController → Frame + NavigationView
- UITableView → ListView with ObservableCollection<T>
- UIAlertController → ContentDialog (parented to XamlRoot)
- NSUserDefaults → ApplicationData.Current.LocalSettings
- URLSession → System.Net.Http.HttpClient
- DispatchQueue.main.async → DispatcherQueue.TryEnqueue
- @State / @Binding → INotifyPropertyChanged via CommunityToolkit.Mvvm

Use Microsoft.UI.Xaml.* namespaces throughout — never Windows.UI.Xaml.*.
Generate C# — not Swift.
```

## What doesn't map directly

Some iOS concepts don't have a direct WinUI equivalent:

- **In-app purchases**: Use the [Microsoft Store commerce APIs](https://learn.microsoft.com/windows/uwp/monetize/) via `Windows.Services.Store`
- **Push notifications (APNs)**: Use [Windows Push Notification Services (WNS)](https://learn.microsoft.com/windows/apps/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview)  
- **HealthKit / ARKit / CoreML**: Windows equivalents exist in [Windows Health](https://learn.microsoft.com/windows/apps/design/shell/tiles-and-notifications/), [Windows Mixed Reality](https://learn.microsoft.com/windows/mixed-reality/), and [Windows ML](https://learn.microsoft.com/windows/ai/windows-ml/)
- **App Clips**: No direct equivalent — consider [web-to-app linking](https://learn.microsoft.com/windows/uwp/launch-resume/web-to-app-linking)

## Related content

- [Migrate from UWP](uwp-to-winui.md)
- [WinUI agent plugin](../winui-agent-plugin.md)
- [Microsoft Learn MCP Server](../mcp-server.md)
