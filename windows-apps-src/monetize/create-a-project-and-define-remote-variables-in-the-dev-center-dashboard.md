---
author: Xansky
Description: Before you can run an experiment in your Universal Windows Platform (UWP) app with A/B testing, you must create a project and define your remote variables in Partner Center.
title: 在合作伙伴中心中创建实验项目
ms.assetid: C3809FF1-0A6A-4715-B989-BE9D0E8C9013
ms.author: mhopkins
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, uwp, Microsoft Store Services SDK, A/B 测试, 实验
ms.localizationpriority: medium
ms.openlocfilehash: 19a59110fa094aeae3d40dca1372fde9889c108e
ms.sourcegitcommit: 4d88adfaf544a3dab05f4660e2f59bbe60311c00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "6467805"
---
# <a name="create-an-experiment-project-in-partner-center"></a>在合作伙伴中心中创建实验项目

若要开始实验，在合作伙伴中心中创建实验[项目](run-app-experiments-with-a-b-testing.md#terms)为你的应用，并定义你的应用可以访问的远程变量。

以下说明介绍了用于创建项目的核心步骤。 有关演示如何创建项目、然后运行实验的端到端过程的详细演练，请参阅[通过 A/B 测试来创建并运行你的第一个实验](create-and-run-your-first-experiment-with-a-b-testing.md)。

## <a name="instructions"></a>说明

1. 登录到[合作伙伴中心](https://partner.microsoft.com/dashboard)。
2. 在 **“你的应用”** 下，选择你想为之创建实验的应用。
3. 在导航窗格中，选择**服务**，然后选择**实验**。
4. 在**实验**页面上，单击**项目**部分中的**新建项目**按钮。 如果你已经创建了一个或多个项目，这些项目会在**项目**部分中列出。
5. 在**新建项目**页面中，输入新项目的名称。
6. 在**远程变量**部分中，添加你希望用于此项目中所有实验的[变量](run-app-experiments-with-a-b-testing.md#terms)，并为每个变量定义默认值。 此处指定的默认值将用于实验的控件组，也将用于没有参与此实验的任何用户。
  1. 如果**远程变量**部分已折叠，请单击本部分标题上的**显示**。
  2. 单击**添加变量**创建每个你希望用于此项目中任何实验的新变量，并键入变量的变量名称和默认值。
  3. 添加变量完成后，请单击**保存**。
3. 在 **SDK 集成**部分中，记下[项目 ID](run-app-experiments-with-a-b-testing.md#terms)值。 当你[为实验编写应用代码](code-your-experiment-in-your-app.md)，你必须引用此项目 ID 在代码中以便可以接收变体数据并将视图和转换事件报告给合作伙伴中心。

> [!NOTE]
> 在项目中的实验处于活动状态时，不可编辑、添加或删除远程变量。 此限制有助于保护活动实验的控件组的数据完整性。


## <a name="next-steps"></a>后续步骤

创建项目后，可以[为实验编写应用代码](code-your-experiment-in-your-app.md)以开始检索应用中的变量值，并且可以[在项目中创建实验](define-your-experiment-in-the-dev-center-dashboard.md)。

## <a name="related-topics"></a>相关主题

* [为实验编写应用代码](code-your-experiment-in-your-app.md)
* [在合作伙伴中心中定义实验](define-your-experiment-in-the-dev-center-dashboard.md)
* [合作伙伴中心中管理实验](manage-your-experiment.md)
* [通过 A/B 测试创建和运行你的第一个实验](create-and-run-your-first-experiment-with-a-b-testing.md)
* [通过 A/B 测试运行应用实验](run-app-experiments-with-a-b-testing.md)
