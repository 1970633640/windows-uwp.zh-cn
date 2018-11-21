---
author: mijacobs
Description: TODO
title: 游戏板和遥控器交互
ms.assetid: 784a08dc-2736-4bd3-bea0-08da16b1bd47
label: Gamepad and remote interactions
template: detail.hbs
isNew: true
ms.author: mijacobs
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: a3e87fea7dfce66b16ccdf04ef13950c092660c8
ms.sourcegitcommit: cbe7cf620622a5e4df7414f9e38dfecec1cfca99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "7426502"
---
# <a name="gamepad-and-remote-control-interactions"></a>游戏板和遥控器交互

![遥控器和方向键](images/dpad-remote/dpad-remote.png)

通用 Windows 平台 (UWP) 应用现在支持游戏板和遥控器（Xbox 和电视体验的主要输入设备）输入。

UWP 应用应针对这些输入设备类型进行优化，就像针对电脑上的键盘和鼠标以及手机或平板电脑上的触摸输入进行优化一样。

确保应用适用于这些输入设备是针对 Xbox 和电视进行优化时的重要步骤。

> [!NOTE] 
> 现在可以为电脑上的 UWP 应用插入并使用游戏板，这使验证工作变得轻松。

若要使你的 UWP 应用在使用游戏板或遥控器时提供成功且愉快的用户体验，你应考虑以下事项：

* [硬件按钮](../devices/designing-for-tv.md#hardware-buttons) - 手柄和遥控器提供截然不同的按钮和配置。

* [XY 焦点导航和交互](../devices/designing-for-tv.md#xy-focus-navigation-and-interaction) - XY 焦点导航使用户可以在应用 UI 中四处导航。

* [鼠标模式](../devices/designing-for-tv.md#mouse-mode) - 当 XY 焦点导航有所不足时，鼠标模式可使你的应用模拟鼠标体验。
