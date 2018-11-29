---
ms.assetid: 4e7c2388-b94e-4828-a104-14fa33f6eb2d
description: 了解如何使用 AdControl 类在适用于 Windows10 (UWP) 的 XAML 应用中显示横幅广告。
title: XAML 和 .NET 中的 AdControl
ms.date: 03/22/2018
ms.topic: article
keywords: Windows 10, uwp, 广告, AdControl, 广告控件, XAML, .net, 演练
ms.localizationpriority: medium
ms.openlocfilehash: 161718bb88d7588db345f3de26de2a955ca6620e
ms.sourcegitcommit: b5c9c18e70625ab770946b8243f3465ee1013184
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "7980325"
---
# <a name="adcontrol-in-xaml-and-net"></a>XAML 和 .NET 中的 AdControl


本演练介绍如何使用 [AdControl](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol) 类在适用于 Windows 10（使用 C# 实现）的通用 Windows 平台 (UWP) XAML 应用中显示横幅广告。

> [!NOTE]
> Microsoft 广告 SDK 还支持使用 C++ 实现的 XAML 应用。 有关完整示例项目，请参阅 [GitHub 上的广告示例](http://aka.ms/githubads)。

## <a name="prerequisites"></a>先决条件

* 使用 Visual Studio 2015 或更高版本的 Visual Studio 安装 [Microsoft 广告 SDK](http://aka.ms/ads-sdk-uwp)。 有关安装说明，请参阅[此文章](install-the-microsoft-advertising-libraries.md)。

## <a name="integrate-a-banner-ad-into-your-app"></a>在应用中集成横幅广告

1. 在 Visual Studio 中，打开项目或创建新项目。

    > [!NOTE]
    > 如果你使用现有项目，请打开项目中的 Package.appxmanifest 文件并确保已选择 **Internet（客户端）** 功能。 应用需要使用此功能接收测试广告和实时广告。

2. 如果你的项目面向**任何 CPU**，请更新你的项目以使用特定于体系结构的生成输出（例如，**x86**）。 如果你的项目面向**任何 CPU**，你将无法在以下步骤中成功添加对 Microsoft Advertising 库的引用。 有关详细信息，请参阅[项目中由面向任何 CPU 引起的引用错误](known-issues-for-the-advertising-libraries.md#reference_errors)。

3. 在你的项目中添加对 Microsoft 广告 SDK 的引用：

    1. 在**解决方案资源管理器**窗口中，右键单击**引用**，然后选择**添加引用...**
    2.  在**引用管理器**中，展开**通用 Windows**、单击**扩展**，然后选中**适用于 XAML 的 Microsoft 广告 SDK**（版本 10.0）旁边的复选框。
    3.  在**引用管理器**中，单击“确定”。

4.  修改你要在其中嵌入广告的页面的 XAML，以包含 **Microsoft.Advertising.WinRT.UI** 命名空间。 例如，在由 Visual Studio 生成的默认示例应用中（即，在应用 MyAdFundedWindows10AppXAML 中），XAML 页面是 **MainPage.XAML**。

    由 Visual Studio 生成的 MainPage.xaml 文件的**页面**部分具有以下代码。

    ``` xml
    <Page
      x:Class="MyAdFundedWindows10AppXAML.MainPage"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:local="using:MyAdFundedWindows10AppXAML"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      mc:Ignorable="d">
      <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
      </Grid>
    </Page>
    ```

    添加命名空间引用 **Microsoft.Advertising.WinRT.UI**，以使 MainPage.xaml 文件的**页面**部分具有以下代码。

    ``` xml
    <Page
      x:Class="MyAdFundedWindows10AppXAML.MainPage"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:local="using:MyAdFundedWindows10AppXAML"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      xmlns:UI="using:Microsoft.Advertising.WinRT.UI"
      mc:Ignorable="d">
      <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
      </Grid>
    </Page>
    ```

5. 在**网格**标记中，为 **AdControl** 添加代码。 将 [AdUnitId](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.adunitid) 和 [ApplicationId](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.applicationid) 属性分配至[测试广告单元值](set-up-ad-units-in-your-app.md#test-ad-units)。 另外还要调整控件的**高度**和**宽度**，以使其适应[横幅广告支持的广告大小](supported-ad-sizes-for-banner-ads.md)。

    > [!NOTE]
    > 每个 **AdControl** 都有一个对应的*广告单元*，我们的服务使用该广告单元来为控件提供广告，每个广告单元都包含*单元 ID* 和*应用程序 ID*。 在这些步骤中，你将为控件分配测试广告单元 ID 和应用程序 ID 值。 这些测试值只能在应用的测试版本中使用。 将应用发布到应用商店之前，必须[替换这些测试值的实时值](#release)合作伙伴中心中。

    完整的**网格**标记应类似如下代码。

    ``` xml
    <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <UI:AdControl ApplicationId="3f83fe91-d6be-434d-a0ae-7351c5a997f1"
            AdUnitId="test"
            HorizontalAlignment="Left"
            Height="250"
            VerticalAlignment="Top"
            Width="300"/>
    </Grid>
    ```

    MainPage.xaml 文件的完整代码应如下所示。

    ``` xml
    <Page
      x:Class="MyAdFundedWindows10AppXAML.MainPage"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:local="using:MyAdFundedWindows10AppXAML"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      xmlns:UI="using:Microsoft.Advertising.WinRT.UI"
      mc:Ignorable="d">
      <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <UI:AdControl ApplicationId="3f83fe91-d6be-434d-a0ae-7351c5a997f1"
                  AdUnitId="test"
                  HorizontalAlignment="Left"
                  Height="250"
                  VerticalAlignment="Top"
                  Width="300"/>
      </Grid>
    </Page>
    ```

6.  编译并运行应用以查看是否带有广告。

<span id="release" />

## <a name="release-your-app-with-live-ads"></a>发布包含实时广告的应用

1. 确保在应用中对横幅广告的使用遵循我们的[横幅广告指南](ui-and-user-experience-guidelines.md#guidelines-for-banner-ads)。

2.  在合作伙伴中心中，转到[应用内广告](../publish/in-app-ads.md)页和[创建广告单元](set-up-ad-units-in-your-app.md#live-ad-units)。 对于广告单元类型，请指定**横幅**。 记下广告单元 ID 和应用程序 ID。
    > [!NOTE]
    > 测试广告单元和实时 UWP 广告单元的应用程序 ID 值采用不同的格式。 测试应用程序 ID 值为 GUID。 在合作伙伴中心中创建实时 UWP 广告单元时，广告单元的应用程序 ID 值始终与应用商店 ID 为你的应用 （示例应用商店 ID 值类似于 9NBLGGH4R315） 匹配。

3. 你可以选择通过配置[中介设置](../publish/in-app-ads.md#mediation)部分（位于[应用内广告](../publish/in-app-ads.md)页面上）的设置为 **AdControl** 启用广告中介。 广告中介显示来自多个广告网络（包括其他付费广告网络，如 Taboola 和 Smaato）的广告及 Microsoft 应用促销活动的广告，从而使你能够最大化你的广告收益和应用促销能力。

4.  在代码中，将测试广告单元值 （**ApplicationId**和**AdUnitId**） 替换在合作伙伴中心中生成的实时值。

5.  [你的应用提交](../publish/app-submissions.md)到应用商店使用合作伙伴中心。

6.  查看你在合作伙伴中心中的[广告性能报告](../publish/advertising-performance-report.md)。

<span id="manage" />

## <a name="manage-ad-units-for-multiple-ad-controls-in-your-app"></a>管理你的应用中多个广告控件的广告单元

可在一个应用中使用多个 **AdControl** 对象（例如，应用中的每页可以托管不同的 **AdControl** 对象）。 在此情况下，我们建议你为每个控件分配不同的广告单元。 对每个控件使用不同的广告单元使你可以分别[配置中介设置](../publish/in-app-ads.md#mediation)并获取每个控件的独立[报告数据](../publish/advertising-performance-report.md)。 这还使我们的服务能够更好地优化我们为你的应用提供的广告。

> [!IMPORTANT]
> 每个广告单元都只能在一个应用中使用。 如果在多个应用中使用某个广告单元，将不为该广告单元提供广告。

## <a name="related-topics"></a>相关主题

* [横幅广告指南](ui-and-user-experience-guidelines.md#guidelines-for-banner-ads)
* [XAML/C# 演练中的错误处理](error-handling-in-xamlc-walkthrough.md)。
* [GitHub 上的广告示例](http://aka.ms/githubads)
* [为应用设置广告单元](set-up-ad-units-in-your-app.md)
