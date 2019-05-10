---
Description: 精心设计的有针对性的动作可以使应用变得栩栩如生，并且使体验感觉精良和完美。 帮助用户理解上下文更改，将体验与视觉转换紧密相连。
title: UWP 应用中的动作和动画
ms.assetid: 21AA1335-765E-433A-85D8-560B340AE966
label: Motion
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: stmoy
design-contact: jeffarn
doc-status: Published
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 249251afeee95d80070e6df80980a2fbc5be7f06
ms.sourcegitcommit: 09edf480f2224e29e190fad8518f680c16e21c6d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065246"
---
# <a name="motion-for-uwp-apps"></a>适用于 UWP 应用的动作

![“移动”图标](../images/motion-2x.png)

Fluent 动作在应用中有其用途。 它基于用户行为提供智能反馈、让 UI 感觉保持生动，并指导用户在你的应用中导航。 Fluent 动作在用户和其数字体验之间引起情感连接。 我们建立了用户已从物理世界中了解的自然运动的基础，并在这个基础上扩展我们的系统。

## <a name="fluent-motion-principles"></a>Fluent 动作原则

### <a name="physical"></a>物理

动作中的对象展现现实世界中的对象行为。 流畅、敏捷的运动可以打造自然的体验，从而建立起情感连接、增加个性化。

![物理动作的 UI 示例](images/Physical.gif)
> 在通过触控与 UI 交互时，UI 的移动与交互速度直接相关。 因为触控是直接操作，你与之交互的对象将影响其周围的对象。

### <a name="functional"></a>功能

动作有其用途，并且具有可信性。 它指导用户了解复杂情况，并帮助建立层次结构。 移动为展示带来增强的效果，并通过隐藏感知延迟优化用户体验。

![功能动作的 UI 示例](images/functional.gif)
> 页面过渡是专门构建的。 它们提供有关页面如何彼此相关的提示。 它们以被视为快速的方式移动，即使在效果不佳的情况。

### <a name="continuous"></a>连续的

点到点的流畅运动自然地绘制眼睛并指导用户操作。 它巧妙地将用户任务拼接起来，使其感觉更可用、更友好。

![连续动作的 UI 示例](images/continuous3.gif)
> 对象在场景与场景之间移动或在场景内变形以提供连续性，并帮助用户保持上下文。

### <a name="contextual"></a>上下文

智能动作以与用户操作 UI 相同的方式向用户提供反馈。 交互以用户为中心。 运动效果适合外形规格并围绕场景设计。 它应该让每个用户都感觉舒适。

![上下文动作的 UI 示例](images/Contextual.gif)
> 动画应绑定到用户交互。 上下文菜单从用户激活它的点部署。 

## <a name="motion-articles"></a>动作文章

:::row:::
    :::column:::
        ### [Timing and easing](timing-and-easing.md)
        Timing and easing are important elements that make motion feel natural for objects entering, exiting, or moving within the UI.
    :::column-end:::
    :::column:::
        ### [Directionality and gravity](directionality-and-gravity.md)
        Directional signals help provide a solid mental model of the journey a user takes across experiences. Directional movement is subject to forces like gravity, which reinforces the natural feel of the movement.
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        ### [Page transitions](page-transitions.md)
        Page transitions navigate users between pages in an app, providing feedback about the relationship between pages. They help users understand where they are in the navigation hierarchy.
    :::column-end:::
    :::column:::
        ### [Connected animation](connected-animation.md)
        Connected animations let you create a dynamic and compelling navigation experience by animating the transition of an element between two different views.
    :::column-end:::
:::row-end:::
