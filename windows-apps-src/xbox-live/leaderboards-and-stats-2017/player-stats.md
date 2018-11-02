---
title: 玩家统计数据
author: aablackm
description: 了解如何在 Xbox Live 中设置玩家统计数据。
ms.assetid: 5ec7cec6-4296-483d-960d-2f025af6896e
ms.author: aablackm
ms.date: 07/30/2018
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one, 玩家统计数据, 排行榜
ms.localizationpriority: medium
ms.openlocfilehash: 3cc6855a572a1636e92f3bcbf0a8e0d9a96a8bb4
ms.sourcegitcommit: 70ab58b88d248de2332096b20dbd6a4643d137a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2018
ms.locfileid: "5934510"
---
# <a name="player-stats"></a>玩家统计数据

如[数据平台概述](../data-platform/data-platform.md)中所述，统计数据是要跟踪的玩家相关信息的重要组成部分。 例如*爆头数*或*单圈最快时间*。 统计数据用于生成排行榜，在许多游戏的社区中将允许玩家比较他们的工作和与好友的技能和每个其他玩家的方案。 配置的统计信息显示在游戏的[游戏中心](../data-platform/designing-xbox-live-experiences.md)排行榜，玩家将看到他们如何针对其好友还玩游戏的排名。 在游戏的游戏中心中显示的统计数据被称为**功能统计数据**，又称为**主要统计信息**。除了游戏中心中显示，从 Xbox One 1806 更新起特别推荐的统计数据可能还会定期出现在用户可能会添加到其主视图的固定内容块。 这允许快速访问有关的社交排行榜直接从主页视图。 请务必记住，特别推荐的统计数据是显示在固定内容块中，，所以用户可能不始终只能看到他们如果 Microsoft 内容服务确定内容的另一项可能更有吸引力的几个可能的项之一。

## <a name="stats-2013-and-2017"></a>统计数据 2017年和 2013

当前有两个实现 Xbox Live、 Stats 2013 和 Stats 2017 统计数据。 这两者都是提供给ID@Xbox和托管合作伙伴开发。 Xbox Live 创意者计划开发人员可能仅使用 Stats 2017，并因此可以忽略 Stats 2013。

Xbox Live 创意者计划开发人员可以跳到[Stats 2017 文档](stats2017.md)。

这些两个实现从根本上讲是不同的原则上运行。 当使用 Stats 2013 包含用户执行某项操作某些信息向 Xbox Live 服务发送**事件**。 这些**事件**中的信息用于相应地更新统计数据。 统计数据 2013年中该服务将跟踪并更新所有统计数据值，使其玩家或一组玩家的统计信息值的真实的源。 为了便于对比，Stats 2017 中将发送的实际的统计数据值本身的要使用的服务器。 统计数据 2017 年 10 月服务器会少为的值不验证发送给它，因此它是由你的作品，并跟踪的正确的统计数据值的统计信息值的资料来源。 我们建议你跟踪，并且如果你决定实现 Stats 2017 与[Xbox Live 存储平台](../storage-platform/storage-platform.md)在云中存储你的统计数据。 你可以将 Stats 2017 视为报告服务。 为你的游戏的正确的统计数据发送到服务器，统计数据将然后坐在服务器上，并等待显示请求或更新。

## <a name="a-brief-history"></a>简短历史记录

启动的 Xbox One，Xbox Live 引入了新的事件驱动的统计数据模型中，玩家 Stats 2013。 这提供了大量的好处 – 从游戏通过单个事件即可更新多个 Xbox Live 功能，如排行榜和成就; 数据Xbox Live 配置依赖于服务器而不是在客户端;以及更多内容。 在 Xbox One 发布以来年中，我们密切听取了游戏开发人员的反馈，开发人员一致地请求和会允许它们在绕过的复杂性附带事件驱动的系统，以及允许的更简化的统计数据服务它们用于跟踪的方法已对其进行练习任何统计数据。 具体取决于开发人员的反馈创建新的简化的版本的统计数据将使统计数据逻辑的控件返回到开发人员的手。 系统是 Stats 2017，只需采用值服务通过游戏使开发人员能够控制的逻辑如何确定统计信息值传递给它。

## <a name="how-stats-are-handled-in-2013-and-2017"></a>统计数据 2017年 2013年中的处理方式

让我们来看看配置和 2013年和 2017年更新统计数据。 让我们假设我们将从一些通用 rpg 进行统计数据，并且想要跟踪的危险终止。

统计数据 2013年中你的游戏如何发送*事件*，其中包含有关玩家执行的操作的信息。 此事件中玩家具有配备双刃剑时，将 slaying 操作 orc。 此事件中包含的信息的一些可能，拍摄 slay 操作、 件事 slayed 已 orc，一组的类型为 melee，且使用武器为双刃剑。 Stats 2013 将运行此信息通过多个配置的开发人员，在[Xbox 开发人员门户 (XDP)](https://xdp.xboxlive.com/User/Contact/MyAccess?selectedMenu=devaccounts)或[Windows 开发人员中心](https://developer.microsoft.com/en-us/windows)，并更新统计数据，还配置由你，具体取决于该事件的规则。 统计数据 2013年中该服务将跟踪的 slaying 的统计信息值应该是什么。 与双刃剑事件 slay orc 无法更新多个统计信息，如、 击杀数、 orcs slain，数和双刃剑击杀数。

统计数据 2017 年 3 月，你将发送的实际值设置为你的统计信息。 双刃剑示例 slay orc，为你的游戏将跟踪的总击杀、 双刃剑技能和 orcs 分别 slain 数，并且发送该服务的每项统计数据更新的数量。 服务有最小验证检查，以确保你正在发送大量有意义，所以绝对由你的游戏发送正确的统计数据。 尽管你可以使用 Stats 2017 服务的游戏会话开始时取消统计数据的值，你不应使用 Stats 2017 服务以确认正在运行该会话时的统计数据的值。

下面，你可以看到图示的两种类型的统计数据的工作方式。
![统计数据的区别图示](../images/stats/Stats2013-7DiagramColored.jpg)

## <a name="a-few-more-notes"></a>一些详细说明

对于ID@Xbox和托管的合作伙伴开发人员有几个你时应注意的 Stats 2013 和 Stats 2017 之间进行选择为你的游戏的多个区别。

Stats 2013 允许多个排行榜视图。
Stats 2013 允许你更轻松地深入了解你的统计信息的元数据。 在我们 orc 杀死整体统计数据是跟踪的击杀数的示例。 Stats 2013 允许你深入了解到内容已终止与什么武器以及定义的信息可能需要配置的任何其他终止的统计信息。

Stats 2013 具有本机分钟播放统计数据，Stats 2013 中允许访问玩家的游戏时间在游戏中，而无需配置统计信息。 任何玩的统计信息必须通过统计数据 2017 年你的作品来跟踪。

Stats 2013 具有近的实时更新频率。
Stats 2013 事件系统几乎立即更新统计数据。 在 Stats 2017 没有更新统计数据刷新到该服务前五分钟的等待时间。 开发人员可以手动刷新统计数据，但仍将在最小值为 30 秒之间刷新被节流。

Stats 2013 可以支持其他 Xbox Live 服务。
使用 Stats 2013 可用于统计数据解锁成就，并作出匹配决策。 Stats 2017 仅用于生成排行榜。

## <a name="further-reading"></a>进一步阅读

有关 Stats 2013 的详细说明你可以读取[Stats 2013 上的合作伙伴仅文档](https://developer.microsoft.com/en-us/games/xbox/docs/xboxlive/xbox-live-partners/event-driven-data-platform/user-stats)。
有关 Stats 2017 的更深入地说明读取[统计数据 2017年文档](stats2017.md)。