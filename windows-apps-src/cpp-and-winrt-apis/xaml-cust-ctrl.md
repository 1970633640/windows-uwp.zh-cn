---
author: stevewhims
description: 本主题将指导你完成的步骤创建简单的自定义控件使用 C + + WinRT。 你可以生成的相关信息来创建你自己功能丰富且可自定义的 UI 控件。
title: XAML 自定义（模板化）控件与 C++/WinRT
ms.author: stwhi
ms.date: 08/01/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp，标准，c + +，cpp，winrt，投影，XAML，自定义，模板化控件
ms.localizationpriority: medium
ms.openlocfilehash: fd1843afc58bc758db1c6e575f3733bdc4f47b4e
ms.sourcegitcommit: 2a63ee6770413bc35ace09b14f56b60007be7433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3929493"
---
# <a name="xaml-custom-templated-controls-with-cwinrtwindowsuwpcpp-and-winrt-apisintro-to-using-cpp-with-winrt"></a>使用 XAML 自定义 （模板化） 控件[C + + WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)

> [!NOTE]
> **与在商业发行之前可能会进行实质性修改的预发布产品相关的一些信息。 Microsoft 对于此处提供的信息不作任何明示或默示的担保。**

> [!IMPORTANT]
> 有关支持你了解如何利用 C++/WinRT 来使用和创作运行时类的基本概述和术语，请参阅[通过 C++/WinRT 使用 API](consume-apis.md) 和[通过 C++/WinRT 创作 API](author-apis.md)。

通用 Windows 平台 (UWP) 的最强大功能之一是用户界面 (UI) 堆栈提供如何创建基于 XAML[**控件**](/uwp/api/windows.ui.xaml.controls.control)类型的自定义控件的灵活性。 XAML UI 框架提供了[自定义依赖属性](/windows/uwp/xaml-platform/custom-dependency-properties)和附加的属性和[控件模板](/windows/uwp/design/controls-and-patterns/control-templates)，这使其更轻松地创建功能丰富且可自定义控件等功能。 本主题将指导你完成的步骤创建自定义 （模板化） 控件使用 C + + WinRT。

## <a name="create-a-blank-app-bglabelcontrolapp"></a>创建空白应用 (BgLabelControlApp)
首先在 Microsoft Visual Studio 中创建新项目。 创建**Visual c + +** > **Windows 通用** > **空白应用 (C + + WinRT)** 项目，并将其命名为*BgLabelControlApp*。

我们将创作新类来表示自定义 （模板化） 控件。 我们正在同一编译单元内创作和使用该类。 但我们希望能够来实例化此类 XAML 标记中的，因此，它将成为一个运行时类。 而且我们将使用 C++/WinRT 来创作和使用它。

创作新的运行时类的第一步是将新的 **Midl 文件(.idl)** 项添加到项目。 将其命名为 `BgLabelControl.idl`。 删除 `BgLabelControl.idl` 的默认内容，然后粘贴到此运行时类声明中。

```idl
// BgLabelControl.idl
namespace BgLabelControlApp
{
    runtimeclass BgLabelControl : Windows.UI.Xaml.Controls.Control
    {
        BgLabelControl();
        static Windows.UI.Xaml.DependencyProperty LabelProperty{ get; };
        String Label;
    }
}
```

以上列表演示声明一个依赖属性 (DP) 时遵循的模式。 有两个部分每个分发点。 首先，声明类型[**DependencyProperty**](/uwp/api/windows.ui.xaml.dependencyproperty)的只读的静态属性。 它具有 DP 以及*属性*的名称。 你将在实现中使用此静态属性。 第二，你使用的类型和你 DP 名称声明读写实例属性。

> [!NOTE]
> 如果你想 DP 浮点类型，然后将其`double`(`Double` [MIDL 3.0](/uwp/midl-3/)中)。 声明和实现类型的 DP `float` (`Single` MIDL 中)，然后为该 DP 在 XAML 标记中设置一个值将导致错误和*无法创建 'Windows.Foundation.Single 从文本<NUMBER>*。

保存文件并生成项目。 在生成过程中，`midl.exe` 工具会运行以创建描述该运行时类的 Windows 运行时元数据文件 (`\BgLabelControlApp\Debug\BgLabelControlApp\Unmerged\BgLabelControl.winmd`)。 然后，`cppwinrt.exe` 工具运行以生成源代码文件，从而为你在创作和使用运行时类时提供支持。 这些文件包含让你开始实现已在 IDL 中声明的**BgLabelControl**运行时类的存根。 这些存根是 `\BgLabelControlApp\BgLabelControlApp\Generated Files\sources\BgLabelControl.h` 和 `BgLabelControl.cpp`。

将这些存根文件 `BgLabelControl.h` 和 `BgLabelControl.cpp` 从 `\BgLabelControlApp\BgLabelControlApp\Generated Files\sources\` 复制到项目文件夹中，即 `\BgLabelControlApp\BgLabelControlApp\`。 在**解决方案资源管理器**中，确保将**显示所有文件**切换为打开。 右键单击已复制的存根文件，然后单击**包括在项目中**。

## <a name="implement-the-bglabelcontrol-custom-control-class"></a>实现**BgLabelControl**自定义控件类
现在，让我们打开 `\BgLabelControlApp\BgLabelControlApp\BgLabelControl.h` 和 `BgLabelControl.cpp` 并实现运行时类。 在`BgLabelControl.h`、 更改要设置的默认样式键，实现**标签**和**LabelProperty**的构造函数、 添加一个名为**介绍 OnLabelChanged**处理的依赖属性的值更改的静态事件处理程序和添加私有成员**LabelProperty**适用的应用商店的支持字段。

后添加这些内容，你`BgLabelControl.h`如下所示。

```cppwinrt
// BgLabelControl.h
...
struct BgLabelControl : BgLabelControlT<BgLabelControl>
{
    BgLabelControl() { DefaultStyleKey(winrt::box_value(L"BgLabelControlApp.BgLabelControl")); }

    winrt::hstring Label()
    {
        return winrt::unbox_value<winrt::hstring>(GetValue(m_labelProperty));
    }

    void Label(winrt::hstring const& value)
    {
        SetValue(m_labelProperty, winrt::box_value(value));
    }

    static Windows::UI::Xaml::DependencyProperty LabelProperty() { return m_labelProperty; }

    static void OnLabelChanged(Windows::UI::Xaml::DependencyObject const&, Windows::UI::Xaml::DependencyPropertyChangedEventArgs const&);

private:
    static Windows::UI::Xaml::DependencyProperty m_labelProperty;
};
...
```

在`BgLabelControl.cpp`，定义如下的静态成员。

```cppwinrt
// BgLabelControl.cpp
...
Windows::UI::Xaml::DependencyProperty BgLabelControl::m_labelProperty =
    Windows::UI::Xaml::DependencyProperty::Register(
        L"Label",
        winrt::xaml_typename<winrt::hstring>(),
        winrt::xaml_typename<BgLabelControlApp::BgLabelControl>(),
        Windows::UI::Xaml::PropertyMetadata{ winrt::box_value(L"default label"), Windows::UI::Xaml::PropertyChangedCallback{ &BgLabelControl::OnLabelChanged } }
);

void BgLabelControl::OnLabelChanged(Windows::UI::Xaml::DependencyObject const& d, Windows::UI::Xaml::DependencyPropertyChangedEventArgs const& /* e */)
{
    if (BgLabelControlApp::BgLabelControl theControl{ d.try_as<BgLabelControlApp::BgLabelControl>() })
    {
        // Call members of the projected type via theControl.

        BgLabelControlApp::implementation::BgLabelControl* ptr{ winrt::from_abi<BgLabelControlApp::implementation::BgLabelControl>(theControl) };
        // Call members of the implementation type via ptr.
    }
}
...
```

在本演练中，我们将不会使用**介绍 OnLabelChanged**。 但是，以便你可以了解如何使用属性更改回调中注册依赖属性。 **介绍 OnLabelChanged**实现还显示了如何从基本的投影类型 （基本的投影的类型是**DependencyObject**，在此情况下） 获取派生的投影的类型。 和它显示了如何获取指向实现投影的类型的类型，然后。 第二个操作自然地仅将可能在项目中实现的投影的类型 （实现运行时类的项目）。

> [!NOTE]
> 如果你安装了[Windows 10 SDK 预览版 17661](https://www.microsoft.com/software-download/windowsinsiderpreviewSDK)，或更高版本，然后你可以调用[**winrt::get_self**](/uwp/cpp-ref-for-winrt/get-self)依赖属性更改的事件处理程序中上方，而不是[**winrt:: from_abi**](/uwp/cpp-ref-for-winrt/from-abi)。

## <a name="design-the-default-style-for-bglabelcontrol"></a>**BgLabelControl**设计的默认样式

在它的构造函数， **BgLabelControl**设置的默认样式键本身。 但什么*是*默认样式？ 自定义的 （模板化） 控件需要有一个默认样式&mdash;包含默认控件模板&mdash;它可以用它来呈现其样式和/或模板不设置控件的使用者的情况下。 本部分中，我们将将某个标记文件添加到包含我们的默认样式的项目。

你的项目节点下，创建一个新文件夹并将其命名为"Themes"。 在`Themes`，添加新项的类型**Visual c + +** > **XAML** > **XAML 视图**，并将其命名为"Generic.xaml"。 文件夹和文件名称必须要在 XAML 框架，以便查找自定义控件的默认样式的顺序如下。 删除的默认内容`Generic.xaml`，然后粘贴到下面的标记中。

```xaml
<!-- \Themes\Generic.xaml -->
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:BgLabelControlApp">

    <Style TargetType="local:BgLabelControl" >
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="local:BgLabelControl">
                    <Grid Width="100" Height="100" Background="{TemplateBinding Background}">
                        <TextBlock HorizontalAlignment="Center" VerticalAlignment="Center" Text="{TemplateBinding Label}"/>
                    </Grid>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
</ResourceDictionary>
```

在此情况下，默认样式设置的唯一属性是控件模板。 该模板由 （其后台绑定到 XAML[**控件**](/uwp/api/windows.ui.xaml.controls.control)类型的所有实例都具有**背景**属性） 的正方形和文本元素 （其文本绑定到**BgLabelControl::Label**依赖属性） 组成。

## <a name="add-an-instance-of-bglabelcontrol-to-the-main-ui-page"></a>将**BgLabelControl**实例添加到主 UI 页面

打开 `MainPage.xaml`，其中包含主 UI 页面的 XAML 标记。 （在**StackPanel**中) 的**按钮**元素后立即, 添加以下标记。

```xaml
<local:BgLabelControl Background="Red" Label="Hello, World!"/>
```

此外，添加以下 include 指令`MainPage.h`以便**MainPage**类型 （编译 XAML 标记和命令性代码的组合） 可以知道**BgLabelControl**自定义控件类型。

```cppwinrt
// MainPage.h
...
#include "BgLabelControl.h"
...
```

立即生成并运行该项目。 你将看到的默认控件模板绑定到背景画笔，而**BgLabelControl**实例在标记中的标签。

本演练演示了自定义的 （模板化） 控件的一个简单的示例，在 C + + WinRT。 你可以让你自己的自定义控件，任意丰富、 齐全。 例如，自定义控件可能需要为可编辑的数据网格、 视频播放器或 3D 几何图形的可视化工具是复杂的形式。

## <a name="implementing-overridable-functions-such-as-measureoverride-and-onapplytemplate"></a>实现*可重写*功能，如**MeasureOverride**和**OnApplyTemplate**

派生自定义控件从[**控件**](/uwp/api/windows.ui.xaml.controls.control)运行时类，该类本身进一步派生基本的运行时类。 并且，可重写方法的**控件**、 [**FrameworkElement**](/uwp/api/windows.ui.xaml.frameworkelement)和在你的派生类可以替代的[**UIElement**](/uwp/api/windows.ui.xaml.uielement) 。 下面是代码示例向你显示如何执行该操作。

```cppwinrt
struct BgLabelControl : BgLabelControlT<BgLabelControl>
{
...
    // Control overrides.
    void OnPointerPressed(Windows::UI::Xaml::Input::PointerRoutedEventArgs const& /* e */) const { ... };

    // FrameworkElement overrides.
    Windows::Foundation::Size MeasureOverride(Windows::Foundation::Size const& /* availableSize */) const { ... };
    void OnApplyTemplate() const { ... };

    // UIElement overrides.
    Windows::UI::Xaml::Automation::Peers::AutomationPeer OnCreateAutomationPeer() const { ... };
...
};
```

*可重写*函数本身以不同方式提供不同的语言投影中。 在 C# 中，例如，可重写函数通常显示为受保护的虚拟函数。 在 C + + /winrt 中，它们既不虚拟，也不受保护，但是仍可以替代它们，并提供你自己的实现，如上所示。

## <a name="important-apis"></a>重要的 API
* [控件类](/uwp/api/windows.ui.xaml.controls.control)
* [DependencyProperty 类](/uwp/api/windows.ui.xaml.dependencyproperty)
* [FrameworkElement 类](/uwp/api/windows.ui.xaml.frameworkelement)
* [UIElement 类](/uwp/api/windows.ui.xaml.uielement)

## <a name="related-topics"></a>相关主题
* [控件模板](/windows/uwp/design/controls-and-patterns/control-templates)
* [自定义依赖属性](/windows/uwp/xaml-platform/custom-dependency-properties)