---
author: mijacobs
Description: In a Universal Windows Platform (UWP) app, command elements are the interactive UI elements that enable the user to perform actions, such as sending an email, deleting an item, or submitting a form.
title: 通用 Windows 平台 (UWP) 应用的命令设计基础知识
ms.assetid: 1DB48285-07B7-4952-80EF-02B57D4469F2
label: Command design basics
template: detail.hbs
op-migration-status: ready
ms.author: mijacobs
ms.date: 10/01/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 0f5a994a76b66c04e8750315b6466471dc95b897
ms.sourcegitcommit: cbe7cf620622a5e4df7414f9e38dfecec1cfca99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "7429576"
---
# <a name="command-design-basics-for-uwp-apps"></a>UWP 应用的命令设计基础知识

在通用 Windows 平台 (UWP) 应用中，*命令元素*是使用户可以执行诸如发送一封电子邮件、 删除项或提交表单等操作的交互式 UI 元素。 *命令接口*组成常见命令元素、 承载它们的命令图面、 它们支持的交互以及它们提供的体验。

## <a name="provide-the-best-command-experience"></a>提供最佳的命令体验

命令界面的最重要方面是什么你尝试让用户完成。 规划你的应用的功能时，请考虑完成这些任务和你想要启用的用户体验所需的步骤。 一旦你已完成这些体验的初始草稿，然后做出的决策的工具和交互以实现它们。

下面是一些常见的应用程序体验：

- 发送或提交信息
- 选择设置和选项
- 搜索和筛选内容
- 打开、保存和删除文件
- 编辑或创建内容

通过使用命令体验的设计。 选择你的应用的输入设备支持，并且你的应用如何响应每台设备。 通过支持最广泛的功能和首选项为可用，移植，且可访问尽可能使你的应用。



<!--
When designing a command interface, the most important decision is choosing what a user can do. To plan the right type of interactions, focus on your app - consider the user experiences you want to enable, and what steps users will need to take. Once you decide what you want users to accomplish, then you can provide them the tools to do so.
-->

## <a name="choose-the-right-command-elements"></a>选择正确的命令元素

在命令界面中使用正确的元素可以使直观的易于使用应用和费解、 令人困惑的应用之间的区别。 在通用 Windows 平台 (UWP) 提供的全套命令元素。 下面是列出了一些最常见的 UWP 命令元素。

:::row:::
    :::column:::
        ![button image](images/commanding/thumbnail-button.svg)
    :::column-end:::
    :::column span="2":::
        <b>Buttons</b>

        <a href="../controls-and-patterns/buttons.md" style="text-decoration:none">Buttons</a> trigger an immediate action. Examples include sending an email, submitting form data, or confirming an action in a dialog.
:::row-end:::

:::row:::
    :::column:::
        ![list image](images/commanding/thumbnail-list.svg)
    :::column-end:::
    :::column span="2":::
        <b>Lists</b>

        <a href="../controls-and-patterns/lists.md" style="text-decoration:none">Lists</a> present items in a interactive list or a grid. Usually used for many options or display items. Examples include drop-down list, list box, list view and grid view.
:::row-end:::

:::row:::
    :::column:::
        ![selection control image](images/commanding/thumbnail-selection.svg)
    :::column-end:::
    :::column span="2":::
        <b>Selection controls</b>

        Lets users choose from a few options, such as when completing a survey or configuring app settings. Examples include <a href="../controls-and-patterns/checkbox.md">check box</a>, <a href="../controls-and-patterns/radio-button.md">radio button</a>, and <a href="../controls-and-patterns/toggles.md">toggle switch</a>.
:::row-end:::

:::row:::
    :::column:::
        ![Calendar  image](images/commanding/thumbnail-calendar.svg)
    :::column-end:::
    :::column span="2":::
        <b>Calendar, date and time pickers</b>

        <a href="../controls-and-patterns/date-and-time.md">Calendar, date and time pickers</a> enable users to view and modify date and time info, such as when creating an event or setting an alarm. Examples include calendar date picker, calendar view, date picker, time picker.
:::row-end:::

:::row:::
    :::column:::
        ![Predictive text entry image](images/commanding/thumbnail-autosuggest.svg)
    :::column-end:::
    :::column span="2":::
        <b>Predictive text entry</b>

        Provides suggestions as users type, such as when entering data or performing queries. Examples include <a href="../controls-and-patterns/auto-suggest-box.md">auto-suggest box</a>.<br>
:::row-end:::

有关完整列表，请参阅[控件和 UI 元素](../controls-and-patterns/index.md)

## <a name="place-commands-on-the-right-surface"></a>将命令放置在合适的图面上

在你的应用，包括应用画布或特殊命令容器，例如命令栏、 命令栏浮出控件、 菜单栏上或对话框中，可以将命令元素放置在各种图面上。

始终尝试让用户直接操作内容而不是通过命令作用于内容，如拖放以重新排列列表项而不是上移和下移命令按钮。 

但是，这可能不可能与某些输入设备，或适应特定用户能力和首选项。 在这些情况下，尽可能情况下，提供尽可能多的命令提示并将这些命令元素放置在应用中的命令图面上。

下面列出了一些最常见的命令图面。

:::row:::
    :::column:::
        ![app canvas image](images/commanding/thumbnail-canvas.svg)
    :::column-end:::
    :::column span="2":::
        <b>App canvas (content area)</b>

        If a command is constantly needed for users to complete core scenarios, put it on the canvas. Because you can put commands near (or on) the objects they affect, putting commands on the canvas makes them easy and obvious to use. However, choose the commands you put on the canvas carefully. Too many commands on the app canvas take up valuable screen space and can overwhelm the user. If the command won't be frequently used, consider putting it in another command surface.
:::row-end:::

:::row:::
    :::column:::
        ![commandbar image](images/commanding/thumbnail-commandbar.svg)
    :::column-end:::
    :::column span="2":::
        <b>Command bars and menu bars</b>

        <a href="../controls-and-patterns/app-bars.md">Command bars</a> help organize commands and make them easy to access. Command bars can be placed at the top of the screen, at the bottom of the screen, or at both the top and bottom of the screen (a <a href="../controls-and-patterns/menus.md#create-a-menu-bar">MenuBar</a> can also be used when the functionality in your app is too complex for a command bar).
:::row-end:::

:::row:::
    :::column:::
        ![context menu image](images/commanding/thumbnail-contextmenu.svg)
    :::column-end:::
    :::column span="2":::
        <b>Menus and context menus</b>

        <p>Menus and context menus save space by organizing commands and hiding them until the user needs them. Users typically access a menu or context menu by clicking a button or right-clicking a control.</p> 

        <p>The <a href="../controls-and-patterns/command-bar-flyout.md">command bar flyout </a> is a type of contextual menu that combines the benefits of a command bar and a context menu into a single control. It can provide shortcuts to commonly-used actions and provide access to secondary commands that are only relevant in certain contexts, such as clipboard or custom commands.</p>

        <p>UWP also provides a set of traditional menus and context menus; for more info, see the <a href="../controls-and-patterns/menus.md">menus and context menus overview</a>.</p>
:::row-end:::

## <a name="provide-command-feedback"></a>提供命令反馈 

命令反馈与用户通信，，检测到的交互或命令、 如何它已解释和处理，以及是否已成功或不。 这有助于用户了解他们做了，以及他们下一步可以做。 理想的情况下，应该在 UI 中自然地集成反馈，这样用户就不必被打断或采取额外行动（除非绝对有必要）。

> [!NOTE]
> 不提供反馈，除非绝对必要和反馈在其他地方不可用。 保持你的应用程序 UI 干净整洁除非你要添加的值。

下面是几种在应用中提供反馈的方法。

:::row:::
    :::column:::
        ![commandbar content area image](images/commanding/thumbnail-commandbar2.svg)
    :::column-end:::
    :::column span="2":::
        <b>Command bar</b>

        The content area of the <a href="../controls-and-patterns/app-bars.md">command bar</a> is an intuitive place to communicate status to users if they'd like to see feedback.
:::row-end:::

:::row:::
    :::column:::
        ![Flyout image](images/commanding/thumbnail-flyout.svg)
    :::column-end:::
    :::column span="2":::
        <b>Flyouts</b>

       <a href="../controls-and-patterns/dialogs-and-flyouts/index.md">浮出控件</a>是可以通过点击或单击浮出控件之外的某个位置来消除轻型上下文弹出窗口。
:::row-end:::

:::row:::
    :::column:::
        ![Dialog image](images/commanding/thumbnail-dialog.svg)
    :::column-end:::
    :::column span="2":::
        <b>Dialog controls</b>

        <a href="../controls-and-patterns/dialogs-and-flyouts/index.md">Dialog controls</a> are modal UI overlays that provide contextual app information. In most cases, dialogs block interactions with the app window until being explicitly dismissed, and often request some kind of action from the user. Dialogs can be disruptive and should only be used in certain situations. For more info, see the [When to confirm or undo actions](#when-to-confirm-or-undo-actions) section.
    :::column-end:::
:::row-end:::

> [!TIP]
> 请务必注意你的应用使用确认对话框的频率；当用户犯错时，这些对话框十分有用，但每当用户有意尝试执行某个操作时，这些对话框反而是障碍。

### <a name="when-to-confirm-or-undo-actions"></a>何时确认或撤消操作

无论如何设计你的应用程序 UI 精良，所有用户都执行某项操作后悔他们。 你的应用可帮助在这些情况下，通过要求确认某个操作，或通过提供撤消最近操作的方法。

:::row:::
    :::column:::
        ![do image](images/do.svg)

        For actions that can't be undone and have major consequences, we recommend using a confirmation dialog. Examples of such actions include:
        -   Overwriting a file
        -   Not saving a file before closing
        -   Confirming permanent deletion of a file or data
        -   Making a purchase (unless the user opts out of requiring a confirmation)
        -   Submitting a form, such as signing up for something
    :::column-end:::
    :::column:::
        ![do image](images/do.svg)

        For actions that can be undone, offering a simple undo command is usually enough. Examples of such actions include:
        -   Deleting a file
        -   Deleting an email (not permanently)
        -   Modifying content or editing text
        -   Renaming a file
:::row-end:::

##  <a name="optimize-for-specific-input-types"></a>针对特定输入类型进行优化

有关优化特定输入类型或设备的用户体验的详细信息，请参阅[交互入门](../input/index.md)。

