---
author: Xansky
description: "介绍了为确保通用 Windows 平台 (UWP) 应用在高对比度主题处于活动状态时可用所需的步骤。"
ms.assetid: FD7CA6F6-A8F1-47D8-AA6C-3F2EC3168C45
title: "高对比度主题"
template: detail.hbs
translationtype: Human Translation
ms.sourcegitcommit: f3da82cab8813653a6ee999976983937649b42b2
ms.openlocfilehash: 30785998d11f09ef94f33789e3e74b0933d9c83e

---

# 高对比度主题  

Windows 支持面向操作系统和应用的用户可能会选择启用的高对比度主题。 高对比度主题使用一块小型的对比色调色板，使界面看起来更加适宜。

**图 1. 在浅色主题和高对比度黑色主题下显示的计算器。**

![在浅色主题和高对比度黑色主题下显示的计算器。](images/high-contrast-calculators.png)


你可以使用“设置”&gt;“轻松使用”&gt;“高对比度”**切换到高度比度主题。

> [!NOTE]
> 不要将高对比度主题与浅色和深色主题混为一谈，浅色和深色主题的调色板更大，但是不被视为拥有高对比度。 有关更多浅色和深色主题，请参阅有关[颜色](../style/color.md)的文章。

尽管常用控件随完整的高对比度支持免费提供，但自定义 UI 时仍需小心谨慎。 最常见的高对比度 bug 通常由硬编码内联控件上的颜色引起。

```xaml
<!-- Don't do this! -->
<Grid Background="#E6E6E6">

<!-- Instead, create BrandedPageBackgroundBrush and do this. -->
<Grid Background="{ThemeResource BrandedPageBackgroundBrush}">
```

在第一个示例中，当 `#E6E6E6` 颜色设置为内联时，网格将在所有主题中保留该背景色。 如果用户切换到高对比度黑色主题，他们希望你的应用有一个黑色背景。 由于 `#E6E6E6` 几乎为白色，所以有些用户可能无法与你的应用进行交互。

在第二个示例中，[**{ThemeResource} 标记扩展**](../xaml-platform/themeresource-markup-extension.md)用来引用 [**ThemeDictionaries**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.resourcedictionary.themedictionaries.aspx)（[**ResourceDictionary**](https://msdn.microsoft.com/library/windows/apps/BR208794) 元素中的一个专用属性）集合中的颜色。 ThemeDictionaries 允许 XAML 根据用户的当前主题自动为你切换颜色。

## 主题字典

当你需要从其系统默认值更改颜色时，可为你的应用创建 ThemeDictionaries 集合。

1. 首先创建正确的管道（如果尚不存在）。 在 App.xaml 中，创建 ThemeDictionaries 集合，其中至少要包含 **Default** 和 **HighContrast**。
2. 在 Default 中，创建所需的 [Brush](http://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.media.brush.aspx) 类型，通常为 SolidColorBrush。 为它提供特定于其用途的 x:Key 名称：
3. 为它分配所需的颜色。
4. 将 Brush 复制到 HighContrast 中。

``` xaml
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.ThemeDictionaries>
            <!-- Default is a fallback if a more precise theme isn't called
            out below -->
            <ResourceDictionary x:Key="Default">
                <SolidColorBrush x:Key="BrandedPageBackgroundBrush" Color="#E6E6E6" />
            </ResourceDictionary>

            <!-- Optional, Light is used in light theme.
            If included, Default will be used for Dark theme -->
            <ResourceDictionary x:Key="Light">
                <SolidColorBrush x:Key="BrandedPageBackgroundBrush" Color="#E6E6E6" />
            </ResourceDictionary>

            <!-- HighContrast is used in all high contrast themes -->
            <ResourceDictionary x:Key="HighContrast">
                <SolidColorBrush x:Key="BrandedPageBackgroundBrush" Color="#E6E6E6" />
            </ResourceDictionary>
        </ResourceDictionary.ThemeDictionaries>
    </ResourceDictionary>
</Application.Resources>
```

最后一步是确定要在高对比度中使用哪种颜色，这将在下一节中进行介绍。

> [!NOTE]
> HighContrast 不是唯一可用的项名。 另外，还有 HighContrastBlack、HighContrastWhite 和 HighContrastCustom。 在大多数情况下，只需使用 HighContrast。

## 高对比度颜色

在“设置”&gt;“轻松使用”&gt;“高对比度”**页面上，默认有 4 个高对比度主题。 

**图 2. 在用户选择某一选项后，该页面将显示预览。**

![高对比度设置](images/high-contrast-settings.png)

**图 3. 可以单击预览上的每个颜色样本来更改其值。 每个颜色样本还直接映射到 XAML 颜色资源。**

![高对比度资源](images/high-contrast-resources.png)

每一个 `SystemColor*Color` 资源都是一个变量，可在用户切换高对比度主题时自动更新颜色。 以下是在何处以及何时使用每个资源的指南。

资源 | 用法
-------- | -----
SystemColorWindowTextColor | 正文、标题、列表；无法与之进行交互的任何文本
SystemColorHotlightColor | 超链接
SystemColorGrayTextColor | 禁用的 UI
SystemColorHighlightTextColor | 正在选择、已选择或当前正在与之进行交互的文本或 UI 的前景色
SystemColorHighlightColor | 正在选择、已选择或当前正在与之进行交互的文本或 UI 的背景色
SystemColorButtonTextColor | 按钮的前景色；可以与之进行交互的任何 UI
SystemColorButtonFaceColor | 按钮的背景色；可以与之进行交互的任何 UI
SystemColorWindowColor | 页面、窗格、弹出窗口和栏的背景
<br/>
通常有助于查看现有应用、“开始”菜单或常用控件，了解其他人如何解决类似于自己面临的高对比度设计问题。

**应做事项**

* 如有可能，请考虑背景/前景配对。
* 当应用正在运行时，在 4 个高对比度主题中都进行测试。 用户切换主题时，应无需重新启动你的应用。
* 保持一致。

**禁止事项**

* 硬编码 HighContrast 主题中的颜色；使用 `SystemColor*Color` 资源。
* 选择具有美学效果的颜色资源。 请记住，它们会随主题变化而变化！
* 不要对辅助性或提示性正文使用 `SystemColorGrayTextColor`。


若要续接前面的示例，你需要选择一个适用于 `BrandedPageBackgroundBrush` 的资源。 因为名称指示它将用于背景，因此 `SystemColorWindowColor` 是一个不错的选择。

``` xaml
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.ThemeDictionaries>
            <!-- Default is a fallback if a more precise theme isn't called
            out below -->
            <ResourceDictionary x:Key="Default">
                <SolidColorBrush x:Key="BrandedPageBackgroundBrush" Color="#E6E6E6" />
            </ResourceDictionary>

            <!-- Optional, Light is used in light theme.
            If included, Default will be used for Dark theme -->
            <ResourceDictionary x:Key="Light">
                <SolidColorBrush x:Key="BrandedPageBackgroundBrush" Color="#E6E6E6" />
            </ResourceDictionary>

            <!-- HighContrast is used in all high contrast themes -->
            <ResourceDictionary x:Key="HighContrast">
                <SolidColorBrush x:Key="BrandedPageBackgroundBrush" Color="{ThemeResource SystemColorWindowColor}" />
            </ResourceDictionary>
        </ResourceDictionary.ThemeDictionaries>
    </ResourceDictionary>
</Application.Resources>
```

接着在应用中，你可以立即设置背景。

```xaml
<Grid Background="{ThemeResource BrandedPageBackgroundBrush}">
```

请注意 `{ThemeResource}` 的两次用法，一次用于引用 `SystemColorWindowColor`，另一次用于引用 `BrandedPageBackgroundBrush`。 两次都需要应用在运行时搭配正确主题。 此时适合测试应用功能。 当你切换到高对比度主题时，网格的背景将自动更新。 当在不同高对比度主题之间切换时，它的背景也随之更新。

## 何时使用边框

在高对比度模式下，页面、窗格、弹出窗口和栏应该都使用 `SystemColorWindowColor` 作为它们的背景。 必要时，请只添加高对比度边框来保留 UI 中的重要边界。

**图 4. 在高对比度模式下，导航窗格和页面共享同一背景色。 必须仅使用高对比度边框将它们分开。**

![从页面其余部分分离的导航窗格](images/high-contrast-actions-content.png)

## 列表项

在高对比度模式下，当将光标悬停在 [ListView](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.listview.aspx) 中的项目上、按下或选择它们时，它们会将自己的背景设置为 `SystemColorHighlightColor`。 复杂的列表项通常有一个 bug，即当将光标悬停在某项上、按下或选择该项时，该列表项的内容无法反转颜色。 这导致无法读取该项。

**图 5. 浅色主题（左）和高对比度黑色主题（右）中的简单列表。 已选中第二项；注意它的文本颜色在高对比度模式下的反转方式。**

![浅色主题和高对比度黑色主题中的简单列表](images/high-contrast-list1.png)



### 带有彩色文本的列表项

在 ListView 的 [DataTemplate](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.itemscontrol.itemtemplate.aspx) 中设置 TextBlock.Foreground 是原因之一。 这样做的目的通常是为了构建视觉层次结构。 Foreground 属性在 [ListViewItem](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.listviewitem.aspx) 上设置，当将光标悬停在该项上、按下或选择该项时，DataTemplate 中的 TextBlocks 继承正确的前景色。 但是，设置 Foreground 将打断这种继承关系。

**图 6. 浅色主题（左）和高对比度黑色主题（右）中的复杂列表。 请注意，在高对比度模式下，所选项目的第二行未能反转。**

![浅色主题和高对比度黑色主题中的复杂列表](images/high-contrast-list2.png)

你可以通过 ThemeDictionaries 集合中的某个 Style，有条件的设置 Foreground，以便解决此问题。 因为 Foreground 并非由 HighContrast 中的 SecondaryBodyTextBlockStyle 设置，所以它的颜色将正确反转。

```xaml
<!-- In App.xaml... -->
<ResourceDictionary.ThemeDictionaries>
    <ResourceDictionary x:Key="Default">
        <Style
            x:Key="SecondaryBodyTextBlockStyle"
            TargetType="TextBlock"
            BasedOn="{StaticResource BodyTextBlockStyle}">
            <Setter Property="Foreground" Value="{StaticResource SystemControlForegroundBaseMediumBrush}" />
        </Style>
    </ResourceDictionary>

    <ResourceDictionary x:Key="Light">
        <Style
            x:Key="SecondaryBodyTextBlockStyle"
            TargetType="TextBlock"
            BasedOn="{StaticResource BodyTextBlockStyle}">
            <Setter Property="Foreground" Value="{StaticResource SystemControlForegroundBaseMediumBrush}" />
        </Style>
    </ResourceDictionary>

    <ResourceDictionary x:Key="HighContrast">
        <!-- The Foreground Setter is omitted in HighContrast -->
        <Style
            x:Key="SecondaryBodyTextBlockStyle"
            TargetType="TextBlock"
            BasedOn="{StaticResource BodyTextBlockStyle}" />
    </ResourceDictionary>
</ResourceDictionary.ThemeDictionaries>

<!-- Usage in your DataTemplate... -->
<DataTemplate>
    <StackPanel>
        <TextBlock Style="{StaticResource BodyTextBlockStyle}" Text="Double line list item" />

        <!-- Note how ThemeResource is used to reference the Style -->
        <TextBlock Style="{ThemeResource SecondaryBodyTextBlockStyle}" Text="Second line of text" />
    </StackPanel>
</DataTemplate>
```

### 带有按钮和链接的列表项

有时，列表项中包含着更加复杂的控件，如 [HyperlinkButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.hyperlinkbutton.aspx) 或 [Button](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.button.aspx)。 这些控件在有光标悬停、按下或选择时有各自的状态，这在列表项上不起作用。 超链接在高对比度黑色模式下也是黄色，这导致当某个列表项上有光标悬停、按下或选择时，很难读取这些超链接。

**图 7. 请注意在高对比度模式中读取超链接的难度。**

![浅色主题和高对比度黑色主题中带有超链接的列表](images/high-contrast-list3.png)

解决方案是在高对比度模式中将 DataTemplate 的背景设置为 `SystemColorWindowColor`。 这样将产生高对比度的边框效果。

```xaml
<!-- In App.xaml... -->
<ResourceDictionary.ThemeDictionaries>
    <ResourceDictionary x:Key="Default">
        <SolidColorBrush x:Key="HighContrastOnlyBackgroundBrush" Color="Transparent" />
    </ResourceDictionary>

    <ResourceDictionary x:Key="HighContrast">
        <SolidColorBrush x:Key="HighContrastOnlyBackgroundBrush" Color="{ThemeResource SystemColorWindowColor}" />
    </ResourceDictionary>
</ResourceDictionary.ThemeDictionaries>

<!-- Usage in your ListView... -->
<ListView>
    <ListView.ItemContainerStyle>
        <Style TargetType="ListViewItem">
            <!-- Causes the DataTemplate to fill the entire width and height
            of the list item -->
            <Setter Property="HorizontalContentAlignment" Value="Stretch" />
            <Setter Property="VerticalContentAlignment" Value="Stretch" />

            <!-- Padding is handled in the DataTemplate -->
            <Setter Property="Padding" Value="0" />
        </Style>
    </ListView.ItemContainerStyle>
    <ListView.ItemTemplate>
        <DataTemplate>
            <!-- Margin of 2px allows some of the ListViewItem's background
            to shine through. An additional left padding of 10px puts the
            content a total of 12px from the left edge -->
            <StackPanel
                Margin="2,2,2,2"
                Padding="10,0,0,0"
                Background="{ThemeResource HighContrastOnlyBackgroundBrush}">

                <!-- Foreground is explicitly set so that it doesn't
                disappear on hovered, pressed, or selected -->
                <TextBlock
                    Foreground="{ThemeResource SystemControlForegroundBaseHighBrush}"
                    Text="Double line list item" />

                <HyperlinkButton Content="Hyperlink" />
            </StackPanel>
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>
```
**图 8. 当你的列表项中有更复杂的控件时，使用边框效果非常合适。**

![浅色主题和高对比度黑色主题中带有超链接的列表，已修复](images/high-contrast-list4.png)



## 检测高对比度

你可以使用 [**AccessibilitySettings**](https://msdn.microsoft.com/library/windows/apps/BR242237) 类的成员，以编程方式检查当前主题是否为高对比度主题。

> [!NOTE]
> 确保从初始化应用且已经显示内容的范围内调用 **AccessibilitySettings** 构造函数。

## 相关主题  
* [辅助功能](accessibility.md)
* [UI 对比度和设置示例](http://go.microsoft.com/fwlink/p/?linkid=231539)
* [XAML 辅助功能示例](http://go.microsoft.com/fwlink/p/?linkid=238570)
* [XAML 高对比度示例](http://go.microsoft.com/fwlink/p/?linkid=254993)
* [**AccessibilitySettings**](https://msdn.microsoft.com/library/windows/apps/BR242237)



<!--HONumber=Aug16_HO3-->


