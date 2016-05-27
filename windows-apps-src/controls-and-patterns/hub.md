---
author: Jwmsft
Description: 中心控件使用分层导航模式支持具有相关信息体系结构的应用。
title: 中心控件
ms.assetid: F1319960-63C6-4A8B-8DA1-451D59A01AC2
label: Hub
template: detail.hbs
---
# 中心控件/模式


利用中心控件，你可以将应用内容整理到不同但又相关的区域或类别中。 中心的各个区域可按首选顺序遍历，并且可用作更具体体验的起始点。

![中心示例](images/hub_example_tablet.png)

中心的内容可以显示在功能强大的平移视图中，这样用户一眼就能看见新增内容、可用功能和相关信息。 中心通常具有一个页面标头，而对于多个内容区域，每个区域都具有一个区域标头。

中心控件具有多个功能，这些功能适用于生成内容导航模式。

-   **视觉导航**

    使用中心可以让内容以简洁且易于浏览的多样化矩阵形式进行显示。

-   **分类**

    每个中心区域都允许其内容按逻辑顺序排列。

-   **混合内容类型**

    借助混合内容类型，变量资产大小和比率可以通用。 中心允许每个内容类型以其独特的方式整齐地排列在每个中心区域中。

-   **变量页面和内容宽度**

    作为全景模型，中心允许其区域宽度发生变化。 这非常适合不同深度的内容，并使从少数到多数的项目也可以很好地进行格式化。

-   **弹性体系结构**

    如果你希望使应用体系结构一目了然，你可以使所有频道内容都与中心区域摘要相符。

<span class="sidebar_heading" style="font-weight: bold;">重要的 API</span>

-   [**Hub 类 (XAML)**](https://msdn.microsoft.com/library/windows/apps/dn251843)
-   [**HubSection 类 (XAML)**](https://msdn.microsoft.com/library/windows/apps/dn251845)
-   [**Hub 对象 (HTML)**](https://msdn.microsoft.com/library/windows/apps/dn255137)


## 这是正确的控件吗？

对于显示按层次结构排列的大量内容，使用中心控件会很有效。 中心针对浏览和发现新内容设置了优先级，使它们可用于显示应用商店或媒体集合的中项目。

中心只不过是你可以使用的几个导航元素之一；若要了解有关导航模式和其他导航元素的详细信息，请参阅[通用 Windows 平台 (UWP) 应用的导航设计基础知识](https://msdn.microsoft.com/library/windows/apps/dn958438)。

## 中心体系结构

中心控件具有一个分层导航模式，该模式支持具有相关信息体系结构的应用。 中心由不同类别的内容构成，每个类别都映射到应用的区域页中。 区域页可以采用任何形式显示，这些形式必须能够最好地表示该方案及该区域所包含的内容。

![带有好友应用的分层食物的线框](images/navigation_diagram_food_with_friends_app_new.png)

## 布局和平移/滚动

有多种方法可设置中心的内容布局并对其进行导航；只需确保中心的内容列表始终沿着与中心滚动方向相垂直的方向平移。

**水平平移**

![水平平移中心示例](images/controls_hub_horizontal_pan.png)
**垂直平移**

![垂直平移中心示例](images/controls_hub_vertical_pan.png)
**通过垂直滚动列表/网格的水平平移**

![通过垂直滚动列表来水平平移中心的示例](images/controls_hub_horizontal_vertical_scroll.png)
**水平滚动列表/网格的垂直平移**

![水平平移中心示例](images/controls_hub_vertical_horizontal_scroll.png)

## 示例

中心提供了大量的设计灵活性。 这可让你设计具有各种诱人和丰富视觉体验的应用。 你可以将展示图像或内容部分用于第一组；对可水平和垂直裁剪而不丢失关注中心的展示磁贴使用大图像。 下面是单个展示图像的示例，以及该图像如何能够针对横向、纵向和较窄宽度进行裁剪。

![针对不同窗口大小进行裁剪的展示图像](images/hub_hero_cropped2.png)

在移动设备上，一次只能有一个中心区域可见。

![小屏幕上的中心模式示例](images/phone_hub_example.png)

## 建议

-   若要让用户知道中心区域中有更多内容，我们建议裁剪内容，以便查看一定数量的内容。
-   根据应用的需求，你可以将多个中心区域添加到中心控件，其中每一个都提供一种具有独特目的的功能。 例如，一个区域可能包含一系列链接和控件，而另一个则可能是缩略图的存储库。 用户可以使用内置于中心控件的手势支持在这些区域之间平移。
-   动态重排内容是使其适应不同窗口大小的最佳方式。
-   如果有许多中心区域，请考虑添加语义式缩放。 当应用调整至较窄宽度时，这还便于查找各个区域。
-   我们不建议通过一个中心区域中的项进入另一个中心；你可以改用交互式标头导航至其他中心区域或页面。
-   中心是一个起始点，可进行自定义以满足你的应用的需求。 你可以更改中心的以下方面：
    -   区域数量
    -   每部分中的内容类型
    -   各部分的放置和顺序
    -   部分的大小
    -   各部分之间的间距
    -   部分与中心的顶部或底部之间的间距
    -   标题和内容中的文本样式和大小
    -   背景、区域、区域标题和区域内容的颜色



## 相关文章

- [导航基础知识](https://msdn.microsoft.com/library/windows/apps/dn958438)
- [**Windows.UI.Xaml.Controls Hub 类**](https://msdn.microsoft.com/library/windows/apps/dn251843)
- [XAML 中心控件示例](http://go.microsoft.com/fwlink/p/?LinkID=310072)
- [使用中心](https://msdn.microsoft.com/library/windows/apps/xaml/dn308518)


<!--HONumber=May16_HO2-->


