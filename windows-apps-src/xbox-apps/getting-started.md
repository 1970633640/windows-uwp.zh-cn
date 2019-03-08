---
title: Xbox One 上的 UWP 应用开发入门
description: 如何针对 UWP 开发设置电脑和 Xbox One。
ms.date: 10/12/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: c94d27e87853b570268e3a39fe941c817b3eda6a
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57590972"
---
# <a name="getting-started-with-uwp-app-development-on-xbox-one"></a>Xbox One 上的 UWP 应用开发入门

**注意** 遵循这些步骤以针对通用 Windows 平台 (UWP) 开发成功设置电脑和 Xbox One。 完成设置后，你可以在[适用于 Xbox One 的 UWP](index.md) 页面上了解有关 Xbox One 上的开发人员模式和生成 UWP 应用的详细信息。 

## <a name="before-you-start"></a>开始之前

在开始之前，你将需要执行以下操作：
-   设置与最新版本的 Windows 10 的 PC。
<!-- -  Install Microsoft Visual Studio 2015 Update 3 or Microsoft Visual Studio 2017.

    > [!NOTE]
    > Visual Studio 2017 is required if you are using the Windows 10, build 15063 SDK. -->

- 在 Xbox One 主机上具有至少 5 GB 的可用空间。

## <a name="setting-up-your-development-pc"></a>设置你的开发电脑

1.  安装 Visual Studio 2015 Update 3 或 Visual Studio 2017。

    如果要安装 Visual Studio 2015 Update 3，请确保你选择**自定义**安装，并选择**通用 Windows 应用开发工具**复选框 – 它不是默认值的一部分安装。 如果你是 C++ 开发人员，确保选择“自定义安装”，然后选择“C++”。

    如果要安装 Visual Studio 2017，请确保选择**通用 Windows 平台开发**工作负载。 如果您在 c + + 开发人员，**摘要**在右侧窗格下**通用 Windows 平台开发**，请确保你选择**c + + 通用 Windows 平台工具**复选框。 它不是默认安装的一部分。

    有关详细信息，请参阅[设置在 Xbox 开发环境在 UWP](development-environment-setup.md)。

2.  安装最新[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。

3.  为进行开发的电脑启用开发人员模式 (**设置 / 更新和安全 / 开发人员 / 使用开发人员功能 / 开发人员模式**)。

现在，你的开发电脑已准备就绪，可以观看此视频，或者继续阅读以了解如何设置用于开发的 Xbox One，然后创建一个 UWP 应用并部署到 Xbox One。
</br>
</br>
<iframe src="https://channel9.msdn.com/Events/Xbox/App-Dev-on-Xbox/Get-started-with-App-Dev-on-Xbox/player#time=51s:paused" width="600" height="338"  allowFullScreen frameBorder="0"></iframe>

## <a name="setting-up-your-xbox-one-console"></a>设置 Xbox One 主机

1.  在 Xbox One 上激活开发人员模式。 下载应用，获取激活代码，然后输入到**管理 Xbox One 控制台**在合作伙伴中心应用程序开发人员帐户中的页。 有关详细信息，请参阅 [Xbox One 开发人员模式激活](devkit-activation.md)。 

2.  打开**开发人员模式下激活**应用，然后选择**交换机和重启**。 恭喜，你现在具有处于开发人员模式下的 Xbox One！
  
  > [!NOTE]
  > 你的零售游戏和应用不会在开发人员模式下运行，但你创建的应用或游戏会在该模式下运行。 切换回零售模式以运行你最喜爱的游戏和应用。
    
  > [!NOTE]
  > 必须先在该主机上进行用户登录，然后才能在开发人员模式下将应用部署到你的 Xbox One。 可以使用你的现有 Xbox Live 帐户，也可以在开发人员模式下为你的主机创建新帐户。 

## <a name="creating-your-first-project-in-visual-studio"></a>在 Visual Studio 中创建第一个项目

有关详细信息，请参阅[设置在 Xbox 开发环境在 UWP](development-environment-setup.md)。

1.  **有关C#** :创建新的通用 Windows 项目，然后在**解决方案资源管理器**，右键单击该项目并选择**属性**。 选择**调试**选项卡上，更改**目标设备**到**远程计算机**，键入 IP 地址或主机名到 Xbox One 控制台**远程计算机**字段，然后选择**世界 （未加密的协议）** 中**身份验证模式**下拉列表。   

    你可以通过在主机上启动“开发人员主页”（“主页”右侧的大磁贴）并查看左上角找到你的 Xbox One IP 地址。 有关开发人员主页的详细信息，请参阅 [Xbox One 工具简介](introduction-to-xbox-tools.md)。  

2.  **对于 c + + 和 HTML/Javascript 项目**:遵循一个类似于路径C#项目，但在项目属性中转到**调试**选项卡上，选择**远程计算机**在调试器中，打开下拉列表，键入 IP 地址或主机名到控制台**计算机名称**字段，然后选择**通用 （未加密的协议）** 中**身份验证类型**字段。

3. 选择**x64**从顶部菜单栏中的绿色播放按钮左侧的下拉列表。
   
4.  按 F5 后，你的应用将生成并开始在 Xbox One 上部署。
  
5.  第一次执行此操作时，Visual Studio 将提示你为 Xbox One 输入 PIN。 可以通过在 Xbox One 上启动 Dev 主页并选择获取 PIN**显示 Visual Studio pin**按钮。
  
6.  在配对后，你的应用将开始部署。 第一次执行此操作时可能有点慢（我们将所有工具复制到 Xbox），但是如果它不只需要几分钟，则可能出现了某些错误。 请确保你已遵循以上所有步骤（尤其是你是否已将“身份验证模式”设置为“通用”？），并且你正在使用与 Xbox One 的有线网络连接。  

7. 坐下来放松。 享受你的第一个在主机上运行的应用！  

## <a name="thats-it"></a>就这么简单！

![Hello World](images/getting-started-hello-world.png)

## <a name="see-also"></a>另请参阅  
- [常见问题](frequently-asked-questions.md)  
- [在 Xbox 开发人员计划上的 UWP 的已知的问题](known-issues.md)
- [在 Xbox One 上 UWP](index.md) 
