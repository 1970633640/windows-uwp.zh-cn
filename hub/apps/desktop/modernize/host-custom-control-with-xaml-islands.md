---
description: 本文演示如何使用 XAML 孤岛在 WPF 应用程序中托管自定义 UWP 控件。
title: 使用 XAML 孤岛在 WPF 应用程序中托管自定义 UWP 控件
ms.date: 01/24/2020
ms.topic: article
keywords: windows 10、uwp、windows 窗体、wpf、xaml 孤岛、自定义控件、用户控件、宿主控件
ms.author: mcleans
author: mcleanbyron
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d881fc42e453e2ace0a44543c3e204aa154958b7
ms.sourcegitcommit: ca1b5c3ab905ebc6a5b597145a762e2c170a0d1c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79209793"
---
# <a name="host-a-custom-uwp-control-in-a-wpf-app-using-xaml-islands"></a>使用 XAML 孤岛在 WPF 应用程序中托管自定义 UWP 控件

本文演示如何使用 Windows 社区工具包中的[WindowsXamlHost](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/windowsxamlhost)控件在面向 .net Core 3 的 WPF 应用程序中托管自定义 UWP 控件。 自定义控件包含来自 Windows SDK 的多个第一方 UWP 控件，并将其中一个 UWP 控件中的属性绑定到 WPF 应用程序中的字符串。 本文还演示了如何从[WinUI 库](https://docs.microsoft.com/uwp/toolkits/winui/)承载第一方 UWP 控件。

尽管本文演示了如何在 WPF 应用程序中执行此操作，但此过程与 Windows 窗体应用程序类似。 有关在 WPF 中承载 UWP 控件和 Windows 窗体应用的概述，请参阅[此文](xaml-islands.md#wpf-and-windows-forms-applications)。

## <a name="required-components"></a>所需的组件

若要在 WPF （或 Windows 窗体）应用程序中托管自定义 UWP 控件，你的解决方案中将需要以下组件。 本文提供了有关创建每个组件的说明。

* **应用程序的项目和源代码**。 只有面向 .NET Core 3 的应用才支持使用[WindowsXamlHost](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/windowsxamlhost)控件托管自定义 UWP 控件。 面向 .NET Framework 的应用不支持此方案。

* **自定义 UWP 控件**。 你需要承载自定义 UWP 控件的源代码，以便可以将其与你的应用进行编译。 通常，自定义控件在与 WPF 或 Windows 窗体项目相同的解决方案中引用的 UWP 类库项目中定义。

* **一个 UWP 应用项目，用于定义从 XamlApplication 派生的根应用程序类**。 WPF 或 Windows 窗体项目必须有权访问 Windows 社区工具包提供的[XamlApplication](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/master/Microsoft.Toolkit.Win32.UI.XamlApplication)类的 XamlHost 类实例的访问权限。 执行此操作的建议方法是在单独的 UWP 应用项目中定义此对象，该项目是适用于 WPF 或 Windows 窗体应用的解决方案的一部分。 此对象用作根元数据提供程序，用于为应用程序的当前目录中的程序集中的自定义 UWP XAML 类型加载元数据。

    > [!NOTE]
    > 你的解决方案只能包含一个定义 `XamlApplication` 对象的项目。 应用中的所有自定义 UWP 控件共享相同的 `XamlApplication` 对象。 定义 `XamlApplication` 对象的项目必须包含对 XAML 岛上用于 UWP 控件的所有其他 UWP 库和项目的引用。

## <a name="create-a-wpf-project"></a>创建 WPF 项目

在开始之前，请按照以下说明创建 WPF 项目，并将其配置为承载 XAML 孤岛。 如果你有现有 WPF 项目，则可以修改项目的这些步骤和代码示例。

> [!NOTE]
> 如果有一个面向 .NET Framework 的现有项目，则需要将项目迁移到 .NET Core 3。 有关详细信息，请参阅[此博客系列](https://devblogs.microsoft.com/dotnet/migrating-a-sample-wpf-app-to-net-core-3-part-1/)。

1. 如果尚未这样做，请安装最新版本的[.Net Core 3 SDK](https://dotnet.microsoft.com/download/dotnet-core/3.0)。

2. 在 Visual Studio 2019 中，创建一个新的**WPF 应用程序（.Net Core）** 项目。

3. 确保启用[包引用](https://docs.microsoft.com/nuget/consume-packages/package-references-in-project-files)：

    1. 在 Visual Studio 中，单击 "**工具"-> "NuGet 包管理器-> 包管理器设置**"。
    2. 请确保已为**默认包管理格式**选择**PackageReference** 。

4. 在**解决方案资源管理器**中右键单击 WPF 项目，然后选择 "**管理 NuGet 包**"。

5. 在 " **NuGet 包管理器**" 窗口中，确保选择 "**包括预发行**版"。

6. 选择 "**浏览**" 选项卡，搜索[XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.XamlHost)包（版本 v 6.0.0 或更高版本），然后安装包。 此包提供了使用**WindowsXamlHost**控件承载 UWP 控件所需的所有内容，包括其他相关的 NuGet 包。
    > [!NOTE]
    > Windows 窗体应用必须使用[XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.XamlHost)包（版本 v 6.0.0 或更高版本）。

7. 配置解决方案以面向特定的平台，例如 x86 或 x64。 对于以**任何 CPU**为目标的项目，不支持自定义 UWP 控件。

    1. 在**解决方案资源管理器**中，右键单击 "解决方案" 节点，然后选择 "**属性**" " -> **配置属性**" -> **Configuration Manager**"。
    2. 在 "**活动解决方案平台**" 下，选择 "**新建**"。 
    3. 在 "**新建解决方案平台**" 对话框中，选择 " **X64**或**X86** "，并按 **"确定"** 。 
    4. 关闭 "打开" 对话框。

## <a name="define-a-xamlapplication-class-in-a-uwp-app-project"></a>在 UWP 应用项目中定义 XamlApplication 类

接下来，将 UWP 应用项目添加到解决方案，并将此项目中的默认 `App` 类修改为派生自 Windows 社区工具包提供的[XamlHost. XamlApplication](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/master/Microsoft.Toolkit.Win32.UI.XamlApplication)类。 您的应用程序将使用此类作为根元数据提供程序，以便为您的应用程序的当前目录中的程序集中的自定义 UWP XAML 类型加载元数据。

1. 在**解决方案资源管理器**中，右键单击 "解决方案" 节点，然后选择 "**添加** -> "**新建项目**"。
2. 向你的解决方案中添加一个**空白应用（通用 Windows）** 项目。 请确保目标版本和最低版本均设置为**Windows 10 1903 版**或更高版本。
3. 在 UWP 应用项目中，安装[XamlApplication](https://www.nuget.org/packages/Microsoft.Toolkit.Win32.UI.XamlApplication) NuGet 包（版本 v 6.0.0 或更高版本）。
4. 打开**app.config**文件，并将此文件的内容替换为以下 xaml。 将 `MyUWPApp` 替换为 UWP 应用项目的命名空间。

    ```xml
    <xaml:XamlApplication
        x:Class="MyUWPApp.App"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:xaml="using:Microsoft.Toolkit.Win32.UI.XamlHost"
        xmlns:local="using:MyUWPApp">
    </xaml:XamlApplication>
    ```

5. 打开**App.xaml.cs**文件，并将此文件的内容替换为以下代码。 将 `MyUWPApp` 替换为 UWP 应用项目的命名空间。

    ```csharp
    namespace MyUWPApp
    {
        public sealed partial class App : Microsoft.Toolkit.Win32.UI.XamlHost.XamlApplication
        {
            public App()
            {
                this.Initialize();
            }
        }
    }
    ```

6. 从 UWP 应用项目中删除**MainPage**文件。
7. 清除 UWP 应用项目，然后生成该项目。
8. 在 WPF 项目中，右键单击 "**依赖项**" 节点，并添加对 UWP 应用项目的引用。

## <a name="instantiate-the-xamlapplication-object-in-the-entry-point-of-your-wpf-app"></a>在 WPF 应用程序的入口点实例化 XamlApplication 对象

接下来，将代码添加到 WPF 应用程序的入口点，以创建刚在 UWP 项目中定义的 `App` 类的实例（这是现在派生自 `XamlApplication`的类）。 此对象用作根元数据提供程序，用于为应用程序的当前目录中的程序集中的自定义 UWP XAML 类型加载元数据。

1. 在 WPF 项目中，右键单击项目节点，选择 "**添加** -> **新项**"，然后选择 "**类**"。 命名类**程序**，然后单击 "**添加**"。

2. 将生成的 `Program` 类替换为以下代码，然后保存该文件。 将 `MyUWPApp` 替换为 UWP 应用项目的命名空间，并将 `MyWPFApp` 替换为您的 WPF 应用程序项目的命名空间。

    ```csharp
    public class Program
    {
        [System.STAThreadAttribute()]
        public static void Main()
        {
            using (new MyUWPApp.App())
            {
                MyWPFApp.App app = new MyWPFApp.App();
                app.InitializeComponent();
                app.Run();
            }
        }
    }
    ```

3. 右键单击项目节点，然后选择 "**属性**"。

4. 在 "属性" 的 "**应用程序**" 选项卡上，单击 "**启动对象**" 下拉箭头，然后选择在上一步中添加的 `Program` 类的完全限定名称。 
    > [!NOTE]
    > 默认情况下，WPF 项目会在生成的代码文件中定义一个 `Main` 入口点函数，而不应进行修改。 此步骤会将项目的入口点更改为新 `Program` 类的 `Main` 方法，这使你能够添加在应用程序启动过程早期运行的代码。 

5. 保存对项目属性所做的更改。

## <a name="create-a-custom-uwp-control"></a>创建自定义 UWP 控件

若要在 WPF 应用程序中托管自定义 UWP 控件，你必须具有控件的源代码，以便可以使用你的应用进行编译。 自定义控件通常是在 UWP 类库项目中定义的，以方便实现可移植性。

在本部分中，将在新的类库项目中定义一个简单的自定义 UWP 控件。 您也可以在上一节中创建的 UWP 应用项目中定义自定义 UWP 控件。 不过，这些步骤在单独的类库项目中执行此操作是为了便于演示，因为这通常是实现自定义控件以实现可移植性的方式。

如果已经有一个自定义控件，则可以使用它，而不是此处所示的控件。 但是，您仍需要配置包含该控件的项目，如以下步骤所示。

1. 在**解决方案资源管理器**中，右键单击 "解决方案" 节点，然后选择 "**添加** -> "**新建项目**"。
2. 将**类库（通用 Windows）** 项目添加到解决方案。 请确保目标版本和最低版本均设置为**Windows 10 1903 版**或更高版本。
3. 右键单击项目文件，然后选择 "**卸载项目**"。 再次右键单击项目文件，然后选择 "**编辑**"。
4. 在关闭 `</Project>` 元素之前，添加以下 XML 以禁用多个属性，然后保存该项目文件。 必须启用这些属性才能在 WPF （或 Windows 窗体）应用程序中托管自定义 UWP 控件。

    ```xml
    <PropertyGroup>
      <EnableTypeInfoReflection>false</EnableTypeInfoReflection>
      <EnableXBindDiagnostics>false</EnableXBindDiagnostics>
    </PropertyGroup>
    ```

5. 右键单击项目文件，然后选择 "**重新加载项目**"。
6. 删除默认的**Class1.cs**文件，并向项目中添加新的**用户控件**项。
7. 在用户控件的 XAML 文件中，添加以下 `StackPanel` 作为默认 `Grid`的子元素。 此示例将添加一个 ``TextBlock`` 控件，然后将该控件的 ``Text`` 特性绑定到 ``XamlIslandMessage`` 字段。

    ```xml
    <StackPanel Background="LightCoral">
        <TextBlock>This is a simple custom UWP control</TextBlock>
        <Rectangle Fill="Blue" Height="100" Width="100"/>
        <TextBlock Text="{x:Bind XamlIslandMessage}" FontSize="50"></TextBlock>
    </StackPanel>
    ```

8. 在用户控件的代码隐藏文件中，将 `XamlIslandMessage` 字段添加到用户控件类，如下所示。

    ```csharp
    public sealed partial class MyUserControl : UserControl
    {
        public string XamlIslandMessage { get; set; }

        public MyUserControl()
        {
            this.InitializeComponent();
        }
    }
    ```

9. 生成 UWP 类库项目。
10. 在 WPF 项目中，右键单击 "**依赖项**" 节点，并添加对 UWP 类库项目的引用。
11. 在之前配置的 UWP 应用项目中，右键单击 "**引用**" 节点，然后添加对 UWP 类库项目的引用。
12. 重新生成整个解决方案并确保所有项目都已成功生成。

## <a name="host-the-custom-uwp-control-in-your-wpf-app"></a>在 WPF 应用程序中托管自定义 UWP 控件

1. 在**解决方案资源管理器**中，展开 WPF 项目，然后打开 mainwindow.xaml 文件或您要在其中承载自定义控件的其他窗口。
2. 在 XAML 文件中，将以下命名空间声明添加到 `<Window>` 元素。

    ```xml
    xmlns:xaml="clr-namespace:Microsoft.Toolkit.Wpf.UI.XamlHost;assembly=Microsoft.Toolkit.Wpf.UI.XamlHost"
    ```

3. 在同一文件中，将以下控件添加到 `<Grid>` 元素。 将 `InitialTypeName` 特性更改为 UWP 类库项目中的用户控件的完全限定名称。

    ```xml
    <xaml:WindowsXamlHost InitialTypeName="UWPClassLibrary.MyUserControl" ChildChanged="WindowsXamlHost_ChildChanged" />
    ```

4. 打开代码隐藏文件，并将以下代码添加到 `Window` 类。 此代码定义 `ChildChanged` 事件处理程序，该处理程序将 UWP 自定义控件 ``XamlIslandMessage`` 字段的值分配给 WPF 应用程序中的 `WPFMessage` 字段的值。 将 `UWPClassLibrary.MyUserControl` 更改为 UWP 类库项目中的用户控件的完全限定名称。

    ```csharp
    private void WindowsXamlHost_ChildChanged(object sender, EventArgs e)
    {
        // Hook up x:Bind source.
        global::Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost windowsXamlHost =
            sender as global::Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost;
        global::UWPClassLibrary.MyUserControl userControl =
            windowsXamlHost.GetUwpInternalObject() as global::UWPClassLibrary.MyUserControl;

        if (userControl != null)
        {
            userControl.XamlIslandMessage = this.WPFMessage;
        }
    }

    public string WPFMessage
    {
        get
        {
            return "Binding from WPF to UWP XAML";
        }
    }
    ```

6. 生成并运行应用，并确认 UWP 用户控件按预期显示。

## <a name="add-a-control-from-the-winui-library-to-the-custom-control"></a>将 WinUI 库中的控件添加到自定义控件

在传统上，UWP 控件已作为 Windows 10 操作系统的一部分发布，并通过 Windows SDK 向开发人员提供。 [WinUI 库](https://docs.microsoft.com/uwp/toolkits/winui/)是一种替代方法，在此方法中，Windows SDK 中第一方 UWP 控件的更新版本分发到未绑定到 Windows SDK 版本的 NuGet 包中。 此库还包括不属于 Windows SDK 和默认 UWP 平台的新控件。 有关更多详细信息，请参阅我们的[WinUI 库路线图](https://github.com/microsoft/microsoft-ui-xaml/blob/master/docs/roadmap.md)。

本部分演示如何将 WinUI 库中的 UWP 控件添加到用户控件，以便可以在 WPF 应用程序中承载此控件。

1. 在 UWP 应用项目中，安装最新版本的[Microsoft. UI](https://www.nuget.org/packages/Microsoft.UI.Xaml) NuGet 包。

2. 在此项目的 App.config 文件中，将以下子元素添加到 `<xaml:XamlApplication>` 元素。

    ```xml
    <Application.Resources>
        <XamlControlsResources xmlns="using:Microsoft.UI.Xaml.Controls" />
    </Application.Resources>
    ```

    添加此元素后，此文件的内容现在应如下所示。

    ```xml
    <xaml:XamlApplication
        x:Class="MyUWPApp.App"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:xaml="using:Microsoft.Toolkit.Win32.UI.XamlHost"
        xmlns:local="using:MyUWPApp">
        <Application.Resources>
            <XamlControlsResources xmlns="using:Microsoft.UI.Xaml.Controls" />
        </Application.Resources>
    </xaml:XamlApplication>
    ```

3. 在 UWP 类库项目中，安装最新版本的[Microsoft. UI](https://www.nuget.org/packages/Microsoft.UI.Xaml) NuGet 包（在 UWP 应用项目中安装的版本相同）。

4. 在同一项目中，打开用户控件的 XAML 文件，并将以下命名空间声明添加到 `<UserControl>` 元素。

    ```xml
    xmlns:winui="using:Microsoft.UI.Xaml.Controls"
    ```

5. 在同一文件中，添加一个 `<winui:RatingControl />` 元素作为 `<StackPanel>`的子元素。 此元素从 WinUI 库添加[RatingControl](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.ratingcontrol?view=winui-2.2)类的实例。 添加此元素后，`<StackPanel>` 现在应如下所示。

    ```xml
    <StackPanel Background="LightCoral">
        <TextBlock>This is a simple custom UWP control</TextBlock>
        <Rectangle Fill="Blue" Height="100" Width="100"/>
        <TextBlock Text="{x:Bind XamlIslandMessage}" FontSize="50"></TextBlock>
        <winui:RatingControl />
    </StackPanel>
    ```

6. 生成并运行应用，并确认新的评级控件按预期方式显示。

## <a name="package-the-app"></a>打包应用程序

可以选择将 WPF 应用打包在[.msix 包](https://docs.microsoft.com/windows/msix)中进行部署。 .MSIX 是适用于 Windows 的新式应用打包技术，它基于 MSI、.appx、App-v 和 ClickOnce 安装技术的组合。

以下说明介绍了如何使用 Visual Studio 2019 中的[Windows 应用程序打包项目](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-packaging-dot-net)将解决方案中的所有组件打包到 .msix 包中。 仅当要将 WPF 应用打包到 .MSIX 包时，才需要执行这些步骤。 请注意，这些步骤当前包括特定于托管自定义 UWP 控件的方案的一些解决方法。

1. 向解决方案添加新的[Windows 应用程序打包项目](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-packaging-dot-net)。 创建项目时，请选择 " **Windows 10，版本1903（10.0;版本18362）** 用于**目标版本**和**最低版本**。

2. 在打包项目中，右键单击 "**应用程序**" 节点，然后选择 "**添加引用**"。 在项目列表中，选择解决方案中的 WPF 项目，然后单击 **"确定"** 。

3. 编辑 WPF 项目文件。 这些更改当前是打包自定义 UWP 控件的 WPF 应用程序所必需的。

    1. 在解决方案资源管理器中，右键单击 WPF 项目节点，然后选择 "**卸载项目**"。
    2. 右键单击 WPF 项目节点，然后选择 "**编辑**"。
    3. 找到文件中的最后一个 `</PropertyGroup>` 结束标记，并在该标记后面添加以下 XML。

        ``` xml
        <PropertyGroup>
          <AssetTargetFallback>uap10.0.18362</AssetTargetFallback>
        </PropertyGroup>
        ```

    4. 保存并关闭项目文件。
    5. 右键单击 WPF 项目节点，然后选择 "**重新加载项目**"。

4. 生成并运行打包项目。 确认 WPF 运行，UWP 自定义控件按预期方式显示。

## <a name="related-topics"></a>相关主题

* [在桌面应用中托管 UWP XAML 控件（XAML 孤岛）](xaml-islands.md)
* [XAML 孤岛代码示例](https://github.com/microsoft/Xaml-Islands-Samples)
* [WindowsXamlHost](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/windowsxamlhost)
