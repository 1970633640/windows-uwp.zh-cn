---
author: Jwmsft
Description: "提供了顶级导航，同时节省屏幕空间。"
title: "导航窗格指南"
ms.assetid: 8FB52F5E-8E72-4604-9222-0B0EC6A97541
label: Nav pane
template: detail.hbs
translationtype: Human Translation
ms.sourcegitcommit: a3924fef520d7ba70873d6838f8e194e5fc96c62
ms.openlocfilehash: 3aed1658f0a9fa81677f5089d343969840ab33f1

---
# <a name="nav-panes"></a>导航窗格

<link rel="stylesheet" href="https://az835927.vo.msecnd.net/sites/uwp/Resources/css/custom.css"> 

导航窗格（或简称“导航”窗格）是一种可容纳许多顶级导航项目，同时又节省屏幕空间的导航模式。 导航窗格广泛用于移动应用，但在较大的屏幕上也效果良好。 在用作覆盖层时，该窗格保持折叠状态并且不遮挡内容，直到用户按下按钮（这对于较小的屏幕很方便）。 当在停靠模式下使用窗格时，它保持打开状态，这在有足够屏幕空间的情况下可提高效用。

![导航窗格示例](images/navHero.png)

<div class="important-apis" >
<b>重要的 API</b><br/>
<ul>
<li>[**SplitView 类**](https://msdn.microsoft.com/library/windows/apps/dn864360)</li>
<li> </li>
<li> </li>
<li> </li>
<li> </li>
<li> </li>
</ul>
</div>


## <a name="is-this-the-right-pattern"></a>这是正确的模式吗？

导航窗格适用于以下情况：

-   具有许多相似类型的高级导航项目的应用。 例如具有“橄榄球”、“棒球”、“篮球”、“足球”等类别的体育应用。
-   跨应用提供一致的导航体验。 导航窗格应仅包括导航元素，而非操作。
-   中等数量到大量 (5-10+) 的顶级导航类别。
-   保留屏幕空间（作为覆盖层）。
-   不经常访问的导航项。 （作为覆盖层）。

## <a name="building-a-nav-pane"></a>生成导航窗格

导航窗格模式包括导航类别窗格、内容区域以及打开或关闭窗格的可选按钮。 生成导航窗格最简单的方法是使用[拆分视图控件](split-view.md)，它附带了一个空窗格和始终可见的内容区域。

若要试用实现此模式的代码，请从 GitHub 下载 [XAML 导航解决方案](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlNavigation)。

<div class="microsoft-internal-note">
导航窗格和汉堡的红线在 [UNI](http://uni/DesignDepot.FrontEnd/#/Search?c=t&t=Windows%2BRS1%2BControls&f=NavPane_Hamburger) 上可用。
</div>

### <a name="pane"></a>窗格

导航类别的标头转到窗格中。 应用设置和帐户管理的入口点（如果适用）也转到窗格中。 导航标题通常是用户可从中进行选择的项目列表。

![导航窗格的窗格示例](images/nav_pane_expanded.png)

### <a name="content-area"></a>内容区域

内容区域是显示选定导航位置的信息的位置。 它可以包含个别元素或其他子级别导航。

### <a name="button"></a>按钮

在显示时，按钮允许用户打开和关闭窗格。 该按钮在固定位置中保持可见，不随窗格移动。 建议将该按钮放在应用的左上角。 导航窗格按钮是可视化的，其形式为三条堆叠的水平线，通常称为“汉堡包”按钮。

![导航窗格按钮的示例](images/nav_button.png)

该按钮通常与文本字符串相关联。 在应用顶层，应用标题可以显示在该按钮旁边。 在较低级别的应用上，文本字符串可能是用户当前所在页面的标题。

## <a name="nav-pane-variations"></a>导航窗格变体

导航窗格中有三种模式：覆盖、精简和内联。 精简可以根据需要进行折叠和扩展。 当压缩时，窗格始终显示为可以扩展的细窄长条。 默认情况下，内联窗格保持打开状态。

### <a name="overlay"></a>覆盖

-   覆盖层可在任何屏幕大小上以纵向方向或横向方向使用。 在其默认（折叠）状态下，覆盖层不占据任何空间，仅显示按钮。
-   提供可节省屏幕空间的按需导航。 非常适合用于手机和平板手机。
-   该窗格默认处于隐藏状态，仅按钮可见。
-   通过按导航窗格按钮可打开和关闭覆盖层。
-   展开状态是暂时的，当进行选择时、使用后退按钮时或用户点击窗格以外的位置时，将取消展开状态。
-   覆盖可覆盖在内容上方，并且不会重排内容。

### <a name="compact"></a>精简

-   精简模式可以指定为 `CompactOverlay`，表示在打开时覆盖内容，或者是 `CompactInline`，表示将内容挤出原来的位置。 我们建议使用 CompactOverlay。
-   精简窗格可以在使用少量的屏幕空间时指示选定的位置。
-   此模式更适用于中等大小的屏幕，如平板电脑。
-   默认情况下，仅可通过导航图标关闭窗格，并且该按钮可见。
-   按导航窗格按钮可以打开和关闭窗格，其行为与覆盖或内联相似，具体取决于指定的显示模式。
-   选择的内容将显示在列表图标上，以突出显示用户在导航树中所在的位置。

### <a name="inline"></a>内联

-   导航窗格保持打开状态。 此模式更适合较大的屏幕。
-   支持与窗格之间的拖放方案。
-   此状态不需要导航窗格按钮。 如果使用该按钮，将推出内容区域，并且该区域内的内容将重排。
-   选择的内容将显示在列表项上，以强调用户在导航树中所在的位置。

## <a name="adaptability"></a>适应性

为了最大程度地实现各种设备的可用性，我们推荐使用[断点](../layout/screen-sizes-and-breakpoints-for-responsive-design.md)，并且根据应用窗口的宽度调整导航窗格的模式。
-   较小的窗口
   -   小于或等于 640px 宽度。
   -   导航窗格应该处在覆盖模式中，默认情况下处于关闭状态。
-   中等大小的窗口
   -   大于 640px 并且小于或等于 1007px 宽度。
   -   导航窗格应该处在长条模式中，默认情况下处于关闭状态。
-   较大窗口
   -   大于 1007px 宽度。
   -   导航窗格应该处于停靠模式下，默认情况下处于打开状态。

## <a name="tailoring"></a>定制

若要优化应用的 [10 英尺体验](http://go.microsoft.com/fwlink/?LinkId=760736)，请考虑更改导航元素的可视外观以定制导航窗格。 让用户注意选定的导航项或关注的导航项的重要性可能会更大，具体取决于交互上下文。 对于游戏板是最常用的输入设备的 10 英尺体验，确保用户可以在屏幕上轻松跟踪当前关注的项目的位置非常重要。

![定制的导航窗格项示例](images/nav_item_states.png)

## <a name="related-topics"></a>相关主题

* [拆分视图控件](split-view.md)
* [大纲/细节](master-details.md)
* [导航基础知识](https://msdn.microsoft.com/library/windows/apps/dn958438)
 

 



<!--HONumber=Dec16_HO2-->


