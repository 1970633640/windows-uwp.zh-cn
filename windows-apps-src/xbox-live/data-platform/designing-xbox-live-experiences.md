---
title: 设计 Xbox Live 体验
author: KevinAsgari
description: 了解如何通过为游戏规划玩家统计信息、排行榜和成就来为 Xbox Live 成员设计出色的体验。
ms.assetid: d2a85621-7d02-4b11-a7fa-9ebaee0092d5
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one, 统计信息, 成就, 排行榜, 设计
ms.localizationpriority: medium
ms.openlocfilehash: 112beacc2009f495da64475a0740560b7271b43d
ms.sourcegitcommit: 5dda01da4702cbc49c799c750efe0e430b699502
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/21/2018
ms.locfileid: "4111264"
---
# <a name="designing-xbox-live-experiences"></a>设计 Xbox Live 体验

本主题将指导你完成使用 Xbox Live 的数据平台功能，思考并向你的游戏添加用户统计信息、成就和排行榜的示例过程。

## <a name="example"></a>示例
让我们配置一个虚构游戏，通过它来向你显示数据平台如何帮助你在 Xbox One 仪表板、Windows 10 上的 Xbox 应用，以及你的游戏中展现令人惊叹的 Xbox Live 体验。 对于此场景，我们将处理名为 _Races 2015_ 的虚构赛车游戏。

为了获得这些体验的最大价值，我们将遵循以下建议的规划阶段：
1. 设计 XBL 体验
2. 设计支持你的场景所需的统计信息
3. 根据需要配置“特别推荐的统计信息”、“成就”或“排行榜”


## <a name="1-design-your-xbox-live-experiences"></a>1. 设计 Xbox Live 体验
我们希望 _Race 2015_ 充分利用 Xbox Live，以保持用户在游戏内部和外部的参与度。 要提出的第一个问题是：

1. 我们希望游戏中心的“成就”选项卡体验是什么样的？ （特别推荐的统计信息和社交排行榜）
2. 我们希望在游戏中向玩家提供哪些要实现的目标和动机？ （成就）
3. 我们希望玩家在游戏中使用哪些分数或统计信息来确定自己在好友中的排名？ （排行榜）


### <a name="gamehubs---featured-statistics-and-social-leaderboards"></a>游戏中心 - 特别推荐的统计信息和社交排行榜
游戏中心是登录体验，用户可以在这里了解有关游戏的一切。 作为开发人员和/或发布者，这是你向尚未购买你游戏的 Xbox 用户_展现_该游戏如何出色且丰富的绝佳位置。 游戏中心还被设计为向已经拥有游戏的玩家显示进度和有吸引力指标。 在“成就”选项卡下，用户可以找到“游戏进度和成就”、“主要统计信息”和“社交排行榜”。

此部分的目标是为游戏捕获最有吸引力的指标，并呈现这些指标以提供游戏玩家体验的独特画面，同时在社交排行榜中确定玩家在好友中的排名。 例如，Forza 6 的“成就”选项卡可能像下面这样：

![游戏中心图像](../images/omega/forza_gamehub.png)


你将注意到，有些统计信息（如“行驶英里数”和“夺冠次数”）有金、银或铜装饰，用来说明玩家在好友中的排名。 与这些统计信息中的任何信息交互都会显示完整的排行榜，如下所示：

![排行榜](../images/omega/progress_gamehub_lb.png)

 对于 _Race 2015_，我们相信以下是一组能够表示游戏的玩家体验的不错的统计信息，以及合适的排名指标：
 * 单圈最快时间
 * 夺冠次数
 * 行驶英里数


### <a name="achievements"></a>成就
成就是一个系统范围的机制，能够在所有游戏中通过一致的方式引导和奖励用户在游戏内的操作。 正确设计此体验将帮助指导用户最充分地体验游戏，并延长游戏的寿命。

对于 _Races 2015_，下面是我们想要配置的一部分成就：
* 单圈完成时间在 60 秒以下
* 以第一名的成绩完成 10 场比赛
* 每个赛道至少完成 1 场比赛
* 拥有 5 辆汽车
* 行驶 10,000 英里
* ...


###  <a name="leaderboards"></a>排行榜
排行榜使玩家能够，针对他们在游戏中完成的特定操作，将自己与其他玩家进行比较。 除了游戏中心中的社交排行榜，我们还可以配置在游戏中使用的全球排行榜。 以下是一些我们将需要在其中为所有用户排名的排行榜：

* 单圈最快时间
 * 元数据：跟踪此情况发生的位置
 * 元数据：使用的汽车
 * 元数据：天气状况
* 夺冠次数
* 收集的汽车最多

## <a name="next-steps"></a>后续步骤
既然你已经了解了如何有效地设计“统计信息”、“排行榜”和“成就”，现在你便可以开始在你的作品中实现这些体验了。  接下来的几个部分将介绍从开发人员中心内的配置开始的端到端过程。

请参阅[玩家统计信息](../leaderboards-and-stats-2017/player-stats.md)
