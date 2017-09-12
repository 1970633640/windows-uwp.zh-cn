---
author: mijacobs
Description: "此文章将从设计角度介绍通用 Windows 平台 (UWP) 的功能、优点和要求。 了解平台为你免费提供了哪些内容，以及可供你支配的工具。"
title: "通用 Windows 平台 (UWP) 应用设计（Windows 应用）简介"
ms.assetid: 50A5605E-3A91-41DB-800A-9180717C1E86
label: Intro to UWP app design
template: detail.hbs
op-migration-status: ready
ms.author: mijacobs
ms.date: 08/9/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.openlocfilehash: 8db6dbe00c20b6371ae7007f07e628d16467ea9d
ms.sourcegitcommit: 0d5b3daddb3ae74f91178c58e35cbab33854cb7f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2017
---
#  <a name="introduction-to-uwp-app-design"></a>UWP 应用设计简介

<link rel="stylesheet" href="https://az835927.vo.msecnd.net/sites/uwp/Resources/css/custom.css">

通用 Windows 平台 (UWP) 应用可以在任何基于 Windows 的设备（从手机到平板电脑或电脑）上运行。 

设计一个在此类型号各异的设备上都外观精美的应用，可能是一项较大的挑战。 幸运的是，通用 Windows 平台 (UWP) 提供了一组内置功能和通用构建基块，可帮助你创建适用于各种设备、屏幕和输入法的 UX。 本文将介绍 UWP 应用的 UI 功能和优势，并为创建你的第一个 UWP 应用提供一些高级设计指南。 

## <a name="video-summary"></a>视频摘要

> [!VIDEO https://channel9.msdn.com/Blogs/One-Dev-Minute/Designing-Universal-Windows-Platform-apps/player]


<!--
![windows-powered devices](images/1894834-hig-device-primer-01-500.png)
-->

<!--
![A design for an app that runs on windows phone, tablets, and pcs](images/food-truck-finder/uap-foodtruck--md-detail.png)
-->


## <a name="uwp-features"></a>UWP 功能

我们先看一下你将在创建 UWP 应用时获得的一些功能。

### <a name="effective-pixels-and-scaling"></a>有效像素和缩放

UWP 应用会自动调整控件、字体和其他 UI 元素的大小，以使它们在所有设备上清晰可见并易于交互。

当你的应用在设备上运行时，系统将使用算法来使 UI 元素在屏幕上的显示方式规范化。 此缩放算法考虑了观看距离和屏幕密度（每英寸像素），以针对感知大小（而不是物理大小）进行优化。 该缩放算法确保用户可从 10 英尺远处识别 Surface Hub 上高 24 像素的字体，正如从几英寸远处识别 5 英寸手机上高 24 像素的字体。

![不同设备的观看距离](images/1910808-hig-uap-toolkit-03.png)

基于缩放系统的工作原理，在设计 UWP 应用时，要以*有效像素*而不是实际物理像素为单位进行设计。 那么，这如何影响你设计应用的方式呢？

-   在设计时，你可以忽略像素密度和实际屏幕分辨率。 而是针对同一大小级别的有效分辨率（以有效像素为单位的分辨率）进行设计（有关详细信息，请参阅 [屏幕大小和断点文章](screen-sizes-and-breakpoints-for-responsive-design.md)）。

-   当系统缩放 UI 时，会按 4 的倍数进行缩放。 若要确保清晰的外观，将你的设计贴靠到 4x4 像素网格：将 UI 元素的边距、大小和位置设置为 4 个有效像素的倍数。 请注意，文本不会有此要求；文本可以是任何大小和位置。 

下图显示了映射到 4x4 像素网格的设计元素。 设计元素将始终具有清晰、尖锐的边缘。

![贴靠到 4x4 像素网格](images/rsp-design/epx-4pixelgood.png)

> [!TIP]
> 在使用图像编辑程序创建屏幕原型时，将 DPI 设置为 72，并将图像尺寸设置为目标大小级别的有效分辨率。 要获得大小类和有效分辨率的列表，请参阅[屏幕大小和断点文章](screen-sizes-and-breakpoints-for-responsive-design.md)。


### <a name="universal-input-and-smart-interactions"></a>通用输入和智能交互

UWP 中的另一个内置功能是通过智能交互启用通用输入。 尽管可以针对特定输入模式和设备设计应用，但并不需要这样做。 这是因为默认情况下，通用 Windows 应用依赖于智能交互。 这意味着你可以围绕单击交互进行设计，而无需知道或定义该单击是来自实际的鼠标单击还是手指点按。

### <a name="universal-controls-and-styles"></a>通用控件和样式


UWP 还提供了一些有用的构建基块，可使针对多个设备系列设计应用变得更简单。

-   **通用控件**

    UWP 提供一组通用控件，可保证在所有支持 Windows 的设备上良好工作。 这组通用控件包括从常用窗体控件（如单选按钮和文本框）到复杂控件（如可从数据流和模板生成项目列表的网格视图和列表视图）的一切内容。 这些控件是输入感知的，并且针对每个设备系列部署了输入可供性、事件状态和整体功能的适当组合。

    有关这些控件的完整列表和你可以从中创建的模式，请参阅[控件和模式](https://dev.windows.com/design/controls-patterns)部分。

-   **通用样式**

    UWP 应用自动获取一组默认样式，可为你提供以下功能：

    -   一组样式，可自动为应用提供浅色或深色主题（任你选择）并且可融合用户的主题色首选项。

        ![浅色和深色主题](images/1910808-hig-uap-toolkit-01.png)

    -   基于 Segoe 的字型渐变，可确保应用文本在所有设备上都清晰可见。
    -   交互的默认动画。
    -   对高对比度模式的自动支持。 我们在设计样式时牢记高对比度，因此，当你的应用处于高对比度模式的设备上运行时，它将能够正确显示。
    -   对其他语言的自动支持。 我们的默认样式为 Windows 支持的每种语言自动选择正确的字体。 你甚至可以在同一个应用中使用多种语言，而且它们能够正确显示。
    -   对 RTL 阅读顺序的内置支持。

    你可以自定义这些默认样式来个性化你的应用，或者可以将它们完全替换为你自己的内容来创建独特的视觉体验。 例如，下面是一个具有独特视觉样式的天气应用设计：

    ![一个具有其自己的视觉样式的天气应用](images/weather/uwp-weather-tab-phone-700.png)

## <a name="uwp-and-the-fluent-design-system"></a>UWP 和 Fluent 设计系统

 Fluent 设计系统可帮助你创建包含光线、深度、动画、材料和比例的现代、简洁的 UI。 Fluent 设计正应用于 Windows 10 设备和应用，以创造富有吸引力的美好直观体验。 
 
 如何将 Fluent 设计合并到你的应用中？ 我们将不断添加新的控件和功能，以便轻松地进行操作。 以下是适用于 UWP 的最新 Fluent 设计功能的列表：  

* [亚克力](../style/acrylic.md)是一种可以创造半透明表面的画笔。
* [视差](../style/parallax.md)将三维透视、深度和移动效果添加到诸如列表之类的滚动内容中。
* [展示](../style/reveal.md)使用灯光创建悬停效果以照亮交互 UI 元素。 
* [连接的动画](../style/connected-animation.md)提供细腻的场景转换，以通过维护上下文并提供连续性来提高可用性。 

我们还更新了[设计指南](https://developer.microsoft.com/windows/apps/design)（你当前正在阅读），使它们基于 Fluent 设计原则。

## <a name="the-anatomy-of-a-typical-uwp-app"></a>典型 UWP 应用的结构

既然我们已介绍了 UWP 应用的构建基块，接下来让我们看一下如何将它们组合在一起来创建 UI。

现代用户界面很复杂，它由文本、形状、颜色和动画组成，而它们归根结底由你在所用设备的屏幕中的各个像素组成。 在开始设计用户界面时，你可能面临众多选择。

为使事情变得更简单，让我们从设计角度定义应用结构。 假设应用由屏幕和页面组成。 每个页面都具有一个用户界面，它由三种类型的 UI 元素组成：导航、命令和内容元素。



<table class="uwpd-noborder" >
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><img src="images/1895065-hig-anatomyofanapp-02.png" alt="Navigation, command, and content areas of an address book app" /></p>
<p></p></td>
<td align="left"><strong>导航元素</strong>
<p>导航元素帮助用户选择他们希望显示的内容。 导航元素示例包括[表和透视表](../controls-and-patterns/tabs-pivot.md)、[超链接](../controls-and-patterns/hyperlinks.md)和[导航窗格](../controls-and-patterns/navigationview.md)。</p>
<p>[导航设计基础知识](navigation-basics.md)文章中详细介绍了导航元素。</p>
<strong>命令元素</strong>
<p>命令元素启动操作，例如处理、保存或共享内容。 命令元素示例包括[按钮](../controls-and-patterns/buttons.md)和[命令栏](../controls-and-patterns/app-bars.md)。 命令元素还可以包括屏幕上实际不可见的键盘快捷方式。</p>
<p>[命令设计基础知识](commanding-basics.md)文章中详细介绍了命令元素。</p>
<strong>内容元素</strong>
<p>内容元素显示应用内容。 对于绘画应用，内容可能是一个图形；对于资讯应用，内容可能是一篇新闻报道。</p>
<p>[内容设计基础知识](content-basics.md)文章中详细介绍了内容元素。</p></td>
</tr>
</tbody>
</table>

 

最低要求：应用具有一个初始屏幕和一个用于定义用户界面的主页。 典型的应用将具有多个页面和屏幕，但各个页面的导航、命令和内容元素可能有所不同。

在为你的应用决定正确的 UI 元素时，可能还要考虑将要运行应用的设备和屏幕大小。

## <a name="tailoring-your-app-for-specific-devices-and-screen-sizes"></a>针对特定设备和屏幕大小定制你的应用。

UWP 应用使用有效像素保证你的设计元素清晰可见，并可在所有支持 Windows 的设备上使用。 那么，为什么你还想要针对特定设备系列自定义应用 UI 呢？

**注意**  
在执行进一步操作之前，Windows 不会提供可使应用检测到运行该应用的特定设备的方法。 但它可以指示运行了该应用的设备系列（移动设备、桌面设备等）、有效分辨率，以及应用的可用屏幕空间大小（应用窗口大小）。

 

-   **最有效地利用空间并减少导航需要**

    如果你设计了一个在小屏幕设备（如手机）上十分美观的应用，则该应用将可在显示屏大得多的电脑上使用，但可能会浪费一些空间。 当屏幕大小超过某个值时，你可以自定义应用以显示更多内容。 例如，某个购物应用在手机上可能一次显示一个商品类别，但在 PC 或笔记本电脑上可以同时显示多个类别和产品。

    通过在屏幕上放置更多内容，你可以减少用户需要执行的导航次数。

-   **利用设备的功能**

    某些设备可能具有特定的设备功能。 例如，手机很可能具有位置传感器和相机，而 PC 可能两者皆无。 你的应用可以检测到哪些功能可用，并启用使用它们的功能。

-   **输入优化**

    通用控件库适用于所有输入类型（触摸、触笔、键盘、鼠标），但你仍然可以通过重新排列 UI 元素来优化某些输入类型。 例如，如果将导航元素放置在屏幕底部，则手机用户将更容易访问它们，但大多数电脑用户希望在屏幕顶部看到导航元素。

## <a name="responsive-design-techniques"></a>响应式设计技术


在针对特定屏幕宽度优化应用 UI 时，假设你要创建一个响应式设计。 下面是可用于自定义应用 UI 的六个响应式设计技术。

### <a name="reposition"></a>重新放置

你可以修改应用 UI 元素的位置和放置方式，以充分利用每台设备。 在此示例中，手机或平板手机上的纵向视图需要一个滚动 UI，因为一次只显示一个完整的框架。 当将应用转换到屏幕上允许两个完整框架的设备时，无论是在纵向模式还是横向模式下，框架 B 都可以占用一个专用空间。 如果你要将网格用于放置，则可以继续使用重新放置 UI 元素时的同一网格。

![重新放置](images/rsp-design/rspd-reposition.png)

在此照片应用的示例设计中，照片应用在较大的屏幕上重新放置其内容。

![在较大的屏幕上重新放置内容的应用设计](images/rsp-design/rspd-reposition-type1.png)

### <a name="resize"></a>调整大小

可以通过调整 UI 元素的边距和大小来优化框架大小。 如以下示例所示，这可能使你只需通过增加内容框架即可改善在较大屏幕上的阅读体验。

![调整大小设计要素](images/rsp-design/rspd-resize.png)

### <a name="reflow"></a>重新排列

通过根据设备和方向更改 UI 元素的排列，你的应用可以以最佳方式呈现内容。 例如，在转到较大屏幕时，可能可以切换较大的容器、添加列，以及采用不同的方式生成列表项。

此示例显示如何在较大的屏幕上重新排列手机或平板手机上的单列垂直滚动内容，以显示两列文本。

![重新排列设计元素](images/rsp-design/rspd-reflow.png)

### <a name="showhide"></a>显示/隐藏

你可以基于屏幕空间显示或隐藏 UI 元素，或在设备支持附加功能、特定情况或首选屏幕方向时显示或隐藏 UI。

在此选项卡示例中，带相机图标的中间选项卡可能专用于手机或平板手机上的应用，却并不适用于较大型设备，这就是它显示在右侧设备中的原因。 显示或隐藏 UI 的另一个常见示例适用于媒体播放器控件：在较小型设备上，按钮集是折叠的，而在较大型设备上则是展开的。 例如，与手机上的媒体播放器相比，电脑上的媒体播放器可以处理更多屏幕上的功能。

![隐藏设计要素](images/rsp-design/rspd-revealhide.png)

显示或隐藏技术的一部分包括选择何时显示多个元数据。 当手机或平板手机等设备的实际使用空间达到最大值时，最好显示最少量的元数据。 而在笔记本电脑或台式机上，却可以显示大量元数据。 以下是如何处理显示或隐藏元数据的一些示例：

-   在电子邮件应用中，你可以显示用户的头像。
-   在音乐应用中，你可以显示有关专辑或歌手的详细信息。
-   在视频应用中，你可以显示有关电影或节目的详细信息，例如显示演职人员详细信息。
-   在任一应用中，都可以使各列分解并显示更多详细信息。
-   在任一应用中，都可以获取垂直堆叠的内容并使之以水平方式布局。 当从手机或平板手机转至较大型设备时，堆叠的列表项可以更改为显示多行列表项和多列元数据。

### <a name="replace"></a>替换

通过这种技术，你可以针对特定设备大小级别或方向来切换用户界面。 在此示例中，瞬态 UI（导航窗格及其精简版）适用于较小的设备，但在较大设备上，最好选择使用选项卡。

![替换设计元素](images/rsp-design/rspd-replace.png)

###  <a name="re-architect"></a>重新构建

可以折叠或拆分应用的体系结构，以更好地适应特定设备。 在此示例中，从左侧设备转到右侧设备将显示页面的接合。

![重新构建用户界面的示例](images/rsp-design/rspd-rearchitect.png)

以下是应用此技术以设计智能家居应用的示例。

![使用重新构建响应式设计技术的设计示例](images/rsp-design/rspd-rearchitect-type1.png)

## <a name="tools-and-design-toolkits"></a>工具和设计工具包

我们提供了各种工具来帮助你设计 UWP 应用。 有关 XD、Illustrator、Photoshop、Framer 和 Sketch 工具包以及其他设计工具和字体下载的信息，请参阅我们的[设计工具包页面](../design-downloads/index.md)。 

若要设置计算机以对 UWP 应用进行实际编码，请参阅[入门 &gt; 准备工作](../get-started/get-set-up.md)文章。 

## <a name="related-articles"></a>相关文章

- [UWP 应用是什么？](https://msdn.microsoft.com/library/windows/apps/dn726767.aspx)
- [设计工具包](../design-downloads/index.md)

 
