---
Description: 可以使用合作伙伴中心以运行试验针对通用 Windows 平台 (UWP) 应用的 A / B 测试。
title: 通过 A/B 测试运行应用实验
ms.assetid: 790B4B37-C72D-4CEA-97AF-D226B2216DCC
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, uwp, Microsoft Store Services SDK, A/B 测试, 实验
ms.localizationpriority: medium
ms.openlocfilehash: d4f5271d70cefea99a9caff04e7203e05043440c
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57599772"
---
# <a name="run-app-experiments-with-ab-testing"></a>通过 A/B 测试运行应用实验

可以使用合作伙伴中心以定义远程变量可在运行时检索从通用 Windows 平台 (UWP) 应用程序，并可以使用你的用户以确定驾驶所需的用户行为的最有效值测试这些值的变体。 应用可以使用远程变量配置应用体验，例如应用内购买、注册流程、描述文字和广告发布。

A/B 测试的目标应该是标识远程变量值的变体，该变体可能会通过提供更具吸引力的应用体验提高转换率（例如更多应用内购买）。 确定成功的变体后，你可以立即结束试验，而无需重新发布您的应用程序启用供整个用户受众从合作伙伴中心，该变体。

## <a name="create-and-run-an-ab-test"></a>创建并运行 A/B 测试

若要创建并运行 A/B 测试，请执行以下步骤：

1. [创建项目并在合作伙伴中心定义远程变量](create-a-project-and-define-remote-variables-in-the-dev-center-dashboard.md)。 此项目包含你的实验的变量和默认变量值。  
2. [针对实验为你的应用编码](code-your-experiment-in-your-app.md)。 使用 Microsoft Store Services SDK 中 API 从在合作伙伴中心创建的项目中获取远程变量值、 使用此数据来修改测试时，该功能的行为和查看事件和转换事件发送到合作伙伴中心。
3. [在合作伙伴中心定义试验](define-your-experiment-in-the-dev-center-dashboard.md)。 在你的项目中创建一个可定义你的 A/B 测试的唯一目标和变体的测试。
4. [运行和管理在试验中合作伙伴中心 ashboard](manage-your-experiment.md)。 激活实验，并使用合作伙伴中心查看试验的结果，然后完成该实验。

有关演示端到端过程的演练，请参阅[通过 A/B 测试创建并运行你的第一个实验](create-and-run-your-first-experiment-with-a-b-testing.md)。

## <a name="requirements"></a>要求

A / B 测试在合作伙伴中心仅支持 UWP 应用。

在可以通过 A/B 测试运行实验之前，必须设置你的开发计算机：

* 按照[此处](../get-started/get-set-up.md)的说明为 UWP 开发设置你的开发计算机。
* [安装 Microsoft Store Services SDK](microsoft-store-services-sdk.md#install-the-sdk)。 除了实验的 API，此 SDK 还提供了其他功能（例如，可在应用上显示广告并引导你的客户到“反馈中心”收集反馈）的 API。

## <a name="best-practices"></a>最佳做法

对于最有用的结果，我们建议在通过 A/B 测试运行实验时遵循以下建议：

* 考虑通过变体分配的随机对半拆分分配的两个变体运行实验。
* 运行实验至少需要 2 – 4 周才能收集统计上重要且可操作的有效数据。

<span id="terms" />

## <a name="related-terms"></a>相关术语

|  术语  |  定义  |
|--------|--------------|
| 项目    |   你的应用可使用 Microsoft Store Services SDK 访问的远程变量及默认值的集合。 项目也可以选择包含一个或多个可共享相同远程变量的实验。  |
| Experiment 开头的所有检查点    |   可定义用户将接收的 A/B 测试的一组参数。 实验在项目的作用域中定义，并且每个实验包含以下内容： <p></p><ul><li>指示了用户开始查看属于实验的变体时的*视图事件*。</li><li>指示了到达目标时*转换事件*的一个或多个目标。</li><li>定义了实验使用的变量数据的一个或多个*变体*。 *控件*变体使用在实验的项目中定义的默认变量值。 除了控件变体，实验通常具有至少一个其他变体（含特定于该实验的默认值）。 </li></ul>          |
| 项目 ID    |   将您的应用程序与在合作伙伴中心帐户中的项目相关联的唯一 ID。 您必须使用此 ID 连接使用 A / B 测试服务在应用代码中接收变体的数据和报告到合作伙伴中心的视图和转换事件。 有关详细信息，请参阅[针对实验为应用编码](code-your-experiment-in-your-app.md)。<p></p><p>每个项目和项目中的所有实验都只关联一个项目 ID。 你可以使用项目 ID 帮助区分不同的实验集。 例如，你可能有一组发布到组织测试人员的实验，还有另外一组仅发布到应用的外部用户的实验。  如果应用实现多个实验，它可以引用多个项目 ID。</p>         |
| 变动    |   你在实验中测试的一个或多个变量的集合。 每项实验必须拥有至少一个变量和两个变体（包括控件）。 实验可以有最多五个变体。           |
| 变量    |  你的应用用于初始化某个属性的值或应用中的另外一个值。 在实验中，变量值随变体更改而更改。 结束实验后，变量会分配由你选择发布到应用的所有用户的变体值。 变量可拥有以下类型：字符串、布尔值、双精度和整数。
| 视图事件    |  表示用户开始查看作为实验一部分的变体时，某项活动的任意字符串。 通常，这是你的代码中的某个事件的名称。 应用程序代码将发送到合作伙伴中心此视图事件字符串，当用户开始查看一种变体。 有关详细信息，请参阅[针对实验为应用编码](code-your-experiment-in-your-app.md)。
| 转换事件    |  表示实验目标的目的的任意字符串。 通常，这是你的代码中的某个事件的名称。 应用程序代码将发送到合作伙伴中心此转换事件字符串，当用户达到目的。 有关详细信息，请参阅[针对实验为应用编码](code-your-experiment-in-your-app.md)。  

## <a name="related-topics"></a>相关主题

* [创建项目并在合作伙伴中心定义远程变量](create-a-project-and-define-remote-variables-in-the-dev-center-dashboard.md)
* [代码应用程序进行试验](code-your-experiment-in-your-app.md)
* [在合作伙伴中心定义试验](define-your-experiment-in-the-dev-center-dashboard.md)
* [管理在合作伙伴中心实验](manage-your-experiment.md)
* [创建并运行你的第一个试验使用 A / B 测试](create-and-run-your-first-experiment-with-a-b-testing.md)
