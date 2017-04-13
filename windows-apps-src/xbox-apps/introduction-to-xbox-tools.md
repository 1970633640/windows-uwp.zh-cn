---
author: Mtoepke
title: "Xbox One 工具简介"
description: "特定于 Xbox One 且使用 Windows Device Portal 的工具“开发人员主页”。"
ms.author: mtoepke
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.assetid: 6eaf376f-0d7c-49de-ad78-38e689b43658
ms.openlocfilehash: 536502316db43ccc04a42b935064294dc5173151
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="introduction-to-xbox-one-tools"></a>Xbox One 工具简介

本部分介绍了特定于 Xbox One 且使用 Windows Device Portal 的工具“开发人员主页”__。

## <a name="dev-home"></a>开发人员主页

“开发人员主页”__是 Xbox One 开发工具包上旨在提高开发人员工作效率的工具体验。 “开发人员主页”提供管理和配置开发人员工具包的功能。

若要打开“开发人员主页”，请在主屏幕上选择“开发人员主页”****磁贴。 如果不存在任何磁贴，则控制台不处于开发人员模式中。

  ![Windows Device Portal](images/windowsdeviceportal_1.png)

### <a name="user-interface"></a>用户界面
“开发人员主页”用户界面分为在以下部分中介绍的几个区域。 请注意，主机 IP 地址和友好名称在此处显示。

  ![DevHome UI](images/devhome_ui.png)

#### <a name="header"></a>标题
标题包含关于开发人员工具包的重要“一览”信息。 这包括控制台名称、它的 IP 地址、所在的 Xbox Live 沙盒以及它正在运行的操作系统版本。 在标题右侧，为方便起见显示了当前系统时间和日期。

#### <a name="tool-windows"></a>工具窗口
标题下面是应用的主区域，其中包括一组可配置的工具窗口。 这些窗口旨在支持开发人员自定义应用以提供对各种工具和信息集的访问权限。 有关工具的更多详细信息，请参阅以下个别工具描述。 有关如何配置工具窗口布局和外观的信息，请参阅本页后面的[自定义开发人员主页](#customizing-dev-home)部分。

#### <a name="main-menu"></a>主菜单
通过按控制器上的“菜单”****按钮或导航到屏幕左上方的菜单（“汉堡包”）按钮，你可以访问支持配置应用工作区的主题色和背景图的主菜单，并提供有关应用的反馈。

  ![主菜单](images/devhome_mainmenu.png)

#### <a name="snap-mode"></a>贴靠模式
开发人员主页中的工具可以在运行标题时贴靠到一侧，以便你可以在进行测试时轻松访问工具。

若要访问**贴靠**模式，请选择相应工具的标题、在控制器上按“视图”****按钮，并在上下文菜单中选择“贴靠”****。

  ![贴靠模式](images/devhome_snapmode.png)

开发人员主页将贴靠到右侧。 你可以通过像往常那样双击 **Nexus** 按钮来切换上下文。

  ![Nexus](images/devhome_nexus.png)

#### <a name="tool-descriptions"></a>工具描述
| 工具    | 功能 |
|-------|--------------|
| 游戏和应用    | 列出在开发人员工具包中安装的标题和应用以及快速打开它们的功能。 你还可以查看游戏和应用的进程周期管理 (PLM) 状态，并在上下文菜单中更改 PLM 状态。 |
| 用户    | 列出当前在控制台上注册的用户。 支持用户一键登录/注销、添加用户和来宾，以及查看用户和来宾的详细信息。 |
| [控制台设置](#console-settings) | 提供“一览”视图以及控制台设置和信息的编辑选项。 |
| Visual Studio | 能让你将控制台与 Visual Studio 实例配对，以支持部署。 如有必要，清除所有现有的已配对 VS 实例以防止将 UWP 应用部署到工具包。 |
| [Windows Device Portal](#windows-device-portal) |    在工具包上支持 WDP（基于浏览器的设备管理工具）。 |
| Xbox Live 状态 | 提供 Xbox Live 服务的当前状态。 |
<br/>
### <a name="managing-the-size-of-the-developer-storage-allocation"></a>管理开发人员存储分配的大小

若要增大或减小用于开发人员存储的磁盘空间量，请从主菜单中选择“管理开发人员存储”****。 更改“开发人员存储”****栏的值，然后选择“保存并重新启动”****重新启动主机。

  ![管理开发人员存储分配](images/devhome_storage.png)

### <a name="customizing-dev-home"></a>自定义开发人员主页

开发人员主页已设计为可自定义，并且具有个性化。 你可以选择背景图和主题色来个性化你的开发人员主页体验。 这些选项可以在主菜单上找到。

#### <a name="resizing-and-reordering-tools"></a>调整工具大小和对其重新排序
若要更改工具的大小或位置，请在标题有焦点时使用上下文菜单按钮（控制器上的“视图”****按钮）。 在上下文菜单上，选择“移动”****或“调整大小”****。

  ![移动或调整大小](images/devhome_move.png)

#### <a name="changing-theme-color-and-background-image"></a>更改主题色和背景图
在主菜单上，你可以选择“更改主题色”****。 若要更新用于焦点突出显示的主题色，选择一种新颜色，然后单击“保存”****。

  ![更改主题色](images/devhome_colors.png)

### <a name="providing-feedback"></a>提供反馈
若要提供有关开发人员主页或任何工具进程的反馈，请在主菜单上选择**“提供反馈”**选项。

  ![提供反馈](images/devhome_feedback.png)

## <a name="console-settings"></a>控制台设置
控制台设置工具可快速访问开发人员工具包的设置。

### <a name="setting-a-hostname-for-the-console"></a>设置控制台的主机名
在开发电脑上与控制台通信时，可以为 Xbox One 开发人员工具包设置友好名称（称为_“主机名”_）以用作控制台 IP 地址的替代项。 开发电脑和开发人员工具包必须位于相同子网上才能让主机名连接正常工作。  

若要定义一个开发工具包的主机名，请转到主机设置工具，并在“主机名”____框中键入主机名。  

> [!NOTE]
> 创建主机名时，不需要该名称是唯一名称。 请注意避免名称重复。 达到此目的的一种方法是从开发计算机名称中派生主机名，开发计算机名称通常在组织中是唯一的。

## <a name="windows-device-portal"></a>Windows Device Portal
Windows Device Portal (WDP) 是提供基于浏览器的设备管理体验的 OneCore 设备管理工具。

> [!NOTE]
> 有关 WDP 的详细信息，请参阅 [Windows Device Portal 概述](../debug-test-perf/device-portal.md)。

若要在 Xbox One 控制台上启用 WDP：

1. 在主屏幕上选择“开发人员主页”磁贴。

  ![选择“开发人员主页”磁贴](images/windowsdeviceportal_1.png)

2. 在“开发人员主页”中，导航到“远程管理”****工具。

  ![远程管理工具](images/windowsdeviceportal_2.png)

3. 选择“管理 Windows Device Portal”____，然后按 __A__。
4. 选中“启用 Windows Device Portal”____复选框。
5. 输入__用户名__和__密码__，然后进行保存。 它们用于验证浏览器对开发人员工具包的访问权限。
6. 关闭“设置”____页面，并记下“远程管理”__工具上列出的要连接的 URL。
7. 在浏览器中输入 URL，然后使用已配置的凭据登录。
8. 你将收到已提供证书的警告（类似于以下屏幕截图），因为 Xbox One 控制台签名的安全证书不被视为众所周知的受信任发布者。 单击“继续浏览此网站”****可访问 Windows Device Portal。

  ![安全证书警告](images/security_cert_warning.jpg)

## <a name="xbox-dev-mode-companion"></a>Xbox 开发人员模式助手
Xbox 开发人员模式助手是一个工具，使你无需离开电脑就可以在你的主机上工作。 该应用使你可以查看主机屏幕以及向主机发送输入。 有关详细信息，请参阅 [Xbox 开发人员模式助手](xbox-dev-mode-companion.md)。

## <a name="see-also"></a>另请参阅
- [在针对 UWP 进行开发时如何将 Fiddler 用于 Xbox One](uwp-fiddler.md)
- [Windows Device Portal 概述](../debug-test-perf/device-portal.md)
- [Xbox One 上的 UWP](index.md)


----
