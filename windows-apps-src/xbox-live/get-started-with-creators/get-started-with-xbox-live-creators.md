---
title: Xbox Live 创意者计划入门
description: 提供了帮你开始使用 Xbox Live 创意者计划的链接。
ms.assetid: 2a744405-7ee4-42b4-8f36-9916e8c3a530
ms.date: 12/13/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: cce9d34679884d48475b7a7ae0fa8286204a6289
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57615872"
---
# <a name="get-started-with-the-xbox-live-creators-program"></a>Xbox Live 创意者计划入门
 
Xbox Live 创意者计划让你可以通过简化的认证流程将你的游戏快速地直接发布到 Xbox One 和 Windows 10，并且无需任何概念审批。 如果你的游戏集成了 Xbox Live 且遵循我们的[标准应用商店策略](https://msdn.microsoft.com/en-us/library/windows/apps/dn764944.aspx)，你已经可以发布了。 本文将概括介绍通过 Xbox Live 集成发布和运行游戏所需要的操作。 

Xbox Live 创意者计划游戏必须属于通用 Windows 平台 (UWP) 应用程序。 对于 Xbox One，请参阅 [Xbox One 上的 UWP](https://msdn.microsoft.com/en-us/windows/uwp/xbox-apps/index)，尤其是 [Xbox One 上 UWP 应用和游戏的系统资源](https://msdn.microsoft.com/en-us/windows/uwp/xbox-apps/system-resource-allocation)。 通过 Xbox Live 创意者计划发布的游戏没有访问成就或多人游戏联机服务的权限。 有关支持的服务的完整列表，请参阅[开发人员计划概述功能表](https://docs.microsoft.com/en-us/windows/uwp/xbox-live/developer-program-overview#feature-table)。

## <a name="1-ensure-you-have-a-title-created-in-partner-center"></a>1.确保已在合作伙伴中心中创建标题
必须在定义 Xbox Live 的每个标题[合作伙伴中心](https://partner.microsoft.com/dashboard)将能够登录，并进行 Xbox Live 服务调用之前。  [创建新的创意者主题作品](create-and-test-a-new-creators-title.md)将为你介绍如何执行此操作。

## <a name="2-follow-the-appropriate-guide-to-setup-your-ide-or-game-engine"></a>2.遵照相应的指南来设置您的 IDE 或游戏引擎
你可以遵循适用于自己平台和引擎的相应“入门指南”，并在过程中了解 Xbox Live 的基础知识：

* [开发使用 Visual Studio 的创建者标题](develop-creators-title-with-visual-studio.md)将向您演示如何使用合作伙伴中心中的 Xbox Live 配置将 Visual Studio 项目链接。
* [使用 Unity 开发创意者主题作品](develop-creators-title-with-unity.md)将为你介绍如何创建支持 Xbox Live 的新 Unity 游戏、处理单用户和多用户登录、添加排行榜和统计信息等功能，以及如何生成本机 Visual Studio 项目。

虽然 Unity 是仅为其我们提供了文档，游戏引擎的第三方游戏引擎[(2 & 3) 的构造](https://www.scirra.com/construct2)并[游戏 Maker Studio](https://www.yoyogames.com/gamemaker)还必须文档可帮助您集成 Xbox Live构造或游戏 Maker Studio 到游戏分别。

* [游戏 Maker Studio 2 UWP 现在支持 Xbox Live Creators 计划](https://www.yoyogames.com/gamemaker/xblc)将向您演示如何导出游戏 Maker Studio 项目都可以在 Xbox One 和 Windows 10 PC 上播放。
* [在 UWP 应用的构造中使用 Xbox Live](https://www.scirra.com/tutorials/9540/using-xbox-live-in-uwp-apps)显示如何使用 Xbox Live 在 Construct 2 和 3 场比赛中。

您仍可以为而无需有案可稽的 Xbox Live 集成其他游戏开发引擎，使用 Xbox Live Api 添加到你的标题的 Xbox Live。 要从你的项目使用 Xbox Live API，可以通过 NuGet 程序包添加对二进制文件的引用或者添加 API 源。 添加 NuGet 程序包可加快编译速度，而添加源可简化调试。

有关与第三方不是 Unity 的游戏引擎使用 Xbox Live 服务的支持，使用适当的游戏引擎人员解决问题。

## <a name="3-xbox-live-concepts--testing"></a>3.Xbox Live 的概念和测试
创建主题作品后，你应会了解一些将影响开发主题作品体验的 Xbox Live 概念。 此外，你还需要在游戏计划支持的所有平台上测试游戏，以确保游戏能够按预期运行。

- [Xbox Live Creators 计划的服务配置](xbox-live-service-configuration-creators.md)
- [Xbox Live 测试环境](../xbox-live-sandboxes.md)
- [为 Xbox Live 帐户授权](authorize-xbox-live-accounts.md)

## <a name="4-enable-xbox-live-sign-in"></a>4.实现 Xbox Live 的单一登录
所有 Xbox Live 创意者计划游戏都必须集成 Xbox Live 登录并显示用户身份（玩家代号、玩家头像等）。 你可以选择自动登录用户或允许用户利用按钮来启动登录进程。 登录后必须显示玩家代号，以便玩家验证使用的配置文件正确无误。

- [Xbox Live 社交平台的配置文件中，友元，存在](../social-platform/social-platform.md)

## <a name="5-add-optional-xbox-live-features"></a>5.添加可选的 Xbox Live 功能

Xbox Live 创意者计划提供了一系列功能，旨在帮助你推广游戏和吸引玩家：

- [Xbox Live 数据平台 - 统计信息、排行榜](../data-platform/data-platform.md)可通过让玩家竞相击败其好友并提高排名来提升你的游戏参与度。
- [Xbox Live 存储平台 - 连接存储、主题作品存储](../storage-platform/storage-platform.md)提供跨设备的免费游戏进度漫游，因此，玩家可以轻松地在 Xbox One 和 Windows 电脑之间延续游戏进度。
- [Xbox Live 社交平台 - 个人资料、好友、状态](../social-platform/social-platform.md)可让玩家与好友联系，还能讨论你的游戏。

请务必注意，Xbox Live 创意者计划不支持联机多人游戏、成就或玩家分数。

## <a name="6-release-your-game"></a>6.发布您的游戏

如果你使用的是 Xbox Live 创意者计划，则该过程与发布任何其他 UWP 应用程序的过程相同：

- [Microsoft Store 策略](https://msdn.microsoft.com/en-us/library/windows/apps/dn764944.aspx)包括[游戏和 Xbox 策略](https://msdn.microsoft.com/en-us/library/windows/apps/dn764944.aspx#pol_10_13)
- [发布 Windows 应用](https://developer.microsoft.com/en-us/store/publish-apps)