---
author: mtoepke
title: "使用 DirectX 创建简单的通用 Windows 平台 (UWP) 游戏"
description: "在本套教程中，你将了解如何使用 DirectX 和 C++ 创建基本的通用 Windows 平台 (UWP) 游戏。"
ms.assetid: 9edc5868-38cf-58cc-1fb3-8fb85a7ab2c9
keywords:
- "DirectX 游戏示例"
- "游戏示例, 通用 Windows 平台 (UWP)"
- "Direct3D 11 游戏"
ms.author: mtoepke
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: 3ffce29c3ad7088dd24b848cb159b85a4db158e3
ms.lasthandoff: 02/07/2017

---

# <a name="create-a-simple-universal-windows-platform-uwp-game-with-directx"></a>使用 DirectX 创建简单的通用 Windows 平台 (UWP) 游戏


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

在此教程集中，你将了解如何使用 DirectX 和 C++ 创建基本的通用 Windows 平台 (UWP) 游戏。 我们将介绍游戏的所有主要部分，包括加载资源（如艺术和网格）、创建主游戏循环、实现简单的呈现管道以及添加声音和控件的过程。

我们将向你介绍 UWP 游戏开发技巧和注意事项。 我们不提供完整的端到端游戏。 而重点介绍关键的 UWP DirectX 游戏开发概念， 并围绕这些概念阐述特定于 Windows 运行时的注意事项。

## <a name="objective"></a>目标


-   使用 UWP DirectX 游戏的基本概念和组件，更熟练地使用 DirectX 设计 UWP 游戏。

## <a name="what-you-need-to-know-before-starting"></a>开始之前需要了解的内容


在开始本教程之前，你需要熟悉这些主题。

-   Microsoft C++ 组件扩展 (C++/CX)。 这是对 Microsoft C++ 的更新，它合并了自动引用计数，并且是用于使用 DirectX 11.1 或 更高版本开发 UWP 游戏的语言。
-   基本线性代数和牛顿物理学概念。
-   基本图形编程术语。
-   基本的 Windows 编程概念。
-   基本熟悉 [Direct2D](https://msdn.microsoft.com/library/windows/apps/dd370990.aspx) 和 [Direct3D 11](https://msdn.microsoft.com/library/windows/desktop/hh404569) API。

##  <a name="the-windows-store-direct3d-shooting-game-sample"></a>Windows 应用商店 Direct3D 射击游戏示例


此示例实现一个简单的第一人称射击库，游戏内容是玩家射击移动目标上的球。 击中每个目标就奖给一组点数，玩家可以晋级 6 个难度不断增加的级别。 在级别末尾，将记录点数，并且玩家可以赢得最终得分。

该示例演示以下游戏概念：

-   DirectX 11.1 与 Windows 运行时之间的互操作。
-   第一人称 3D 视角和相机
-   立体 3D 效果
-   3D 中对象之间的冲突检测
-   处理玩家从鼠标、触摸和 Xbox 360 控制器控件的输入
-   音频混合和播放
-   基本游戏状态机

![正在操作的游戏示例](images/simple3dgame-display.png)


| 主题 | 说明 |
|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [设置游戏项目](tutorial--setting-up-the-games-infrastructure.md) | 装配游戏的第一步是在 Microsoft Visual Studio 中设置项目，以便让基础架构正常工作所需的代码量减至最小。 通过使用正确的模板和专门为游戏开发配置项目，可以节省大量的时间和减少不必要的麻烦。 我们将指导你完成设置和配置简单游戏项目的步骤。 |
| [定义游戏的 UWP 应用框架](tutorial--building-the-games-metro-style-app-framework.md) | 为 UWP DirectX 游戏进行编码的第一部分是生成使游戏对象与 Windows 交互的框架。 这包括 Windows 运行时属性，如暂停/恢复事件处理、窗口焦点和贴靠，以及用户界面的事件、交互和过渡。 我们将了解该示例游戏的构建方式，以及它如何为玩家与系统交互定义高级状态机。 |
| [定义主游戏对象](tutorial--defining-the-main-game-loop.md) | 现在，我们将了解游戏示例主对象的详细信息，以及如何将其实现的规则转换为与游戏世界的交互。 |
| [装配呈现框架](tutorial--assembling-the-rendering-pipeline.md) | 现在，我们开始讨论示例游戏如何使用该结构和状态显示其图形。 下面我们通过演示屏幕的图形对象介绍如何实现呈现框架，从图形设备的初始化开始。 |
| [添加用户界面](tutorial--adding-a-user-interface.md) | 你已经了解示例游戏如何实现主游戏对象和基本呈现框架。 现在介绍示例游戏如何向玩家提供有关游戏状态的反馈。 你可在此处了解如何在 3D 图形管道输出上添加简单的菜单选项和提醒显示组件。 |
| [添加控件](tutorial--adding-controls.md) | 现在，我们了解该游戏示例如何在 3D 游戏中实现移动观看控件，以及如何开发基本的触摸、鼠标和游戏控制器控件。 |
| [添加声音](tutorial--adding-sound.md) | 在此步骤中，我们将探讨射击游戏示例如何使用 [XAudio2](https://msdn.microsoft.com/library/windows/desktop/ee415813) API 创建声音播放对象。 |
| [扩展游戏示例](tutorial-resources.md) | 恭喜你！ 此时，你理解了基本 UWP DirectX 3D 游戏的关键组件。 你可以设置游戏的框架，包括视图提供程序和呈现管道，并实现基本的游戏循环。 还可以创建基本的用户界面覆盖层以及合并声音和控件。 你正在创建一个专属游戏，下面是一些可使你进一步了解 DirectX 游戏开发的资源。 |
 

 

 





