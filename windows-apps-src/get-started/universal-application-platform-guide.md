---
author: TylerMSFT
title: "通用 Windows 平台 (UWP) 应用指南"
description: "在本指南中，了解有关可跨多种设备运行的通用 Windows 平台 (UWP) 应用的信息。"
ms.assetid: 59849197-B5C7-493C-8581-ADD6F5F8800B
ms.sourcegitcommit: 213384a194513a0f98a5f37e7f0e0849bf0a66e2
ms.openlocfilehash: 191a7aef1a027747379c991e17afc1580a9ec549

---

# 通用 Windows 平台 (UWP) 应用指南


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 的文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

在本指南中，你将了解如下内容：

-   什么是*设备系列*，以及如何确定要面向的设备系列。
-   借助新的 UI 控件和面板，即可使你的 UI 能够适应不同的设备外形规格。
-   如何了解和控制适用于你的应用的 API 图面。

Windows 8 引入了 Windows 运行时 (WinRT)，这是 Windows 应用模型史上的一次突破。 它的设计初衷是成为通用应用程序体系结构。

在提供 Windows Phone 8.1 后，Windows 运行时在 Windows Phone 8.1 与 Windows 之间仍保持一致。 这使得开发人员能够创建面向使用共享基本代码的 Windows 和 Windows Phone 的*通用 Windows 8 应用*。

Windows10 引入了通用 Windows 平台 (UWP)，这进一步推动了 Windows 运行时模型的发展，并将该平台引入到 Windows 10 统一核心版中。 作为核心版的一部分，UWP 现提供了一个可供在每个运行 Windows 10 的设备上使用的通用应用平台。 借助此次突破，面向 UWP 的应用不仅可以调用对所有设备均通用的 WinRT API，还可以调用特定于要运行应用的设备系列的 API（包括 Win32 和 .NET API）。 UWP 可跨不同设备提供有保证的核心 API 图层。 这意味着你可以创建可安装在各种设备上的单个应用包。 并且借助该单个应用包，Windows 应用商店可提供一个统一的分发渠道，以涉及访问可运行你的应用的所有设备类型。

![通用 Windows 平台应用可在各种设备上运行，支持自适应式用户界面、自然用户输入、一个应用商店、一个开发人员中心，以及云服务](images/universalapps-overview.png)

由于 UWP 应用可在各种具有不同外形规格和输入方式的设备上运行，因此你可能希望针对每个设备对其进行定制，并且可能希望每个设备都能各具独特功能。 设备将其自己独特的 API 添加到有保证的 API 图层。 你可以编写相关代码以有条件地访问这些独特 API，这样你的应用便能在其他设备上提供不同的体验时启用特定于某一设备类型的功能。 自适应 UI 控件和新布局面板可帮助你在广泛的屏幕分辨率中定制你的 UI。

## 设备系列


Windows 8.1 和 Windows Phone 8.1 应用面向以下任一操作系统 (OS)：Window 或 Windows Phone。 在 Windows 10 中，你将不再面向某一操作系统，而是让你的应用改为面向一个或多个设备系列。 设备系列可标识在其中的设备上所需的 API、系统特性和行为。 它还用于确定可从应用商店安装你的应用的设备集。 下面是设备系列的层次结构。

![设备系列](images/devicefamilytree.png)

设备系列是汇总在一起的 API 集，具有给定名称和版本号。 设备系列是操作系统的基础构件。 运行桌面操作系统的电脑，基于桌面设备系列。 运行移动操作系统的手机和平板电脑等，基于移动设备系列。 以此类推。

通用设备系列是特殊系列。 它并非任意操作系统的直接基础构件。 相反，通用设备系列中的 API 集由子设备系列继承。 因此，通用设备系列 API 均能保证存在于每个操作系统中，从而能够存在于每个设备中。

每个子设备系列均将其自己的 API 添加到所继承的设备系列。 子设备系列中生成的 API 集将保证存在于基于该设备系列的操作系统中，因此存在于运行该操作系统的每个设备上。

设备系列的一个好处是，应用可在任意甚至是所有各式各样的设备上运行，范围从手机、平板电脑、台式机一直到 Surface Hub 和 Xbox 控制台。 你的应用还可以使用自适应代码动态监测和使用通用设备系列之外的设备的功能。

你的应用将面向哪些设备系列由你自行决定。 并且该决定将从以下重要方面影响你的应用。 它决定以下项：

-   你的应用可假定在运行时存在（并因此可以自由调用）的 API 集。
-   仅在条件语句内才安全的 API 调用集。
-   可从应用商店安装你的应用的设备集（以及因此你需要考虑的外形规格）。

选择设备系列将产生以下两个主要的结果：可以无条件地由应用调用的 API 图面，以及应用可访问的设备数目。 这两个因素涉及到取舍且成反比关系。 例如，UWP 应用是专门面向通用设备系列的应用，所以可供所有设备使用。 面向通用设备系列的应用可以假定仅存在通用设备系列中的 API（因为这是其目标对象）。 其他 API 必须按条件进行调用。 此外，因为此类应用可在多种设备上运行，所以它还必须具备高度自适应 UI 和综合性的输入功能。 Windows 移动应用是专门面向移动设备系列的应用，并且可用于其操作系统基于移动设备系列的设备（这包括手机、平板电脑以及类似的设备）。 移动设备系列应用可以假定存在移动设备系列中的所有 API，并且其 UI 必须具有适量的自适应性。 面向 IoT 设备系列的应用只能安装在 IoT 设备上，并且可以假定存在 IoT 设备系列中的所有 API。 该应用可能在很大程度上特定于其 UI 和输入功能，正如你知道的那样，它仅在特定类型的设备上运行。

下面是一些注意事项，可帮助你确定要面向的设备系列：

**最大化应用能够访问的设备范围**

若要让你的应用能够访问最大范围的设备，并且需要它能够在尽可能多的设备类型上运行，则该应用需面向通用设备系列。 这样，该应用将自动面向每个基于通用的设备系列（在上述关系图中，均为子通用设备类列）。 这意味着，该应用既可以在每个基于这些设备系列的操作系统上运行，又可以在运行这些操作系统的所有设备上运行。 仅保证可用于所有这些设备的 API 才是由目标通用设备系列的特定版本定义的 API 集。 （在此版本中，版本号始终是 10.0.x.0。）若要了解应用如何调用其目标设备系列版本之外的 API，请参阅本主题后面的“编写代码”。

**将应用的运行范围限制为某一类型的设备**

你可能不希望你的应用在多种设备上运行；或许它专用于某一种设备，比方说，台式电脑或 Xbox 控制台。 在此情况下，你可以选择让你的应用面向某一子设备系列。 例如，如果你的应用面向桌面设备系列，则保证可用于该应用的 API 不仅应包括继承自通用设备系列的 API，还应包括特定于桌面设备系列的 API。

**将应用的运行范围限制为所有可用设备的子集**

既非让你的应用面向通用设备系列，也非面向某一子设备系列，而应将你的应用改为面向两个（或更多）子设备系列。 让你的应用面向桌面和移动设备系列或许也行得通。 或台式电脑和 Xbox。 或台式电脑、Xbox 和 Surface Hub。

**不包括对特定版本的设备系列的支持**

在极少数情况下，你可能希望你的应用在任意设备上运行，但某一特定版本的特定设备系列内的设备除外。 例如，假设你的应用面向 10.0.x.0 版本的通用设备系列。 当操作系统版本在将来出现变动（比方说，更改为 10.0.x.2）时，此时你可能需要通过使应用面向 10.0.x.0 版本的通用设备系列和 10.0.x.1 版本的 Xbox，指定该应用在除 10.0.x.1 版本的 Xbox 之外的任意设备上运行。 然后，你的应用将不适用于 Xbox 10.0.x.1（含该版本号）以及早期版本内的设备系列版本集。

默认情况下，Microsoft Visual Studio 将 **Windows.Universal** 指定为应用包清单文件中的目标设备系列。 若要指定应用从应用商店向其提供的设备系列，请在 Package.appxmanifest 文件中手动配置 [**TargetDeviceFamily**](https://msdn.microsoft.com/library/windows/apps/dn986903) 元素。

## UI 和通用输入


UWP 应用可以在具有不同输入形式、屏幕分辨率、DPI 密度和其他独特的特征的各式各样的设备上运行。 Windows 10 提供了新的通用控件、布局面板和工具，以便你的 UI 能够适应可运行你的应用的设备。 例如，当你的应用要在台式机与移动设备上运行时，你可以定制 UI 以充分利用这两者屏幕分辨率方面的差异。

你的应用 UI 的某些方面将自动适应不同的设备。 诸如按钮和滑块等控件将自动适应不同的设备系列和输入模式。 但是，你的应用的用户体验设计可能需要根据正在运行该应用的设备进行调整。 例如，当照片应用在手持式小型设备上运行时，该应用应当适应 UI，以确保该用法是单手使用的理想之选。 当照片应用在台式机上运行时，UI 应进行调整以充分利用额外的屏幕空间。

Windows 通过以下功能帮助你的 UI 面向多个设备：

-   通用控件和布局面板可帮助你针对设备的屏幕分辨率优化你的 UI
-   常用的输入处理允许你通过触摸、笔、鼠标或键盘或者控制器（如 Microsoft Xbox 控制器）接收输入
-   工具可以帮助你设计出能够适应不同屏幕分辨率的 UI
-   自适应缩放用于调整以适应不同设备的分辨率和 DPI

### 通用控件和布局面板

Windows 10 提供了新的控件，例如日历和拆分视图。 之前仅适用于 Windows Phone 的透视控件现在也可用于通用设备系列。

控件已经过更新，从而可以在较大的屏幕上正常运行、自行根据设备提供的屏幕像素数进行调整，以及可与多种输入类型（例如键盘、鼠标、触摸、笔及 Xbox 控制器之类的控制器）良好地协作运行。

你可能会发现你需要根据正在运行你的应用的设备的屏幕分辨率，来调整整个 UI 布局。 例如，在桌面上运行的通信应用可能包括呼叫方的画中画以及非常适合于鼠标输入的控件：

![桌面通信应用 UI](images/adaptiveux-desktop.png)

但是，当应用在手机上运行时，由于可使用的屏幕空间较少，从而使得你的应用可能会消除画中画视图并放大呼叫按钮，以便进行单手操作：

![手机通信应用 UI](images/adaptiveux-phone.png)

为了帮助你基于可用的屏幕空间量对整体 UI 布局进行调整，Windows 10 引入了自适应面板和设计状态。

### 设计带有自适应面板的自适应 UI

布局面板将依据可用空间为其子面板提供相应的大小和位置。 例如，[**StackPanel**](https://msdn.microsoft.com/library/windows/apps/br209635) 将按顺序（水平或垂直）排列其子面板。 [
            **Grid**](https://msdn.microsoft.com/library/windows/apps/br242704) 会像 CSS 网格那样将其子网格置于单元格中。

新 [**RelativePanel**](https://msdn.microsoft.com/library/windows/apps/dn879546) 实现了由其子元素间的关系定义的布局样式。 它旨在用于创建可适应屏幕分辨率更改的应用布局。 **RelativePanel** 通过定义元素间的关系简化了重新排列元素的过程，这样你便可以生成更为动态的 UI，而无需使用嵌套布局。

在下面的示例中，无论方向或布局做何更改，**blueButton** 都会显示在 **textBox1** 的右侧，随即 **orangeButton** 将显示在下方，并且与 **blueButton** 保持对齐，甚至在 **textBox1** 内键入文本后该框的宽度出现变化时也是如此。 之前需要 **Grid** 中的行和列才能实现此效果，而现在它只需使用极少的标记即可实现。

![Relativepanel 示例](images/relativepane-standalone.png)

```XML
<RelativePanel>
    <TextBox x:Name="textBox1" Text="textbox" Margin="5"/>
    <Button x:Name="blueButton" Margin="5" Background="LightBlue" Content="ButtonRight" RelativePanel.RightOf="textBox1"/>
    <Button x:Name="orangeButton" Margin="5" Background="Orange" Content="ButtonBelow" RelativePanel.RightOf="textBox1" RelativePanel.Below="blueButton"/>
</RelativePanel>
```

### 使用视觉状态触发器，生成可针对可用屏幕空间进行调整的 UI

你的 UI 可能需要根据窗口大小的变化进行调整。 自适应视觉状态允许你更改视觉状态，以响应窗口大小的变化。

StateTriggers 定义激活视觉状态的阈值，然后将根据触发状态更改的窗口大小设置布局属性。

在下面的示例中，当窗口大小的宽度为 720 像素或更高时，将触发名为 **wideView** 的视觉状态，然后将**“评分最高的游戏”**面板安排在右侧显示，并使之与**“热门免费游戏”**面板的顶部对齐。

![视觉状态触发器示例。 宽视图](images/relativepanel-wideview.png)

当窗口的宽度小于 720 像素时，将触发 **narrowView** 视觉状态，因为 **wideView** 触发器将不再适用且将不再有效。 **narrowView** 视觉状态将**“评分最高的游戏”**面板置于下方，并使之与**“热门付费游戏”**面板的左侧对齐：

![视觉状态触发器示例。 窄视图](images/relativepanel-narrowview.png)

下面是上述视觉状态触发器的 XAML。 为了简便起见，删除了下方用“`...`”表示的这些面板的定义。

```XML
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup>
            <VisualState x:Name="wideView">
                <VisualState.StateTriggers>
                    <AdaptiveTrigger MinWindowWidth="720" />
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Target="best.(RelativePanel.RightOf)" Value="free"/>
                    <Setter Target="best.(RelativePanel.AlignTopWidth)" Value="free"/>
                </VisualState.Setters>
            </VisualState>
            <VisualState x:Name="narrowView">
                <VisualState.Setters>
                    <Setter Target="best.(RelativePanel.Below)" Value="paid"/>
                    <Setter Target="best.(RelativePanel.AlignLeftWithPanel)" Value="true"/>
                </VisualState.Setters>
                <VisualState.StateTriggers>
                    <AdaptiveTrigger MinWindowWidth="0" />
                </VisualState.StateTriggers>
            </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
    ...
</Grid>
```

### 工具

默认情况下，你可能需要面向最广泛的可用设备系列。 当你准备好查看你的应用在特定设备上的外观和布局方式时，可使用 Visual Studio 中的设备预览工具栏，在较小或中等移动设备、电脑或者较大电视屏幕上预览你的 UI。 这样一来，你便可以定制和测试自己的自适应视觉状态：

![Visual Studio 2015 设备预览工具栏](images/vs2015-device-preview-toolbar.png)

你无需事先确定好将支持的每个设备类型。 你可以在以后向你的项目添加其他设备大小。

### 自适应缩放

Windows 10 引入了现有缩放模型的演变。 除了缩放矢量内容外，还有一系列统一的比例系数，用于在各种屏幕大小和显示分辨率中为 UI 元素提供一致的大小。 比例系数还与其他操作系统（如 iOS 和 Android）的比例系数兼容。 这样便可以更轻松地在这些平台之间共享资源。

应用商店选择要下载的资源在一定程序上取决于设备的 DPI。 仅下载最匹配设备的资源。

### 常用的输入处理

可以生成通用 Windows 应用，方法是使用可处理各种输入的通用控件，例如鼠标、键盘、触摸、笔和控制器（如 Xbox 控制器）。 墨迹历来仅与笔输入关联，但在 Windows 10 中，墨迹还与某些设备上的触摸和任意指针输入关联。 墨迹在许多设备（包括移动设备）上均受支持，并且易于与几行代码合并。

以下 API 提供对输入的访问：

-   [
            **CoreIndependentInputSource**](https://msdn.microsoft.com/library/windows/apps/dn298460) 是一个新的 API，允许你在主线程或后台线程上使用原始输入。
-   [
            **PointerPoint**](https://msdn.microsoft.com/library/windows/apps/br242038) 将原始触摸、鼠标和笔数据统一成一组统一的接口和事件，可借助 **CoreInput** 在主线程或后台线程上使用它们。
-   [
            **PointerDevice**](https://msdn.microsoft.com/library/windows/apps/br225633) 是支持设备查询功能的设备 API，以便你可以确定哪些输入形式在设备上可用。
-   新的 [**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/dn858535) XAML 控件和 [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/dn922011) Windows 运行时 API 允许你访问墨迹笔划数据。

## 编写代码


[Visual Studio 中 Windows 10 项目](https://msdn.microsoft.com/en-us/library/windows/apps/dn609832.aspx#target_win10)的编程语言选项包括 Visual C++、C#、Visual Basic 和 JavaScript。 对于 Visual C++、C# 和 Visual Basic，可以使用 XAML 实现高保真的本机 UI 体验。 对于 Visual C++，可以选择用 DirectX 来替代 XAML 或者同时使用这两者进行绘制。 对于 JavaScript，表示层将采用 HTML，毋庸置疑，HTML 是跨平台 Web 标准。 大部分代码和 UI 都是通用的，可采用相同的方式在任意位置运行。 但对于为特定设备系列定制的代码和为特定外形规格定制的 UI，你可以选择使用自适应代码和自适应 UI。 让我们来看一下以下不同的用例。

**调用由你的目标设备系列实现的 API**

每当你要调用 API 时，你需知道该 API 是否由应用面向的设备系列实现。 如果有疑问，你可以查阅 API 参考文档。 当你打开相关主题并查看“要求”部分时，你将了解什么是实现设备系列。 假设你的应用面向 10.0.x.0 版本的通用设备系列并且你想要调用 [**Windows.UI.Core.SystemNavigationManager**](https://msdn.microsoft.com/library/windows/apps/dn893595) 类的成员。 在本示例中，设备系列是“通用”。 最好是进一步确认你想要调用的类成员是否还在目标设备系列内，在本例中答案是肯定的。 因此，在本示例中，你现在已知道 API 保证显示在可安装你的应用的每个设备上，并且可以在代码中调用这些 API，就像通常所执行操作的那样。

```csharp
    Windows.UI.Core.SystemNavigationManager.GetForCurrentView().BackRequested += TestView_BackRequested;
```

再如，假设你的应用面向 10.0.x.0 版本的 Xbox 设备系列，则按照你要调用的 API 的参考主题所示，此类 API 是在 10.0.x.0 版本的 Xbox 设备系列中引入的。 同样，在此情况下，此 API 保证会出现在可安装你的应用的每个设备上。 因此，你将能够以正常方式在代码中调用该 API。

请注意，Visual Studio IntelliSense 不识别 API，除非这些 API 由你的应用的目标设备系列或已引用的任何扩展 SDK 实现。 因此，如果你尚未引用任何扩展 SDK，你将能够确保显示在 IntelliSense 中的任何 API 都必须因此位于目标设备系列中，并且你可以自由调用它们。

**调用未由你的目标设备系列实现的 API**

存在这样一种情况：你想要调用 API，但文档中未列出你的目标设备系列。 在此情况下，你可以选择编写自适应代码，以便调用该 API。

**编写带有 ApiInformation 类的自适应代码**

编写自适应代码有两步。 第一步是将你需要访问的 API 提供给项目。 为此，请添加对扩展 SDK（表示具有你想要有条件调用的 API 的设备系列）的引用。 请参阅[扩展 SDK](../porting/w8x-to-uwp-porting-to-a-uwp-project.md#extension-sdks)。

第二步是有条件地在代码中使用 [**Windows.Foundation.Metadata.ApiInformation**](https://msdn.microsoft.com/library/windows/apps/dn949001) 类，测试是否存在你要调用的 API。 此条件将进行评估（无论你的应用在何处运行），但仅针对存在相应 API 的设备评估为 True，从而可调用该 API。

如果你只需调用少量 API，则可以使用 [**ApiInformation.IsTypePresent**](https://msdn.microsoft.com/library/windows/apps/dn949016) 方法，如下所示。

```csharp
    // Note: Cache the value instead of querying it more than once.
    bool isHardwareButtonsAPIPresent =
        Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons");

    if (isHardwareButtonsAPIPresent)
    {
        Windows.Phone.UI.Input.HardwareButtons.CameraPressed +=
            HardwareButtons_CameraPressed;
    }
```

在此情况下，我们可以断定，存在 [**HardwareButtons**](https://msdn.microsoft.com/library/windows/apps/jj207557) 类即代表存在 [**CameraPressed**](https://msdn.microsoft.com/library/windows/apps/dn653805) 事件，因为此类和此成员具有相同的要求信息。 但此时，新的成员将添加到已引入类中，并且这些成员将具有更高的“已引入”版本号。 在此情况下，你可以使用 **IsEventPresent**、**IsMethodPresent**、**IsPropertyPresent** 和类似的方法来测试是否存在各个成员，而无需使用 **IsTypePresent**。 下面提供了一个示例。

```csharp
    bool isHardwareButtons_CameraPressedAPIPresent =
        Windows.Foundation.Metadata.ApiInformation.IsEventPresent
            ("Windows.Phone.UI.Input.HardwareButtons", "CameraPressed");
```

设备系列中的 API 集将进一步细分为 API 合约。 你可以使用 **ApiInformation.IsApiContractPresent** 方法来测试是否存在 API 合约。 如果你想要测试大量 API（它们均位于同一版 API 合约中）的存在，这会很有用。

```csharp
    bool isWindows_Devices_Scanners_ScannerDeviceContract_1_0Present =
        Windows.Foundation.Metadata.ApiInformation.IsApiContractPresent
            ("Windows.Devices.Scanners.ScannerDeviceContract", 1, 0);
```

**UWP 中的 Win32 API**

用 C++/CX 编写的 UWP 应用或 Windows 运行时组件具有对 UWP 所包含的 Win32 API 的访问权限。 这些 Win32 API 由所有 Windows 10 设备系列实现。 将你的应用链接到 Windowsapp.lib。 Windowsapp.lib 是为 UWP API 提供导出的“Umbrella”库。 指向 Windowsapp.lib 的链接将添加到存在于所有 Windows 10 设备系列上的 Dll 的应用依赖项。

有关适用于 UWP 应用的 Win32 API 的完整列表，请参阅 [UWP 应用的 API 集](https://msdn.microsoft.com/library/windows/desktop/mt186421)和 [UWP 应用的 Dll](https://msdn.microsoft.com/library/windows/desktop/mt186422)。

## 用户体验


借助通用 Windows 应用，你可以充分利用正在运行此类应用的设备的独特功能。 你的应用可以利用桌面设备的全部功能、平板电脑上直接操作的自然交互（包括触摸和笔输入）、移动设备的便携性和方便性，以及 [Surface Hub](http://go.microsoft.com/fwlink/?LinkId=526365) 的协作功能。

良好的[设计](http://go.microsoft.com/fwlink/?LinkId=258848)是确定用户如何与你的应用交互，以及确定应用外观和运行方式的过程。 用户体验极大地影响着用户对你的应用的满意度，所以请勿忽略此步骤。 [设计基础知识](https://dev.windows.com/en-us/design)介绍了如何设计通用 Windows 应用。 有关设计出令用户满意的 UWP 应用的信息，请参阅[面向设计人员的通用 Windows 平台 (UWP) 应用简介](https://msdn.microsoft.com/library/windows/apps/dn958439)。 在开始编写代码之前，请参阅[设备入门](../input-and-devices/device-primer.md)，以帮助你全面考虑在你要针对的所有不同外形规格上使用应用的交互体验。

![支持 Windows 的设备](images/1894834-hig-device-primer-01-500.png)

除了在不同设备上的交互外，还需[规划应用](https://msdn.microsoft.com/library/windows/apps/hh465427)以利用在多个设备之间运行的优势。 例如：

-   使用[云服务](http://go.microsoft.com/fwlink/?LinkId=526377)跨设备同步。 了解如何[连接到 Web 服务](https://msdn.microsoft.com/library/windows/apps/xaml/hh761504)以支持你的应用体验。

-   请考虑如何支持用户从一台设备移动到另一台设备，以及如何回到离开时的位置。 将[通知](https://msdn.microsoft.com/library/windows/apps/mt187203)和[应用内购买](https://msdn.microsoft.com/library/windows/apps/mt219684)包含在你的规划中。 这些功能应该能够跨设备运行。

-   使用[适用于 UWP 应用的导航设计基础知识](https://msdn.microsoft.com/library/windows/apps/dn958438)设计你的工作流，以适应移动设备、小屏幕和大屏幕设备。 [设置你的用户界面布局](https://msdn.microsoft.com/library/windows/apps/dn958435)来响应不同的屏幕大小和分辨率。

-   请考虑你的应用中是否有在较小的移动设备屏幕上不奏效的功能。 也可能有一些功能区在固定式台式机上不起作用，而需在移动设备上才能运行。 例如，在大多数应用场景中，[位置](https://msdn.microsoft.com/library/windows/apps/mt219698)即指移动设备。

-   请考虑如何容纳多种输入形式。 请参阅[交互指南](https://msdn.microsoft.com/library/windows/apps/dn611861)，了解用户如何使用 [Cortana](https://msdn.microsoft.com/library/windows/apps/dn974233)、[语音](https://msdn.microsoft.com/library/windows/apps/dn596121)、[触摸交互](https://msdn.microsoft.com/library/windows/apps/hh465370)、[触摸键盘](https://msdn.microsoft.com/library/windows/apps/hh972345)等与你的应用交互。

    请参阅[文本和文本输入指南](https://msdn.microsoft.com/library/windows/apps/dn611864)，以获取更多的传统交互体验。

## 通过你的仪表板提交通用 Windows 应用


利用统一的新 Windows 开发人员中心仪表板，你可以在同一位置管理和提交所有面向 Windows 设备的应用。 新功能简化了流程，同时给予您更多的控制。 你还会找到与[付款详细信息](https://msdn.microsoft.com/library/windows/apps/dn986925)组合的详细[分析报告](https://msdn.microsoft.com/library/windows/apps/mt148522)、[推广你的应用并与客户互动](https://msdn.microsoft.com/library/windows/apps/mt148526)的方式，等等。

若要了解如何在 Windows 应用商店中提交应用以供发布，请参阅[使用统一的 Windows 开发人员中心仪表板](../publish/using-the-windows-dev-center-dashboard.md)。

 

 



<!--HONumber=Jun16_HO4-->


