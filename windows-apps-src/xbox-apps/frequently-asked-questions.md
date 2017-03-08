---
author: Mtoepke
title: "常见问题"
description: "有关 Xbox 上的 UWP 的常见问题解答。"
ms.author: mtoepke
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.assetid: 265fe827-bd4a-48d4-b362-8793b9b25705
translationtype: Human Translation
ms.sourcegitcommit: 5645eee3dc2ef67b5263b08800b0f96eb8a0a7da
ms.openlocfilehash: 059fac41c0c0557dbc3d4739c1da78f794505839
ms.lasthandoff: 02/08/2017

---

# <a name="frequently-asked-questions"></a>常见问题

是否未按预期工作？ 查看此常见问题页面。 另外，请查看[已知问题](known-issues.md)主题和[开发通用 Windows 应用](https://go.microsoft.com/fwlink/?linkid=839446)论坛。 

### <a name="why-are-my-games-and-apps-not-working"></a>为什么我的游戏和应用不工作？

如果你的游戏和应用不工作，或者如果你无法访问应用商店或 Live 服务，你可能在开发人员模式下运行。 当你选择“主页”并在你屏幕的右侧看到较大的“开发人员主页”磁贴（而不是常规的 Gold/Live 内容）时，可以得知你是在开发人员模式下运行。 如果想要玩游戏，你可以打开“开发人员主页”，然后通过使用**退出开发人员模式**按钮切换回零售模式。

### <a name="why-cant-i-connect-to-my-xbox-one-using-visual-studio"></a>为什么我无法使用 Visual Studio 连接到 Xbox One？

首先要确认是在开发人员模式下运行，而不是在零售模式下运行。 你无法连接到在零售模式下运行的 Xbox One。 只需按**主页**按钮并查看你屏幕右侧的“开发人员主页”磁贴，即可对此问题进行检查。 如果你看到的不是该磁贴，而是金会员/Live 内容，这表明你处于零售模式。 若要切换到开发人员模式，需要运行“开发人员模式激活”应用。

> [!NOTE]
> 必须进行用户登录才能部署应用。

有关详细信息，请参阅此页面后面部分的[修复部署失败](#fixing-deployment-failures)。

### <a name="how-do-i-switch-between-retail-mode-and-developer-mode"></a>如何在零售模式和开发人员模式之间切换？

请遵循 [Xbox One 开发人员模式激活](devkit-activation.md)说明以了解有关这些状态的详细信息。

### <a name="how-do-i-know-if-i-am-in-retail-mode-or-developer-mode"></a>我如何知道我是在零售模式下还是在开发人员模式下？

请遵循 [Xbox One 开发人员模式激活](devkit-activation.md)说明以了解有关这些状态的详细信息。 

只需按**主页**按钮并查看你的屏幕右侧，即可对此问题进行检查。 如果你在开发人员模式下，你将在右侧看到“开发人员主页”磁贴。 如果你在零售模式下，你将看到常规的金会员/Live 内容。

### <a name="will-my-games-and-apps-still-work-if-i-activate-developer-mode"></a>当我激活开发人员模式时，我的游戏和应用是否仍可以运行？

是的，你可以从开发人员模式切换到零售模式，同时可以玩游戏。 有关详细信息，请参阅 [Xbox One 开发人员模式激活](devkit-activation.md)页。 

### <a name="can-i-develop-and-publish-x86-apps-for-xbox"></a>我能否开发和发布适用于 Xbox 的 x86 应用？
Xbox 不再支持 x86 应用开发或将 x86 应用商店提交到应用商店。 

### <a name="will-i-lose-my-games-and-apps-or-saved-changes"></a>我的游戏和应用或保存的更改是否会丢失？

如果决定退出开发人员计划，不会丢失安装的游戏和应用。 此外，只要你在玩游戏时处于联机状态，保存的游戏就全部保存在你的 Live 帐户云配置文件中，因此不会丢失它们。

### <a name="how-do-i-leave-the-developer-program"></a>如何退出开发人员计划？

有关如何退出开发人员计划的详细信息，请参阅 [Xbox One 开发人员模式停用](devkit-deactivation.md)主题。

### <a name="i-sold-my-xbox-one-and-left-it-in-developer-mode-how-do-i-deactivate-developer-mode"></a>我已出售我的 Xbox One，并且将它保留在开发人员模式下。 如何停用开发人员模式？

如果你不再能够访问你的 Xbox One，可以在 Windows 开发人员中心中停用它。 有关详细信息，请参阅 [Xbox One 开发人员模式停用](devkit-deactivation.md#deactivate-your-console-using-windows-dev-center)主题中的**使用 Windows 开发人员中心停用主机**部分。 

### <a name="i-left-the-developer-program-using-windows-dev-center-but-im-in-still-developer-mode-what-do-i-do"></a>我已使用 Windows 开发人员中心退出了开发人员计划，但我仍处于开发人员模式下。 我该怎么办？

启动“开发人员主页”，然后选择**退出开发人员模式**按钮。 这将在零售模式下重新启动主机。 

### <a name="can-i-publish-my-app"></a>我是否可以发布我的应用？

如果你有[开发者帐户](https://developer.microsoft.com/store/register)，可以通过开发人员中心[发布应用](../publish/index.md)。 在零售 Xbox One 主机上创建和测试的 UWP 应用将经过当今 Windows 执行的相同引入、审阅和发布过程，以及符合当今 Xbox One 标准的其他审阅。

### <a name="can-i-publish-my-game"></a>我是否可以发布我的游戏？

你可以在开发人员模式下使用 UWP 和你的 Xbox One，在 Xbox One 上生成和测试你的游戏。 若要发布 UWP 游戏，你必须注册 [ID@XBOX](http://www.xbox.com/Developers/id)。 
[ID@XBOX](http://www.xbox.com/Developers/id) 向开发人员提供适用于其游戏的 Xbox Live API 的完整访问权限，包括玩家分数和成就以及在设备之间畅玩多人游戏、云存储和 Xbox One 上 Xbox Live 的所有功能。 
[ID@XBOX](http://www.xbox.com/Developers/id) 还可以为需要访问 Xbox One 硬件最大潜能的游戏提供对 Xbox One 开发工具包的访问权限。

### <a name="will-the-standard-game-engines-work"></a>标准游戏引擎是否工作？

请查看此版本的[已知问题](known-issues.md)页。

### <a name="what-capabilities-and-system-resources-are-available-to-uwp-games-on-xbox-one"></a>哪些功能和系统资源将提供给 Xbox One 上的 UWP 游戏？ 

有关信息，请参阅 [Xbox One 上的 UWP 应用和游戏的系统资源](system-resource-allocation.md)。

### <a name="if-i-create-a-directx-12-uwp-game-will-it-run-on-my-xbox-one-in-developer-mode"></a>如果我创建了 DirectX 12 UWP 游戏，那么它是否可以在开发人员模式下在我的 Xbox One 上运行？

有关信息，请参阅 [Xbox One 上的 UWP 应用和游戏的系统资源](system-resource-allocation.md)。

### <a name="will-the-entire-uwp-api-surface-be-available-on-xbox"></a>在 Xbox 上整个 UWP API 图面是否可用？

请查看此版本的[已知问题](known-issues.md)页。

### <a name="fixing-deployment-failures"></a>修复部署失败

如果无法从 Visual Studio 部署你的应用，以下步骤可能有助于你修复该问题。 如果遇到问题，请通过论坛寻求帮助。

> [!NOTE]
> 必须进行用户登录才能部署应用。 如果收到 0x87e10008 错误消息，请确保已进行用户登录，然后再试一次。

如果 Visual Studio 无法连接到你的 Xbox One：

1. 请确保你在开发人员模式下（已在本页的前面部分讨论过）。
2. 确保已正确设置了你的开发电脑。 是否按照 [Xbox One 上的 UWP 应用开发入门](getting-started.md)中的*全部*指示进行操作？ 

3. 如果尚未执行此操作，请通读[开发环境设置](development-environment-setup.md)主题和 [Xbox One 工具简介](introduction-to-xbox-tools.md)主题。

4. 确保可以从你的开发电脑对你的主机 IP 地址执行“ping”操作。
  > [!NOTE]
  > 为了获得最佳部署性能，我们建议你采用有线连接方式连接你的主机。

5. 确保使用的是**调试**选项卡上的“身份验证”下拉列表中的“通用(未加密协议)”。 有关更多详细信息，请参阅[开发环境设置](development-environment-setup.md)。

<!--6. Make sure you are not hitting a PIN pairing issue; see "Visual Studio/Xbox PIN pairing failures" in the [Known Issues](known-issues.md) topic.-->

<!--
If Visual Studio can connect, but deployment is failing (for example you get this error message: "DEP0700 : Registration of the app failed.(0x80073cf9)"):

1. Make sure that your app is not installed by uninstalling it from the Collections app in the Xbox One shell. 

> **Note**&nbsp;&nbsp;Uninstalling your app from Windows Device Portal (WDP) will not resolve the issue.

2. If your issues persist, uninstall your app or game in the Collections app, leave Developer Mode, restart to Retail Mode, and then switch back to Developer Mode. 
This will clear Dev Storage.

3. If your issues persist, follow the steps above and then use **Reset and keep my games & apps** to delete any stored state on your Xbox One. 
Go to Settings > System > Console info & updates > Reset console, and select the **Reset and keep my games & apps** button.

> **Caution**&nbsp;&nbsp;Doing this will delete all saved settings on your Xbox One including wireless settings, user accounts and any game progress that has not been saved to cloud storage.

> **Caution**&nbsp;&nbsp;DO NOT select the **Reset and remove everything** button.
This will delete all of your games, apps, settings and content and deactivate Developer Mode.
-->

### <a name="if-im-building-an-app-using-htmljavascript-how-do-i-enable-gamepad-navigation"></a>如果我要使用 HTML/JavaScript 生成应用，如何启用游戏板导航？

TVHelpers 是一套 JavaScript 和 XAML/C# 示例和库，可帮助你使用 JavaScript 和 C# 生成出色的 Xbox One 和电视体验。 TVJS 是一个库，可帮助你生成适用于 Xbox One 的高级 UWP 应用。 TVJS 包括对自动控制器导航、丰富媒体播放、搜索以及更多内容的支持。 将 TVJS 用于托管的 Web 应用就像将其用于拥有对 Windows 运行时 API 的完全访问权限的打包 Web UWP 应用一样轻松。

有关详细信息，请参阅 [TVHelpers](https://github.com/Microsoft/TVHelpers) 项目和 [wiki](https://github.com/Microsoft/TVHelpers/wiki) 项目。

## <a name="see-also"></a>另请参阅
- [Xbox One 上的 UWP 的已知问题](known-issues.md)
- [Xbox One 上的 UWP](index.md)

