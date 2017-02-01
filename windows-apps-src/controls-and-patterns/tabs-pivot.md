---
author: Jwmsft
Description: "利用表和透视表，用户可以在经常访问的内容之间导航。"
title: "表和透视表"
ms.assetid: 556BC70D-CF5D-4295-A655-D58163CC1824
label: Tabs and pivots
template: detail.hbs
translationtype: Human Translation
ms.sourcegitcommit: b258771c887d4422433522344b11130b7e9ed1e6
ms.openlocfilehash: 865969a7c965a502acd9fe24df28128399efd380

---
# <a name="pivot-and-tabs"></a>透视表和表

<link rel="stylesheet" href="https://az835927.vo.msecnd.net/sites/uwp/Resources/css/custom.css"> 

透视表控件和相关的表模式用于导航经常访问的不同内容类别。 透视表允许在两个或多个内容窗格之间进行导航，并且依靠文本标题来表明内容的不同部分。

![表示例](images/pivot_Hero_main.png)

表是透视表的视觉变体，它使用图标和文本的组合或纯图标来表明部分内容。 表使用 [**Pivot**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivot.aspx) 控件生成。 [**透视表示例**](http://go.microsoft.com/fwlink/p/?LinkId=619903) 显示如何将透视表控件自定义为表模式。

<div class="important-apis" >
<b>重要的 API</b><br/>
<ul>
<li>[**透视表类**](https://msdn.microsoft.com/library/windows/apps/dn608241)</li>
</ul>
</div>


## <a name="the-pivot-pattern"></a>透视表模式

在使用透视表生成应用时，有一些关键设计变量需要考虑。

- **标题标签。**  标题可以是带有文本的图标、纯图标或纯文本。
- **标题对齐方式。**  标题可以左对齐，也可以居中对齐。
- **顶级或次级导航。**  透视表可以用于任一级别的导航。 （可选）[导航窗格](nav-pane.md)可充当主要级别，而透视表可作为辅助级别。
- **触摸手势支持。**  对于支持触摸手势的设备，你可以使用以下两组交互之一在不同的内容类别之间进行导航：
    1. 点击表/透视表标题以导航到该类别。
    2. 在内容区域上向左或向右轻扫，以导航到相邻类别。

## <a name="examples"></a>示例

手机上的透视表控件。

![透视表示例](images/pivot_example.png)

“闹钟和时钟”应用中的表模式。

![“闹钟和时钟”中的表模式示例](images/tabs_alarms-and-clock.png)

## <a name="create-a-pivot-control"></a>创建透视表控件

[**Pivot**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivot.aspx) 控件随附本部分中所述的基本功能。

此 XAML 使用 3 个部分的内容创建基本透视表控件。

```xaml
<Pivot x:Name="rootPivot" Title="Pivot Title">
    <PivotItem Header="Pivot Item 1">
        <!--Pivot content goes here-->
        <TextBlock Text="Content of pivot item 1."/>
    </PivotItem>
    <PivotItem Header="Pivot Item 2">
        <!--Pivot content goes here-->
        <TextBlock Text="Content of pivot item 2."/>
    </PivotItem>
    <PivotItem Header="Pivot Item 3">
        <!--Pivot content goes here-->
        <TextBlock Text="Content of pivot item 3."/>
    </PivotItem>
</Pivot>
```

### <a name="pivot-items"></a>透视表项目

透视表是一个 [**ItemsControl**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.itemscontrol.aspx)，因此可以包含任何类型的项目集合。 你添加到透视表的任何非显式 [**PivotItem**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivotitem.aspx) 的项目都隐式包装在 PivotItem 中。 由于透视表经常用于在内容页面之间导航，因此通常使用 XAML UI 元素直接填充 [**Items**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.itemscontrol.items.aspx) 集合。 或者，你可以将 [**ItemsSource**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.itemscontrol.itemssource.aspx) 属性设置为数据源。 ItemsSource 中绑定的项目可以属于任何类型，但如果它们不是显式 PivotItems，则必须定义 [**ItemTemplate**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.itemscontrol.itemtemplate.aspx) 和 [**HeaderTemplate**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivot.headertemplate.aspx) 来指定这些项目的显示方式。

你可以使用 [**SelectedItem**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivot.selecteditem.aspx) 属性获取或设置透视表的活动项目。 使用 [**SelectedIndex**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivot.selectedindex.aspx) 属性获取或设置活动项目的索引。

### <a name="pivot-headers"></a>透视表标题

你可以使用 [**LeftHeader**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivot.leftheader.aspx) 和 [**RightHeader**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.pivot.rightheader.aspx) 属性将其他控件添加到透视表标题。

### <a name="pivot-interaction"></a>透视表交互

该控件的特色之处在于以下触摸手势交互：

-   通过点击透视表项目标题，可导航到该标题的部分内容。
-   通过在透视表项目标题上向左或向右轻扫，可导航到相邻部分。
-   通过在部分内容上向左或向右轻扫，可导航到相邻部分。
![在部分内容上向左轻扫的示例](images/pivot_w_hand.png)

该控件有以下两种模式：

**固定不动**

-   当所有透视表标题都适合所允许的空间时，透视表将固定不动。
-   点击某个透视表标签即可导航到相应的页面，即使透视表无法自行移动也是如此。 活动透视表将突出显示。

<div class="microsoft-internal-note">
我们特别建议阻止项目在 10 英尺的环境中旋转。 如果要在 Xbox 上运行应用，请将新的 `IsHeaderItemsCarouselEnabled` 属性设置为 False。
</div>

**旋转**

-   当所有透视表标题不适合所允许的空间时，可旋转透视表。
-   点击某个透视表标签即可导航到相应的页面，并且活动透视表标签将旋转至第一个位置。
-   从最后一个到第一个透视表部分的旋转循环中的透视表项目。

<div class="microsoft-internal-note">
### 透视表焦点

默认情况下，透视表标题上的键盘焦点使用下划线表示。

![默认焦点为选择的标题添加下划线](images/pivot_focus_selectedHeader.png)

自定义透视表和将下划线合并到标题选择视觉的应用可以使用新的 `HeaderFocusVisualPlacement` 属性，以更改默认属性。 当为 `HeaderFocusVisualPlacement=\"ItemHeaders\"` 时，将在整个标题窗格外围绘制焦点。

![ItemsHeader 选项在所有透视表标题外围绘制焦点矩形](images/pivot_focus_headers.png)
</div>

## <a name="recommendations"></a>建议

-   根据屏幕大小来选择表/透视表标题的对齐方式。 对于宽度低于 720 像素的屏幕，通常使用中心对齐效果更佳；而对于宽度高于 720 像素的屏幕，在大多数情况下都推荐使用左对齐。
-   当使用旋转（来回旋转）模式时，避免使用 5 个以上的标题，因为超过 5 个标题的循环可能会令人困惑。
-   仅当透视表项目具有不同的图标时，使用表模式。
-   在透视表项目标题中包含文本，以帮助用户理解每个透视表部分的含义。 图标不一定对所有用户都是无须解释的。

## <a name="get-the-sample-code"></a>获取示例代码
- [透视表示例](http://go.microsoft.com/fwlink/p/?LinkId=619903)<br/>
    查看如何将透视表控件自定义为表模式。
- [XAML UI 基本示例](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/XamlUIBasics)<br/>
    以交互式格式查看所有 XAML 控件。

## <a name="related-topics"></a>相关主题
- [导航设计基础知识](../layout/navigation-basics.md)
- [**透视表示例**](http://go.microsoft.com/fwlink/p/?LinkId=619903)



<!--HONumber=Dec16_HO1-->


