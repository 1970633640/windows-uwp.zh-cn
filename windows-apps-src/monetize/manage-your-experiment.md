---
author: Xansky
Description: After you define your experiment in Partner Center and code your experiment in your app, you are ready to active your experiment and use Partner Center to review the results of your experiment.
title: 合作伙伴中心中管理实验
ms.assetid: D48EE0B4-47F2-455C-8FB9-630769AC5ACE
ms.author: mhopkins
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, uwp, Microsoft Store Services SDK, A/B 测试, 实验
ms.localizationpriority: medium
ms.openlocfilehash: 9d1cdb80a2278850f18cecc631fef0b5dff0fefc
ms.sourcegitcommit: 38f06f1714334273d865935d9afb80efffe97a17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "6203782"
---
# <a name="manage-your-experiment-in-partner-center"></a>合作伙伴中心中管理实验

你[定义你在合作伙伴中心中的实验](define-your-experiment-in-the-dev-center-dashboard.md)，并[为实验编写应用代码](code-your-experiment-in-your-app.md)之后, 你已准备好激活实验，并使用合作伙伴中心查看实验结果。 在获取所需的全部数据后，可以结束你的实验，然后选择是继续使用你的所有应用的控件变体中的变量值还是切换到使用其他变体之一中的变量值。

> [!NOTE]
> 当激活某个实验时，合作伙伴中心会立即开始从进行检测以数据为你的实验记录的任何应用中收集数据。 但是，可能需要几个小时实验数据，以显示在合作伙伴中心。

有关演示如何创建并运行实验的端到端过程的演练，请参阅[通过 A/B 测试来创建并运行你的第一个实验](create-and-run-your-first-experiment-with-a-b-testing.md)。

## <a name="activate-your-experiment"></a>激活实验

当你在合作伙伴中心中的实验的参数满意，并且你已更新你的应用代码时，你可以随时激活实验，以便你可以开始从你的应用中收集实验数据。 激活实验后，你的应用可以检索变体值，并向合作伙伴中心报告视图和转换事件。

1. 登录到[合作伙伴中心](https://partner.microsoft.com/dashboard)。
2. 在 **“你的应用”** 下，通过要激活的实验选择该应用。
3. 在导航窗格中，选择**服务**，然后选择**实验**。
4. 在**项目**部分的项目表中，展开包含你的实验的项目，然后执行以下操作之一：
  * 为你的实验单击**激活**链接。 你的实验已添加到页面顶部附近的**活动实验**部分。
  * 单击实验名称、滚动到实验页面底部，然后单击**激活**。

> [!IMPORTANT]
> 激活实验后，不可再对实验参数进行修改，除非在创建实验时，选中了**可编辑实验**复选框。 在激活实验之前，我们建议你在应用中为实验编码。

## <a name="review-the-results-of-your-experiment"></a>查看实验结果

1. 在合作伙伴中心中，返回到你的应用的**实验**页面。
2. 在**活动实验**部分中，单击活动实验的名称以转到实验页面。
3. 有关活动实验或已完成的实验，此页中的前两个部分提供了实验的结果：
  * **“结果摘要”** 部分列出了实验目标和每个变体的转换率百分比。
  * **“结果详细信息”** 部分为实验中的所有目标的每个变体提供了更多详细信息，包括视图、转换、独特用户、转换率、增量百分比、置信度和重要性。 *置信度*是用来计算错误边距的估计的可靠性统计度量。 *重要性*是基于示例大小的统计度量，用来确定结果不是偶然得出，而是由于特定原因。

> [!NOTE]
> 合作伙伴中心仅报告第一个转换事件的每个用户在 24 小时时间段内。 如果用户在 24 小时时段内在应用中触发多个转换事件，仅报告第一个转换事件。 这是为了帮助防止具有很多转换事件的单个用户扭曲一组用户示例得出的实验结果。


## <a name="complete-your-experiment"></a>完成实验

1. 在合作伙伴中心中，返回到实验页面。 有关说明，请参阅上一节。
2. 在**结果摘要**部分中，执行以下操作之一：
  * 如果想要结束实验并继续使用应用的控件变体中的变量值，请单击**继续**。
  * 如果想要结束实验但切换到使用应用的不同变体中的变量值，请在要对其进行切换的变体下单击**切换**。
3. 单击**确定**确认你想要结束该实验。


## <a name="related-topics"></a>相关主题

* [创建项目并定义远程变量在合作伙伴中心](create-a-project-and-define-remote-variables-in-the-dev-center-dashboard.md)
* [为实验编写应用代码](code-your-experiment-in-your-app.md)
* [在合作伙伴中心中定义实验](define-your-experiment-in-the-dev-center-dashboard.md)
* [通过 A/B 测试创建和运行你的第一个实验](create-and-run-your-first-experiment-with-a-b-testing.md)
* [通过 A/B 测试运行应用实验](run-app-experiments-with-a-b-testing.md)
