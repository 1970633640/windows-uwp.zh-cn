---
author: mijacobs
Description: "本文将介绍有关创建和显示应用设置的最佳做法。"
title: "应用设置指南"
ms.assetid: 2D765E90-3FA0-42F5-A5CB-BEDC14C3F60A
label: Guidelines
template: detail.hbs
translationtype: Human Translation
ms.sourcegitcommit: 59e02840c72d8bccda7e318197e4bf45ed667fa4
ms.openlocfilehash: aeccd755c5fe5df8f2ff5549950ce2d6cb74e8e4

---


# 应用设置指南





应用设置是应用的用户可自定义部分，并位于应用设置页面内。 例如，新闻阅读器应用中的应用设置可以让用户指定要显示的新闻源或屏幕上要显示的列数，而天气应用的设置则可以让用户在摄氏度和华氏度之间选择默认的测量单位。 本文将介绍有关创建和显示应用设置的最佳做法。

![设置窗格的示例](images/app-settings.png)

## <span id="Should_I_include_a_settings_page_in_my_app_"></span><span id="should_i_include_a_settings_page_in_my_app_"></span><span id="SHOULD_I_INCLUDE_A_SETTINGS_PAGE_IN_MY_APP_"></span>应用中应该包含设置页面吗？

以下是属于应用设置页面的应用选项的示例： 

-   影响应用的行为而且不需要频繁调整的配置选项，例如在天气应用中在摄氏度或华氏度之间选择默认的温度单位，更改邮件应用的帐户设置、通知设置或辅助选项。
-   依赖用户首选项的选项，例如音乐、音效或颜色主题。
-   不经常访问的应用信息，例如隐私策略、帮助、应用版本或版权信息。

包含在典型应用工作流中的命令（例如在艺术应用中更改画笔大小）不应该位于设置页面中。 若要了解有关命令放置的详细信息，请参阅[命令设计基础知识](https://msdn.microsoft.com/library/windows/apps/dn958433)。

## <span id="general_principles"></span><span id="GENERAL_PRINCIPLES"></span>常规建议


-   保持设置页面简洁，并使用二进制（开/关）控件。 通常，[切换开关](../controls-and-patterns/toggles.md)是二进制设置的最佳控件。
-   对于让用户从多达 5 个互相排斥的一组相关选项中选择一个项的设置，请使用[单选按钮](../controls-and-patterns/radio-button.md)。
-   在应用设置页面为所有应用设置创建入口点。
-   保持设置简单化。 定义智能默认值，并使设置数保持最少。
-   当用户更改设置时，应用应当立即反映所做的更改。
-   不要包括属于常见应用工作流的命令。

## <span id="Entry_point"></span><span id="entry_point"></span><span id="ENTRY_POINT"></span>入口点


用户进入应用设置页面的方式应取决于应用的布局。

**导航窗格**

对于导航窗格布局，应用设置应为导航选项列表中最后一项，并且应固定到底部：

![导航窗格的应用设置入口点](images/appsettings-entrypoint-navpane.png)

**应用栏**

如果你要使用应用栏或工具栏（通常是中心或表/透视表导航布局的一部分），请将入口点最后一项放置在“更多”弹出窗口菜单中。 如果应用将更能让人发现设置入口点视为很重要的一点，请将入口点直接放在应用栏上，而不是放在“更多”弹出窗口菜单中。

![应用栏的应用设置入口点](images/appsettings-entrypoint-tabs.png)

**中心**

如果你要使用中心布局，应用设置的入口点应放置在应用栏的“更多”弹出窗口菜单中。

**表/透视表**

对于表或透视表布局，我们不推荐将应用设置入口点作为顶部项之一放在导航中。 相反，应用设置的入口点应放置在应用栏的“更多”弹出窗口菜单中。

**大纲-细节**

与其将应用设置入口点深埋在大纲-细节窗格中，不如将其设置为高级大纲窗格上的最后一个固定项。

## <span id="Layout"></span><span id="layout"></span><span id="LAYOUT"></span>布局


在桌面版和移动版上，应用设置窗口都应该全屏填满整个窗口。 如果应用设置菜单拥有最多 4 个高级组，这些组应该叠在一列上。

桌面版：

![桌面版上应用设置页面的布局](images/appsettings-layout-navpane-desktop.png)

移动版：

![手机上应用设置页面的布局](images/appsettings-layout-navpane-mobile.png)

## <span id="_About__section_and__Give_feedback__button"></span><span id="_about__section_and__give_feedback__button"></span><span id="_ABOUT__SECTION_AND__GIVE_FEEDBACK__BUTTON"></span>“关于”部分和“提供反馈”按钮


如果你的应用需要“关于此应用”部分，请专门为之创建一个应用设置页面。 如果你需要“提供反馈”按钮，请将该按钮放置在“关于此应用”页面的底部。

“使用条款”和“隐私声明”应为带有环绕文本的[超链接按钮](../controls-and-patterns/hyperlinks.md)。

![附带“提供反馈”按钮的“关于此应用”部分](images/appsettings-about.png)

## <span id="dos_and_donts"></span><span id="DOS_AND_DONTS"></span>建议


## <span id="add_entry_points"></span><span id="ADD_ENTRY_POINTS"></span>应用设置页面内容


如果你有一个要包括在应用设置页面中的项目列表，请考虑以下指南：

-   将相似或相关的设置分到一个设置标签下。
-   尽力使设置总数保持在 4 个或 5 个以下。
-   无论应用的上下文如何，都显示相同的设置。 如果某些设置与特定的上下文不相关，则在应用设置浮出控件中禁用这些设置。
-   使用描述性的单个词标签来介绍设置。 例如，对于与帐户相关的设置，将该设置命名为“帐户”而非“帐户设置”。 如果希望设置只有一个选项并且设置不为其本身提供描述性标签，则请使用“选项”或“默认”。
-   如果设置直接链接到 Web 而非浮出控件，请使用可视化提示让用户知道这一情况，例如[超链接](../controls-and-patterns/hyperlinks.md)样式的“帮助（在线）”或“Web 论坛”。 请考虑将多个指向 Web 的链接分组到一个具有单个设置的浮出控件。 例如，“关于”设置可以打开具有指向“使用条款”、“隐私策略”和“应用支持”的链接的浮出控件。
-   将不太常用的设置组合到一个入口中，以便每个更常见的设置都有其各自的入口。 将仅包含信息的内容或链接放入“关于”设置。
-   不要复制“权限”窗格中的功能。 默认情况下，Windows 提供此窗格，你无法修改它。

## <span id="add_settings_to_flyouts"></span><span id="ADD_SETTINGS_TO_FLYOUTS"></span> 向“设置”浮出控件添加设置内容


-   在单个列中从上至下展示内容，支持滚动（如果需要）。 滚动限制的最大值是屏幕高度的两倍。
-   使用以下应用设置控件：

    -   [切换开关](../controls-and-patterns/toggles.md)：用于让用户将值设置为打开或关闭。
    -   [单选按钮](../controls-and-patterns/radio-button.md)：用于让用户从多达 5 个互相排斥的一组相关选项中选择一个项。
    -   [文本输入框](../controls-and-patterns/text-block.md)：用于让用户输入文本。 使用与要从用户那里获取的文本类型（如电子邮件或密码）相对应的文本输入框类型。
    -   [超链接](../controls-and-patterns/hyperlinks.md)：用于将用户带到应用中的其他页面或外部网站。 当用户单击超链接时，“设置”浮出控件将会消失。
    -   [按钮](../controls-and-patterns/buttons.md)：用于让用户立即启动操作，不会消除当前的“设置”浮出控件。
-   如果禁用其中一个控件，则添加描述性消息。 将此消息置于禁用的控件上。
-   在为“设置”浮出控件和标头设置动画后，将内容和控件作为单个块进行动画处理。 使用左偏移 100px 的 [**enterPage**](https://msdn.microsoft.com/library/windows/apps/br212672) 或 [**EntranceThemeTransition**](https://msdn.microsoft.com/library/windows/apps/br210288) 动画为内容创建动画。
-   使用部分标头、段落和标签来帮助组织和阐述内容（如果需要）。
-   如果你需要重复设置，请使用 UI 的其他级别或展开/折叠模式，但避免两级以上深度的层次结构。 例如，天气应用提供按城市设置（即，列出各个城市）并让用户在城市上点击以打开一个新浮出控件或展开以显示设置选项。
-   如果加载控件或 Web 内容需要花费时间，请使用不确定的进度控件以指示用户该信息正在加载。 有关详细信息，请参阅[进度控件指南](https://msdn.microsoft.com/library/windows/apps/hh465469)。
-   请勿使用导航按钮或提交更改按钮。 使用超链接导航到其他页面（而不是使用提交更改按钮）从而自动保存在用户取消“设置”浮出控件时对应用设置所做的更改。

\[此文章包含特定于通用 Windows 平台 (UWP) 应用和 Windows 10 的信息。 有关 Windows 8.1 指南，请下载 [Windows 8.1 指南 PDF](https://go.microsoft.com/fwlink/p/?linkid=258743)。\]

## <span id="related_topics"></span>相关主题

* [命令设计基础知识](https://msdn.microsoft.com/library/windows/apps/dn958433)
* [进度控件指南](https://msdn.microsoft.com/library/windows/apps/hh465469) 
           **对于开发人员 (XAML)**
* [存储和检索应用数据](https://msdn.microsoft.com/library/windows/apps/mt299098)
* [
            **EntranceThemeTransition**](https://msdn.microsoft.com/library/windows/apps/br210288)

�



<!--HONumber=Jun16_HO4-->


