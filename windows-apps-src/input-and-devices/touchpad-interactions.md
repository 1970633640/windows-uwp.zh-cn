---
创建具有直观且独特用户交互体验的通用 Windows 平台 (UWP) 应用，它们针对触摸板进行了优化，但在不同的输入设备上功能一致。
触摸板交互
ms.assetid: CEDEA30A-FE94-4553-A7FB-6C1FA44F06AB
触摸板交互
template: detail.hbs
---

# 触摸板设计指南


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 的文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

设计你的应用，以便用户可以通过触摸板与其交互。 触摸板将间接式多点触控输入和定位设备（如鼠标）的精确输入结合起来。 这种结合使触摸板既适用于触摸优化的 UI，也适用于效率应用的较小目标。

 

![触摸板](images/input-patterns/input-touchpad.jpg)


触摸板交互需要满足以下三项：

-   标准触摸板或 Windows 精确式触摸板。

    精确式触摸板针对通用 Windows 平台 (UWP) 设备进行了优化。 它们支持系统在本机处理触摸板体验的某些方面（例如手指跟踪和手掌检测），从而在不同设备之间实现更一致的体验。

-   一个或多个手指直接接触触摸板。
-   触摸接触时移动（或不移动，具体取决于时间阈值）。

触摸传感器提供的输入数据可以实现以下目的：

-   解释为直接操作一个或多个 UI 元素的物理手势（例如平移、旋转、调整大小或移动）。 相比之下，通过某个元素属性窗口或其他对话框与该元素交互被认为是间接操作。
-   作为另一种输入方法识别，例如鼠标或笔。
-   用于补充或修改其他输入方法的方面，例如涂抹用笔绘制的笔划墨迹。

触摸板将间接多点触控输入与指针设备（如鼠标）的精确输入结合。 这种组合使触摸板既适用于触摸优化的 UI，也适用于效率应用和桌面环境通常较小的目标。 针对触摸输入优化 Window 应用商店应用设计，并在默认情况下获得触摸板支持。

由于触摸板支持聚合的交互体验，所以除了触摸输入的内置支持，我们还建议使用 [**PointerEntered**](https://msdn.microsoft.com/library/windows/apps/br208968) 事件来提供鼠标样式的 UI 命令。 例如，使用“上一页”和“下一页”按钮，使用户既可以翻阅网页内容，也可以通过平移浏览内容。

本主题中讨论的手势和指南可以帮助确保你的应用使用最少的代码无缝支持触摸板输入。

## <span id="The_touchpad_language"> </span> <span id="the_touchpad_language"> </span> <span id="THE_TOUCHPAD_LANGUAGE"> </span>触摸板语言


一组在整个系统中通用的简单触摸板交互功能。 针对触摸和鼠标输入优化应用，这种语言可以使用户快速熟悉应用，提升他们的信心，使其更容易了解和使用应用。

用户可以设置远比标准触摸板更多的精确式触摸板手势和交互行为。 这两张图分别显示了不同于标准触摸板和精确触摸板的“设置”>“设备”>“鼠标”>“触摸板”的触摸板设置页面。

![标准触摸板设置](images/mouse-touchpad-settings-standard.png)

<sup>标准\\ 触摸板\\ 设置</sup>

![Windows 精确式触摸板设置](images/mouse-touchpad-settings-ptp.png)

<sup>Windows\\ 精确式\\ 触摸板\\ 设置</sup>

下面是一些用于执行常见任务的触摸板优化手势的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Three-finger_tap"></span><span id="three-finger_tap"></span><span id="THREE-FINGER_TAP"></span>三指点击</p></td>
<td align="left"><p>使用 <strong>Cortana</strong> 搜索或显示<strong>“操作中心”</strong>的用户首选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Three_finger_slide"></span><span id="three_finger_slide"></span><span id="THREE_FINGER_SLIDE"></span>三指滑动</p></td>
<td align="left"><p>打开虚拟桌面任务视图、显示桌面、或切换已打开应用的用户首选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Single_finger_tap_for_primary_action"></span><span id="single_finger_tap_for_primary_action"></span><span id="SINGLE_FINGER_TAP_FOR_PRIMARY_ACTION"></span>单个手指点击进行主操作</p></td>
<td align="left"><p>使用单个手指点击某个元素并调用它的主操作（如启动应用或执行命令）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Two_finger_tap_to_right-click"></span><span id="two_finger_tap_to_right-click"></span><span id="TWO_FINGER_TAP_TO_RIGHT-CLICK"></span>二指点击进行右键单击</p></td>
<td align="left"><p>两个手指同时在某个元素上点击可以将其选中并显示上下文命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Two_finger_slide_to_pan"></span><span id="two_finger_slide_to_pan"></span><span id="TWO_FINGER_SLIDE_TO_PAN"></span>二指滑动进行平移</p></td>
<td align="left"><p>滑动主要用于平移交互，但也可用于移动、绘制或书写。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Pinch_and_stretch_to_zoom"></span><span id="pinch_and_stretch_to_zoom"></span><span id="PINCH_AND_STRETCH_TO_ZOOM"></span>收缩和拉伸以缩放</p></td>
<td align="left"><p>收缩和拉伸手势通常用于调整大小和语义式缩放。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Single_finger_press_and_slide_to_rearrange"></span><span id="single_finger_press_and_slide_to_rearrange"></span><span id="SINGLE_FINGER_PRESS_AND_SLIDE_TO_REARRANGE"></span>单指按下并滑动以重新排列</p></td>
<td align="left"><p>拖动元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Single_finger_press_and_slide_to_select_text"></span><span id="single_finger_press_and_slide_to_select_text"></span><span id="SINGLE_FINGER_PRESS_AND_SLIDE_TO_SELECT_TEXT"></span>单指按下并滑动以选择文本</p></td>
<td align="left"><p>在可选择的文本内按下并滑动来选择它。 双击可选择一个字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Left_and_right_click_zone"></span><span id="left_and_right_click_zone"></span><span id="LEFT_AND_RIGHT_CLICK_ZONE"></span>单击和右键单击区域</p></td>
<td align="left"><p>模拟鼠标设备的左键和右键功能。</p></td>
</tr>
</tbody>
</table>

 

## <span id="Hardware"> </span> <span id="hardware"> </span> <span id="HARDWARE"> </span>硬件


查询鼠标设备功能 ([**MouseCapabilities**](https://msdn.microsoft.com/library/windows/apps/br225626)) 以确定触摸板硬件可以直接访问你的应用 UI 的哪些方面。 我们建议提供适用于触摸和鼠标输入的 UI。

有关查询设备功能的详细信息，请参阅[标识输入设备](identify-input-devices.md)。

## <span id="Visual_feedback"> </span> <span id="visual_feedback"> </span> <span id="VISUAL_FEEDBACK"> </span>视觉反馈


-   当（通过移动或悬停事件）检测到触摸板光标时，显示特定于鼠标的 UI 以指示元素显示的功能。 如果触摸板光标在一定的时间段内没有移动，或者如果用户启动了触摸交互，则让触摸板 UI 逐渐淡出。 这会使 UI 干净整洁。
-   不要使用鼠标获取悬停反馈，由元素提供的反馈就足够（请参阅下面的[光标](#Cursors)）。
-   如果元素不支持交互（如静态文本），不要显示视觉反馈。
-   不要将焦点矩形与触摸板交互结合使用。 保留焦点矩形是为了进行键盘交互。
-   对于所有代表相同输入目标的元素，同时显示视觉反馈。

有关视觉反馈的更常规的指南，请参阅[视觉反馈指南](https://msdn.microsoft.com/library/windows/apps/hh465342)。

## <span id="Cursors"> </span> <span id="cursors"> </span> <span id="CURSORS"> </span>光标


为触摸板指针提供了一组标准光标。 它们用来表示元素的主要操作。

每个标准光标都有一个与它相关联的默认图像。 用户或应用可以随时替换与任何标准光标相关联的默认图像。 Windows 应用商店应用通过 [**PointerCursor**](https://msdn.microsoft.com/library/windows/apps/br208273) 函数指定光标图像。

如果你需要自定义鼠标光标：

-   对于可单击元素，始终使用箭头光标（![箭头光标](images/cursor-arrow.png)）。 对于链接或其他交互元素，不使用指向手光标（![指向手光标](images/cursor-pointinghand.png)）。 而应使用悬停效果（上文中有介绍）。
-   对于可选择文本，使用文本光标（![文本光标](images/cursor-text.png)）。
-   当主要操作是移动（如拖动或裁剪）时，使用移动光标（![移动光标](images/cursor-move.png)）。 对于主要操作是导航的元素（如“开始”菜单磁贴），不使用移动光标。
-   当对象的大小可调整时，使用水平、垂直和对角调整大小光标（![垂直调整光标](images/cursor-vertical.png)， ![水平调整光标](images/cursor-horizontal.png)， ![对角调整光标（左下和右上）](images/cursor-diagonal2.png)， ![对角调整光标（左上和右下）](images/cursor-diagonal1.png)）。
-   当在固定画布（如地图）内平移内容时，使用手掌型光标（![手掌型光标（张开）](images/cursor-pan1.png)， ![手掌型光标（闭合）](images/cursor-pan2.png)）。

## <span id="related_topics"> </span>相关文章


* [处理指针输入](handle-pointer-input.md)
* [标识输入设备](identify-input-devices.md)
**示例**
* [基本输入示例](http://go.microsoft.com/fwlink/p/?LinkID=620302)
* [低延迟输入示例](http://go.microsoft.com/fwlink/p/?LinkID=620304)
* [用户交互模式示例](http://go.microsoft.com/fwlink/p/?LinkID=619894)
* [焦点视觉示例](http://go.microsoft.com/fwlink/p/?LinkID=619895)
**存档示例**
* [输入：设备功能示例](http://go.microsoft.com/fwlink/p/?linkid=231530)
* [输入：XAML 用户输入事件示例](http://go.microsoft.com/fwlink/p/?linkid=226855)
* [XAML 滚动、平移以及缩放示例](http://go.microsoft.com/fwlink/p/?linkid=251717)
* [输入：使用 GestureRecognizer 的笔势和操作](http://go.microsoft.com/fwlink/p/?LinkID=231605)
 





<!--HONumber=Mar16_HO1-->


