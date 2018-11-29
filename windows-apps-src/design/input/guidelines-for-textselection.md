---
Description: This topic describes the new Windows UI for selecting and manipulating text, images, and controls and provides user experience guidelines that should be considered when using these new selection and manipulation mechanisms in your UWP app.
title: 选择文本和图像
ms.assetid: d973ffd8-602e-47b5-ab0b-4b2a964ec53d
label: Selecting text and images
template: detail.hbs
keywords: 键盘, 文本, 输入, 用户交互
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 9679e6e658e7fa1eb50b41331e7e59ec2115fc14
ms.sourcegitcommit: 89ff8ff88ef58f4fe6d3b1368fe94f62e59118ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2018
ms.locfileid: "8199652"
---
# <a name="selecting-text-and-images"></a>选择文本和图像


本文介绍了选择和操作文本、图像和控件，并提供了将这些机制用于应用中时应考虑的用户体验指南。

> **重要 API**：[**Windows.UI.Xaml.Input**](https://msdn.microsoft.com/library/windows/apps/br227994)、[**Windows.UI.Input**](https://msdn.microsoft.com/library/windows/apps/br242084)
 


## <a name="dos-and-donts"></a>应做事项和禁止事项


-   在实现自己的控制手柄 UI 时使用字体字形。 控制手柄是系统范围内提供的两个 Segoe UI 字体的组合。 使用字体资源可以简化不同的 dpi 下的呈现问题，而且适用于各种 UI 缩放平台。 在实现自己的控制手柄时，应当共享下面的 UI 特征：

    -   圆形
    -   在任何背景下可见
    -   大小一致
-   在可选的内容周围提供一个边距以容纳控制手柄 UI。 如果你的应用允许在无法平移/滚动的区域中进行文本选择，请在文本区域的四个边缘都留出一定的边距，左边距和右边距要等于控制手柄边距的一半，上边距和下边距等于 1 个控制手柄高度，如下面的几幅图所示。 这可确保向用户公开整个控制手柄 UI，并尽可能减少与其他基于边缘的 UI 的意外交互。

    ![文本选择控制手柄边距](images/textselection-gripper-margins.png)

-   在交互期间隐藏控制手柄 UI 在交互期间消除由控制手柄带来的封闭。 当控制手柄未被手指完全遮盖或者有多个文本选择控制手柄时，这非常有用。 这可以消除在显示子窗口时的视觉假象。

-   不允许选择控件、标签、图像、专有内容等 UI 元素。 通常，Windows 应用程序仅允许在特定控件内进行选择。 诸如按钮、标签和徽标之类的控件不能选择。 评估选择是否是你应用的一个问题，如果是，请标识应该禁止选择的 UI 区域。 

## <a name="additional-usage-guidance"></a>其他使用指南


文本选择和操作对触摸交互引入的用户体验问题有特别影响。 鼠标、笔/笔触以及键盘输入高度细化：鼠标单击或笔/笔触触点通常映射到单个像素，某个键已按下或未按下。 触控输入并未细化；将指尖的整个表面映射到屏幕上某个特定的 x-y 位置以精确放置文本插入点比较困难。

**注意事项和建议**

使用通过提供完整平台用户交互体验，包括选择和操作行为的 Windowsto 生成应用中的语言框架公开的内置控件。 你会发现对于大多数 UWP 应用来说，内置控件的交互功能就已足够。

使用标准 UWP 文本控件时，本主题中所述的选择行为和视觉对象不能自定义。

**文本选择**

如果你的应用需要支持文本选择自定义 UI，我们建议你遵循此处所述的 Windowsselection 行为。

**可编辑的内容和不可编辑的内容**


借助触摸，选择交互主要是通过诸如用于设置插入光标或选择词汇的点击以及用于修改选择的滑动之类的手势来执行。 与其他 Windowstouch 交互，计时的交互仅限于点按操作和手势来显示信息 UI。 有关详细信息，请参阅[视觉反馈指南](guidelines-for-visualfeedback.md)。

Windowsrecognizes 两个可能选择交互，可编辑和不可编辑的状态，并相应调整选择 UI、 反馈以及功能。

**可编辑的内容**

在词汇的左半部分中点击会将光标放在紧挨词汇的左侧，在词汇的右半部分点击会将光标放在紧挨词汇的右侧。

以下图像演示了如何通过在词汇的开始或结尾附近点击来借助控制手柄放置初始插入光标。

![点击（或长按）词汇左侧可在该词汇的开始处放置插入点和控制手柄。 点击（或长按）词汇右侧可在该词汇的结尾处放置插入点和控制手柄。](images/textselection-place-caret.png)

以下图像演示了如何通过拖动控制手柄来调整选择。

![向任一方向拖动控制手柄可调整选择（第一个控制手柄保持固定，第二个控制手柄显示）。 拖动任一控制手柄可进行后续调整。](images/adjust-selection.png)

以下图像演示了如何通过在选择内或控制手柄上点击来调用上下文菜单（也可以使用长按）。

![在所选内容内或在控制手柄上点击（或长按）可调用上下文菜单。](images/textselection-show-context.png)

**注意**如果拼写错误的单词这些交互会稍。 点击标记为拼写错误的词汇将突出显示整个词汇，并且调用建议拼写上下文菜单。

 

**不可编辑的内容**

以下图像演示如何通过在词汇内点击来选择词汇（初始选择中不包含空格）。

![在词汇内点击可将其选中（初始选择中不包含空格）。](images/select-word.png)

按照与可编辑的文本相同的步骤来调整选择并显示上下文菜单。

**对象操作**

在 UWP 应用中实现自定义对象操作时，尽可能使用相同（或相似）的控制手柄来选择文本。 这有助于在平台内提供一致的交互体验。

例如，控制手柄还可以用在支持大小调整和修剪的图像处理应用中或者用在提供可调整进度栏的媒体播放应用中，如下面的几幅图所示。

![具有进度控制手柄的媒体播放器](images/gripper-mediaplayer.png)

*具有可调整进度栏的媒体播放器。*

![具有修剪控制手柄的图像](images/gripper-imagemanip.png)

*具有修剪控制手柄的图像编辑器。*

## <a name="related-articles"></a>相关文章



**对于开发人员**
* [自定义用户交互](https://msdn.microsoft.com/library/windows/apps/mt185599)

**示例**
* [基本输入示例](https://go.microsoft.com/fwlink/p/?LinkID=620302)
* [低延迟输入示例](https://go.microsoft.com/fwlink/p/?LinkID=620304)
* [用户交互模式示例](https://go.microsoft.com/fwlink/p/?LinkID=619894)
* [焦点视觉示例](https://go.microsoft.com/fwlink/p/?LinkID=619895)

**存档示例**
* [输入：XAML 用户输入事件示例](https://go.microsoft.com/fwlink/p/?linkid=226855)
* [输入：设备功能示例](https://go.microsoft.com/fwlink/p/?linkid=231530)
* [输入：触摸点击测试示例](https://go.microsoft.com/fwlink/p/?linkid=231590)
* [XAML 滚动、平移以及缩放示例](https://go.microsoft.com/fwlink/p/?linkid=251717)
* [输入：简化的墨迹示例](https://go.microsoft.com/fwlink/p/?linkid=246570)
* [输入：Windows 8 手势示例](https://go.microsoft.com/fwlink/p/?LinkId=264995)
* [输入：操作和手势 (C++) 示例](https://go.microsoft.com/fwlink/p/?linkid=231605)
* [DirectX 触控输入示例](https://go.microsoft.com/fwlink/p/?LinkID=231627)
 

 




