---
author: mijacobs
Description: How to create app icons/logos that represent your app in the Start menu, app tiles, the taskbar, the Microsoft Store, and more.
title: 应用图标和徽标
template: detail.hbs
ms.author: mijacobs
ms.date: 04/17/2018
ms.topic: article
keywords: windows 10, uwp
design-contact: Judysa
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 6c389aa207b0756a222c1c82ea99ea007b451b1e
ms.sourcegitcommit: e814a13978f33654d8e995584f4b047cb53e0aef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "6030657"
---
# <a name="app-icons-and-logos"></a>应用图标和徽标 

每个应用有表示它，图标/徽标，并且该图标显示在 Windows shell 中的多个位置中： 

:::row:::
    :::column:::
        * 你的应用窗口标题栏
        * 开始菜单中的应用列表
        * 在任务栏和任务管理器
        * 你的应用磁贴
        * 你的应用的初始屏幕
        * 在 Microsoft Store 中
    :::column-end:::
    :::column:::
        ![windows 10 start and tiles](images/assetguidance01.jpg)
    :::column-end:::
:::row-end:::

本文介绍了创建应用图标的基础知识如何使用 Visual Studio 管理它们，以及如何手动管理它们应需要。
 
（本文是专门用于表示应用本身; 有关常规图标指南，请参阅[图标](icons.md)文章的图标。）

## <a name="icon-types-locations-and-scale-factors"></a>图标类型、 位置和比例系数

默认情况下，Visual Studio 资产子目录中存储图标资源。 下面是的图标显示位置和它们的调用不同类型的列表。 

| 图标名称 | 显示在 | 资产文件名称 |
| ---      | ---        | --- |
| 小磁贴 | “开始”菜单 |  SmallTile.png  |
| 中等磁贴 |开始菜单中，Microsoft Store listing\ *  |  Square150x150Logo.png |
| 宽磁贴  | “开始”菜单   | Wide310x150Logo.png |
| 大磁贴   | 开始菜单中，Microsoft Store listing\ * |  LargeTile.png  |
| 应用图标 | 在开始菜单、 任务栏、 任务管理器的应用列表 | Square44x44Logo.png |
| 初始屏幕 | 应用的初始屏幕 | 是 SplashScreen.png  |
| 锁屏提醒徽标 | 你的应用磁贴 | BadgeLogo.png  |
| 程序包徽标/应用商店徽标 | 应用安装程序，开发人员中心，应用商店的应用商店中的"写评论"选项中的"报告应用程序"选项 | StoreLogo.png  |

\ * 使用，除非你选择[仅显示上传的应用商店中的图像](/windows/uwp/publish/app-screenshots-and-images#display-only-uploaded-logo-images-in-the-store)。 

若要确保这些图标看起来锐每个屏幕上，你可以创建多个版本的不同的显示比例系数的同一个图标。 

比例系数确定文本等 UI 元素的大小。 缩放系数介于 100%和 400%。 较大的值创建较大的 UI 元素，使其更易于查看高 DPI 显示器上。 

:::row:::
    :::column:::
        Windows automatically sets the scale factor for each display based on its DPI (dots-per-inch) and the viewing distance of the device. 

        (Users can override the default value by going to the **Settings &gt; Display &gt; Scale and layout** page.)
    :::column-end:::
    :::column:::
        ![](images/icons/display-settings-screen.png)
    :::column-end:::
:::row-end:::  


由于应用图标资源是位图，位图不会也随比例，我们建议为每个比例系数提供一个版本每个图标资源： 100%、 125%、 150%、 200%和 400%。 有很多图标的 ！ Fortunatly，Visual Studio 提供了一种工具，便于生成和更新这些图标。 

## <a name="microsoft-store-listing-image"></a>Microsoft Store 一览图像

"如何指定为我的应用一览图像在 Microsoft Store 中？"

默认情况下，我们使用某些你的程序包的图像在应用商店中 （以及其他[你在提交过程中提供的图像](https://docs.microsoft.com/en-us/windows/uwp/publish/app-screenshots-and-images)） 此页面顶部表中所述。 但是，你可以选择防止应用商店向 Windows 10 （包括 Xbox） 上的客户显示你的一览时，你的应用包中使用的徽标图像，并改为具有应用商店使用你上传的图像。 这为你提供更好地控制你的应用的外观的整个应用商店的各种显示中。 （请注意，是否你的产品支持较早的操作系统版本，这些客户可能仍会看到图像从你的程序包，即使你使用此选项。）你可以在提交过程的**应用商店一览**步骤的**应用商店徽标**部分中执行此操作。

![在应用提交过程中指定应用商店徽标](images/app-icons/storelogodisplay.png)

选中此框，出现了名为**应用商店显示图像**的新部分。 在这里，你可以上传应用商店将使用你的应用包中的徽标图像代替的 3 个图像大小： 300 x 300、 150 x 150 和 71 x 71 像素。 尽管我们建议提供所有 3 大小，是必需的仅为 300 x 300 大小。

有关详细信息，请参阅[仅显示上传的应用商店中的徽标图像](/windows/uwp/publish/app-screenshots-and-images#display-only-uploaded-logo-images-in-the-store)。

<!-- ### Fallback images for the Store

The simplest way to control the Store listing image is to specify it during the app submission process. If you don't provide these images during the app submission process, the Store will use a tile image:

1. Large tile
2. Medium tile

If these images aren't provided, the Store will search all matching images of the same image type with a square aspect ratio, preferable with a height greated than the scaled requested height (scaled height is the machine's resolution scale factor * display height). If none of the images meet this criteria, the Store will ignore the scale factor and select an image based on height.  -->

<!-- You can provide screenshots, logos, and other art assets (such as trailers and promotional images to include in your app's Microsoft Store listing. Some of these are required, and some are optional (although some of the optional images are important to include for the best Store display).

The Store may also use your app's tile and other images that you include in your app's package. 

For more information, see [App screenshots, images, and trailers in the Microsoft Store](/windows/uwp/publish/app-screenshots-and-images). -->


## <a name="managing-app-icons-with-the-visual-studio-manifest-designer"></a>使用 Visual Studio 清单设计器的管理应用图标

Visual Studio 提供了用于管理你的应用图标调用**清单设计器**的非常有用的工具。 

> 如果你尚未获得 Visual Studio 2017，有很多个版本可用，包括免费版，（Visual Studio 2017 社区版），和其他版本提供免费试用版。 你可以在此处下载它们：[https://developer.microsoft.com/windows/downloads](https://developer.microsoft.com/windows/downloads)


若要启动清单设计器：
<!-- 1. Use Visual Studio to open a UWP project.
2. In the **Solution Explorer**, double-click the package.appmanifest file. 

    ![The Visual Studio 2017 Solution Explorer](images/icons/vs-solution-explorer.png)

    Visual Studio displays the manifest designer.

    ![The Visual Studio 2017 manifest designer](images/icons/vs-manfiest-designer.png)
3. Click the **Visual Assets** tab.

    ![The Visual Assets tab](images/icons/vs-manfiest-designer-visual-assets.png) -->


:::row:::
    :::column:::
        1. 使用 Visual Studio 中打开 UWP 项目。
    :::column-end:::
    :::column:::
        
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        2. 在**解决方案资源管理器**中，双击 Package.appmxanifest 文件。
    :::column-end:::
    :::column:::
        ![The Visual Studio 2017 Manifest Designer](images/icons/vs-solution-explorer.png)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
            Visual Studio displays the Manifest Designer.
    :::column-end:::
    :::column:::
            ![The Visual Assets tab](images/icons/vs-manfiest-designer.png)
    :::column-end:::
:::row-end:::    
:::row:::
    :::column:::
        3. 单击**视觉资源**选项卡。
    :::column-end:::
    :::column:::
        ![The Visual Assets tab](images/icons/vs-manfiest-designer-visual-assets.png)
    :::column-end:::
:::row-end:::        

## <a name="generating-all-assets-at-once"></a>在一次生成所有资源

在**视觉资源**选项卡，**所有视觉资源**，第一个菜单项未完全什么其名称的建议： 生成你的应用需要按某个按钮与每个视觉资产。

![在 Visual Studio 中生成所有视觉资源](images/app-icons/all-visual-assets.png)

你需要做是提供单个图像，并 Visual Studio 将生成小磁贴、 中等磁贴、 大磁贴、 宽磁贴、 大磁贴、 应用图标、 初始屏幕，并为每个比例系数的徽标资产包。

若要在一次生成所有资源：
1. 单击**源**字段旁边 **...** 并选择你想要使用的图像。 如果你使用位图图像，确保它至少 400 400 个像素，以便你获得清晰的结果。 基于矢量的图像适合;Visual Studio 可让你可以使用 AI (Adobe Illustrator) 和 PDF 文件。 
2. （可选）。在**显示设置**部分中，配置以下选项：

    a.  **短名称**： 指定你的应用的短名称。

    b.  **显示名称**： 指示是否要在中等、 宽或调大磁贴上显示的短名称。 

    c. **磁贴背景**： 指定十六进制值或磁贴背景颜色的颜色名称。 例如，`#464646`。 默认值为 `transparent`。

    d. **Spash 屏幕背景**： 指定 spash 屏幕背景的十六进制值或颜色名称。 

3. 单击**生成**。 

Visual Studio 生成你的图像文件，并将其添加到项目。 如果你想要更改你的资源，只需重复此过程。 

缩放的图标资源遵循此文件命名约定：

*文件名*的缩放*比例系数*.png

例如，

Square150x150Logo-比例-100.png、 Square150x150Logo-比例-200.png、 Square150x150Logo-比例-400.png

请注意，Visual Studio 不会生成锁屏提醒徽标，默认情况下。 这是因为锁屏提醒徽标是唯一的并且可能不应匹配你的其他应用图标。 有关详细信息，请参阅[为 UWP 应用项目的锁屏提醒通知](/windows/uwp/design/shell/tiles-and-notifications/badges)。 


## <a name="more-about-app-icon-assets"></a>有关应用图标资源的详细信息
Visual Studio 将生成你的项目，所需的所有应用图标资源，但如果你想要自定义它们，这有助于了解如何在不同于其他应用资源。 

应用图标资源出现在大量的位置： Windows 任务栏、 任务视图、 ALT + TAB、 和开始菜单磁贴的右下角。 在很多地方显示应用图标资源，因为它具有一些额外的大小调整和 plating 的选项没有其他资源:"目标大小"资产和"更新"的资源。 

### <a name="target-size-app-icon-assets"></a>目标大小应用图标资源
除了标准的比例系数大小 ("Square44x44Logo.scale-400.png")，我们还建议创建的"目标大小"资源。 我们将这些资产目标大小，因为它们面向特定的大小，如 16 个像素，而不是特定的比例系数，如 400。 请勿使用缩放停滞系统的曲面的目标大小资源如下：

* “开始”菜单跳转列表（桌面）
* 磁贴下角的“开始”菜单（桌面）
* 快捷方式（桌面）
* 控制面板（桌面）

下面是目标大小的资源的列表：


| 资源大小 | 文件名示例                  |
|------------|------------------------------------|
| 16x16\*    | Square44x44Logo.targetsize-16.png  |
| 24x24\*    | Square44x44Logo.targetsize-24.png  |
| 32x32\*    | Square44x44Logo.targetsize-32.png  |
| 48x48\*    | Square44x44Logo.targetsize-48.png  |
| 256x256\*  | Square44x44Logo.targetsize-256.png |
| 20x20      | Square44x44Logo.targetsize-20.png  |
| 30x30      | Square44x44Logo.targetsize-30.png  |
| 36x36      | Square44x44Logo.targetsize-36.png  |
| 40x40      | Square44x44Logo.targetsize-40.png  |
| 60x60      | Square44x44Logo.targetsize-60.png  |
| 64x64      | Square44x44Logo.targetsize-64.png  |
| 72x72      | Square44x44Logo.targetsize-72.png  |
| 80x80      | Square44x44Logo.targetsize-80.png  |
| 96x96      | Square44x44Logo.targetsize-96.png  |

\ * 至少，我们建议提供这些大小。 

无需向这些资源添加填充；Windows 会根据需要添加填充。 这些资源应占据最少 16 pixel 的占用空间。 

以下是这些资源在 Windows 任务栏上的图标中显示时的示例：

![Windows 任务栏中的资源](images/assetguidance21.png)

### <a name="unplated-assets"></a>未着色的资源
默认情况下，Windows 默认情况下使用彩色背板顶部的基于目标的资源。 如果需要，你可以提供基于目标的未着色的资源。 "更新"，则意味着资产将显示透明背景。 请记住，这些资产将显示在不同的背景色。 

![未着色和着色资源](images/assetguidance22.png)

下面是使用未着色的应用图标资源的图面：
* 任务栏和任务栏缩略图（桌面）
* 任务栏跳转列表
* 任务视图
* ALT+TAB


### <a name="target-and-unplated-sizing"></a>目标和未着色的大小调整

下面是基于目标的资源，以 100%缩放的大小建议：

![基于目标的资源大小调整（比例为 100%）](images/assetguidance23.png)


## <a name="more-about-splash-screen-assets"></a>有关初始屏幕资源的详细信息
有关初始屏幕的详细信息，请参阅[UWP 的初始屏幕文章](/windows/uwp/launch-resume/splash-screens)。

## <a name="more-about-badge-logo-assets"></a>有关锁屏提醒徽标资源的详细信息

你使用的资源生成器生成所需的所有资产，时为什么它不会都生成锁屏提醒徽标默认情况下的原因： 它们明显不同于其他应用资源。 锁屏提醒徽标是显示在通知和应用的磁贴上的状态图像。 

有关详细信息，请参阅[为 UWP 应用项目的锁屏提醒通知](/windows/uwp/design/shell/tiles-and-notifications/badges)。


## <a name="customizing-asset-padding"></a>自定义的资源填充

默认情况下，Visual Studio 资产生成器到任何映像应用推荐的填充。 如果你的映像已经包含填充或者你想要扩展到磁贴的结尾的全出血图像，你可以关闭此功能通过取消选中**应用推荐的填充**复选框。 

### <a name="tile-padding-recommendations"></a>磁贴填充建议
如果你想要提供你自己的填充，下面是我们建议为磁贴。 

有 4 个磁贴大小： 小 (71 x 71)、 中等 (150 x 150)、 范围 (310 x 150) 和大 (310 x 310)。 

每个磁贴资源的大小与在其上放置的磁贴大小相同。

![显示全出血的磁贴](images/app-icons/tile-assets1.png)

如果你不希望你用来扩展到边缘的磁贴的图标，你可以使用在你的资产透明像素创建填充。 

![磁贴和背板](images/assetguidance05.png)

对于小磁贴，将图标宽度和高度限制为磁贴大小的 66%：

![小磁贴大小调整比率](images/assetguidance09.png)

对于中磁贴，将图标宽度限制为磁贴大小的 66%，将高度限制为 50%。 这可以防止品牌栏中的元素重叠：

![中磁贴大小调整比率](images/assetguidance10.png)

对于宽磁贴，将图标宽度限制为磁贴大小的 66%，将高度限制为 50%。 这可以防止品牌栏中的元素重叠：

![宽磁贴大小调整比率](images/assetguidance11.png)

对于大磁贴，将图标宽度限制为磁贴大小的 66%，将高度限制为 50%：

![大磁贴大小比率](images/assetguidance12.png)

某些图标专用于水平或垂直方向，而其他图标具有更复杂形状，使它们无法完全拟合目标尺寸。 居中显示的图标可向一侧加权。 在此情况下，如果图标占据的视觉权重与完全拟合的图标相同，则该图标的一部分可能悬挂在建议的占用之外：

![三个居中的图标](images/assetguidance13.png)

使用全出血资源，将在磁贴的边距和边缘内相交的元素考虑在内。 保留的边距至少占据 16% 的磁贴高度或宽度。 此百分比表示最小磁贴大小的边距宽度的两倍：

![带有边距的全出血磁贴](images/assetguidance14.png)

在此示例中，边距太紧：

![带有过紧边距的全出血磁贴](images/assetguidance15.png)









