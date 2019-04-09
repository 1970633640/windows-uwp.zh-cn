---
Description: 菜单和上下文菜单会在用户发出请求时显示命令或选项列表。
title: 菜单和上下文菜单
label: Menus and context menus
template: detail.hbs
ms.date: 01/08/2019
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 0327d8c1-8329-4be2-84e3-66e1e9a0aa60
pm-contact: yulikl
design-contact: kimsea
dev-contact: llongley
doc-status: Published
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: d3ea8e2bff2455340a1183dbe5c1840fdb599d46
ms.sourcegitcommit: 7a1d5198345d114c58287d8a047eadc4fe10f012
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59247185"
---
# <a name="menus-and-context-menus"></a>菜单和上下文菜单

菜单和上下文菜单会在用户发出请求时显示命令或选项列表。 使用菜单浮出控件以显示单个，内联菜单。 使用菜单栏在水平行中，通常在应用程序窗口的顶部显示一组菜单。 每个菜单可以菜单项和子菜单。

![典型上下文菜单示例](images/contextmenu_rs2_icons.png)

| **获取 Windows UI 库** |
| - |
| 此控件是作为 Windows UI 库，包含新控件和适用于 UWP 应用的 UI 功能的 NuGet 包的一部分。 有关详细信息，包括安装说明，请参阅[Windows 用户界面库概述](https://docs.microsoft.com/uwp/toolkits/winui/)。 |

| **平台 Api** | **Windows UI 库 Api** |
| - | - |
| [MenuFlyout 类](/uwp/api/windows.ui.xaml.controls.menuflyout)，[菜单栏类](/uwp/api/windows.ui.xaml.controls.menubar)， [ContextFlyout 属性](/uwp/api/windows.ui.xaml.uielement.contextflyout)， [FlyoutBase.AttachedFlyout 属性](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.primitives.flyoutbase.attachedflyout.aspx) | [菜单栏类](/uwp/api/microsoft.ui.xaml.controls.menubar) |

## <a name="is-this-the-right-control"></a>这是正确的控件吗？

菜单和上下文菜单通过在用户不需要使用时对命令进行组织和隐藏，从而节省空间。 如果需要经常使用某一特定命令并希望有可用的空间，请考虑将该命令直接置于其自己的元素（而非菜单）中，以便用户无需遍历菜单即可访问它。

菜单和上下文菜单都是用于组织命令;若要显示任意内容，例如的通知或确认请求中，使用[对话框或弹出](dialogs.md)。

### <a name="menubar-vs-menuflyout"></a>菜单栏 vs。MenuFlyout

若要附加到画布上 UI 元素浮出控件中显示一个菜单，使用 MenuFlyout 控件承载在菜单项。 作为常规菜单或上下文菜单，可以调用菜单浮出控件。 菜单浮出控件承载在单个顶级菜单 （和可选的子菜单）。

若要在水平行显示一组多个顶级菜单，请使用菜单栏。 您通常放置在应用程序窗口的顶部菜单栏。

### <a name="menubar-vs-commandbar"></a>菜单栏 vs。CommandBar

菜单栏和命令栏二者都表示图面，可用来向用户公开的命令。 在菜单栏提供的快速而简单的方法以公开一组用于应用程序可能需要更多的组织或分组超出允许的命令栏的命令。

此外可以与 CommandBar 结合使用菜单栏。 在菜单栏用于提供大量命令和命令栏，以突出显示的最常用的命令。

## <a name="examples"></a>示例

<table>
<th align="left">XAML 控件库<th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p>如果已安装 <strong style="font-weight: semi-bold">XAML 控件库</strong>应用，请单击此处<a href="xamlcontrolsgallery:/item/MenuFlyout">打开此应用，了解 MenuFlyout 的实际应用</a>。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">获取 XAML 控件库应用 (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">获取源代码 (GitHub)</a></li>
    </ul>
</td>
</tr>
</table>

## <a name="menus-vs-context-menus"></a>菜单与上下文菜单

菜单和上下文菜单的外观和它们可以包含类似。 事实上，可以使用相同的控件[MenuFlyout](https://msdn.microsoft.com/library/windows/apps/dn299030)，若要创建它们。 不同之处在于，如何让用户对其进行访问。

何时应使用菜单或上下文菜单？

- 如果宿主元素的按钮或某些其他的主要作用是提供其他命令的命令元素，请使用一个菜单。
- 如果主机元素是一些具有另一主要用途（如显示文本或图像）的其他类型的元素，则使用上下文菜单。

例如，使用上一个按钮菜单提供筛选和排序选项的列表。 在此方案中，按钮控件的主要用途是提供对菜单的访问权限。

![邮件中的菜单示例](images/Mail_Menu.png)

如果要将命令（如剪切、复制和粘贴）添加到某个文本元素，请使用上下文菜单而不是菜单。 在此方案中，文本元素的主要作用是显示和编辑文本；其他命令（如剪切、复制和粘贴）是辅助命令，属于上下文菜单。

![照片库中的上下文菜单示例](images/ContextMenu_example.png)

### <a name="menus"></a>菜单

- 具有始终显示的单个入口点（例如，位于屏幕顶部的“文件”菜单）。
- 通常附加到某个按钮或父菜单项。
- 通过左键单击（或等效操作，例如用手指点击）进行调用。
- 与通过其[浮出控件](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.button.flyout.aspx)或[FlyoutBase.AttachedFlyout](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.primitives.flyoutbase.attachedflyout.aspx)属性，或在应用程序窗口的顶部菜单栏中进行分组。

### <a name="context-menus"></a>上下文菜单

- 附加到单个元素并显示辅助命令。
- 通过右键单击（或等效操作，例如用手指按住）进行调用。
- 通过 [ContextFlyout](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.uielement.contextflyout.aspx) 属性与元素相关联。

## <a name="icons"></a>图标

请考虑提供菜单项图标：

- 最常使用的项。
- 其图标是标准或已知的菜单项。
- 菜单项的图标也说明了该命令的执行。

对于没有标准可视化的命令可不必提供图标。 加密图标没有帮助，创建可视的待筛选邮件，并阻止用户关注重要菜单项。

![带图标的示例上下文菜单](images/contextmenu_rs2_icons.png)

````xaml
<MenuFlyout>
  <MenuFlyoutItem Text="Share" >
    <MenuFlyoutItem.Icon>
      <FontIcon Glyph="&#xE72D;" />
    </MenuFlyoutItem.Icon>
  </MenuFlyoutItem>
  <MenuFlyoutItem Text="Copy" Icon="Copy" />
  <MenuFlyoutItem Text="Delete" Icon="Delete" />
  <MenuFlyoutSeparator />
  <MenuFlyoutItem Text="Rename" />
  <MenuFlyoutItem Text="Select" />
</MenuFlyout>
````

> [!TIP]
> MenuFlyoutItem 中图标的大小为 16x16px。 如果使用 SymbolIcon、 FontIcon 或 PathIcon，图标会自动缩放为正确的大小，且不会丢失的保真度。 如果你使用 BitmapIcon，请确保你的资产为 16x16 像素。  

## <a name="create-a-menu-flyout-or-a-context-menu"></a>创建菜单浮出控件或上下文菜单

若要创建菜单浮出控件或上下文菜单，请使用[MenuFlyout 类](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyout)。 通过添加定义菜单的内容[MenuFlyoutItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyoutitem)， [MenuFlyoutSubItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyoutsubitem)， [ToggleMenuFlyoutItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.togglemenuflyoutitem)， [RadioMenuFlyoutItem](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.radiomenuflyoutitem)并[MenuFlyoutSeparator](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyoutseparator) MenuFlyout 的对象。

这些对象如下：

- [MenuFlyoutItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyoutitem) - 执行即时操作。
- [MenuFlyoutSubItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyoutsubitem)— 包含级联菜单项的列表。
- [ToggleMenuFlyoutItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.togglemenuflyoutitem) - 打开或关闭选项。
- [RadioMenuFlyoutItem](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.radiomenuflyoutitem)— 排斥的菜单项之间进行切换。
- [MenuFlyoutSeparator](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyoutseparator) - 直观地区分菜单项。

此示例将创建[MenuFlyout](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyout) ，并使用[ContextFlyout](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.uielement.contextflyout.aspx)属性，该属性可用于大多数控件，以显示上下文菜单作为 MenuFlyout。

````xaml
<Rectangle
  Height="100" Width="100">
  <Rectangle.ContextFlyout>
    <MenuFlyout>
      <MenuFlyoutItem Text="Change color" Click="ChangeColorItem_Click" />
    </MenuFlyout>
  </Rectangle.ContextFlyout>
  <Rectangle.Fill>
    <SolidColorBrush x:Name="rectangleFill" Color="Red" />
  </Rectangle.Fill>
</Rectangle>
````

````csharp
private void ChangeColorItem_Click(object sender, RoutedEventArgs e)
{
    // Change the color from red to blue or blue to red.
    if (rectangleFill.Color == Windows.UI.Colors.Red)
    {
        rectangleFill.Color = Windows.UI.Colors.Blue;
    }
    else
    {
        rectangleFill.Color = Windows.UI.Colors.Red;
    }
}
````

下一个示例几乎完全相同，但该示例使用 [FlyoutBase.ShowAttachedFlyout](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.primitives.flyoutbase.showattachedflyout) 属性将其显示为菜单，而不是使用 [ContextFlyout](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.uielement.contextflyout.aspx) 属性来显示 [MenuFlyout 类](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyout)作为上下文菜单。

````xaml
<Rectangle
  Height="100" Width="100"
  Tapped="Rectangle_Tapped">
  <FlyoutBase.AttachedFlyout>
    <MenuFlyout>
      <MenuFlyoutItem Text="Change color" Click="ChangeColorItem_Click" />
    </MenuFlyout>
  </FlyoutBase.AttachedFlyout>
  <Rectangle.Fill>
    <SolidColorBrush x:Name="rectangleFill" Color="Red" />
  </Rectangle.Fill>
</Rectangle>
````

````csharp
private void Rectangle_Tapped(object sender, TappedRoutedEventArgs e)
{
    FlyoutBase.ShowAttachedFlyout((FrameworkElement)sender);
}

private void ChangeColorItem_Click(object sender, RoutedEventArgs e)
{
    // Change the color from red to blue or blue to red.
    if (rectangleFill.Color == Windows.UI.Colors.Red)
    {
        rectangleFill.Color = Windows.UI.Colors.Blue;
    }
    else
    {
        rectangleFill.Color = Windows.UI.Colors.Red;
    }
}
````

### <a name="light-dismiss"></a>光关闭

光解除如菜单、 上下文菜单和其他浮出控件的控件，捕获内部瞬时 UI 直到关闭的键盘和游戏板焦点。 若要为此行为提供视觉提示，Xbox 上的轻型消除控件将绘制覆盖，以便使 UI 范围之外的可见性变暗。 可以使用 [LightDismissOverlayMode](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.primitives.flyoutbase.lightdismissoverlaymode.aspx) 属性来修改此行为。 默认情况下，瞬时 Ui 将在 Xbox 上绘制浅解除覆盖 (**自动**)，但不是其他设备系列。 您可以选择强制在覆盖区上，要始终**上**或始终**关闭**。

```xaml
<MenuFlyout LightDismissOverlayMode="Off" />
```

## <a name="create-a-menu-bar"></a>创建菜单栏

> [!IMPORTANT]
> 菜单栏需要 Windows 10，版本 1809年 ([SDK 17763](https://developer.microsoft.com/windows/downloads/windows-10-sdk)) 或更高版本，或[Windows 用户界面库](https://docs.microsoft.com/uwp/toolkits/winui/)。

使用相同的元素以创建在菜单栏中，如下所示的菜单弹出菜单。 但是，而不是对中 MenuFlyout MenuFlyoutItem 对象进行分组，您将它们组合 MenuBarItem 元素中。 每个 MenuBarItem 将作为顶级菜单添加到菜单栏。

![菜单栏的示例](images/menu-bar-submenu.png)

> [!NOTE]
> 此示例显示了如何创建 UI 结构，但不显示任何命令的实现。

```xaml
<muxc:MenuBar>
    <muxc:MenuBarItem Title="File">
        <MenuFlyoutSubItem Text="New">
            <MenuFlyoutItem Text="Plain Text Document"/>
            <MenuFlyoutItem Text="Rich Text Document"/>
            <MenuFlyoutItem Text="Other Formats..."/>
        </MenuFlyoutSubItem>
        <MenuFlyoutItem Text="Open..."/>
        <MenuFlyoutItem Text="Save"/>
        <MenuFlyoutSeparator />
        <MenuFlyoutItem Text="Exit"/>
    </muxc:MenuBarItem>

    <muxc:MenuBarItem Title="Edit">
        <MenuFlyoutItem Text="Undo"/>
        <MenuFlyoutItem Text="Cut"/>
        <MenuFlyoutItem Text="Copy"/>
        <MenuFlyoutItem Text="Paste"/>
    </muxc:MenuBarItem>

    <muxc:MenuBarItem Title="View">
        <MenuFlyoutItem Text="Output"/>
        <MenuFlyoutSeparator/>
        <muxc:RadioMenuFlyoutItem Text="Landscape" GroupName="OrientationGroup"/>
        <muxc:RadioMenuFlyoutItem Text="Portrait" GroupName="OrientationGroup" IsChecked="True"/>
        <MenuFlyoutSeparator/>
        <muxc:RadioMenuFlyoutItem Text="Small icons" GroupName="SizeGroup"/>
        <muxc:RadioMenuFlyoutItem Text="Medium icons" IsChecked="True" GroupName="SizeGroup"/>
        <muxc:RadioMenuFlyoutItem Text="Large icons" GroupName="SizeGroup"/>
    </muxc:MenuBarItem>

    <muxc:MenuBarItem Title="Help">
        <MenuFlyoutItem Text="About"/>
    </muxc:MenuBarItem>
</muxc:MenuBar>
```

## <a name="get-the-sample-code"></a>获取示例代码

- [XAML 控件库示例](https://github.com/Microsoft/Xaml-Controls-Gallery) - 以交互式格式查看所有 XAML 控件。
- [XAML 关联菜单示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlContextMenu)

## <a name="related-articles"></a>相关文章

- [MenuFlyout 类](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.menuflyout)
- [菜单栏类](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.menubar)
