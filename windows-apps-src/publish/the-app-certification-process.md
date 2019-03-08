---
Description: 当您完成创建应用程序的提交并单击提交到应用商店时，提交输入认证步骤。
title: 应用认证过程
ms.assetid: 0DCB4344-224D-4E5A-899F-FF7A89F23DBC
ms.date: 10/31/2018
ms.topic: article
keywords: windows 10，uwp，发布，预处理，认证，释放，挂起、 提交、 发布状态，时间
ms.localizationpriority: medium
ms.openlocfilehash: 733d5ff882d7ed7c574f6fe6fedd28b79c3913d9
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57597072"
---
# <a name="the-app-certification-process"></a>应用认证过程

当你完成应用提交的创建并单击**提交到 Microsoft Store** 时，提交将进入认证步骤。 此过程通常在几小时内完成，但在某些情况下可能需要最多三个工作日。 你的提交通过了认证后，它可能需要最多 24 小时的客户，若要查看新提交，或更改更新提交到包的应用程序的列表。 如果你更新仅更改了应用商店列表详细信息，将在不到一小时内完成发布过程。  发布你的提交，并在仪表板中的应用程序的状态将会通知您**在存储区**。

## <a name="preprocessing"></a>预处理

成功上载应用包并提交应用进行认证后，应用包将排队接受测试。 如果在预处理过程中检测到任何错误，我们会显示一条消息。 有关可能错误的详细信息，请参阅[解决提交错误](resolve-submission-errors.md)。

## <a name="certification"></a>认证

在此阶段中，将执行多个测试：

-   **安全测试：** 此第一个测试将检查病毒和恶意软件应用程序的包。 如果应用未能通过这项测试，您将需要运行最新防病毒软件检查开发系统，然后在安全的系统上重新生成您的应用包。
-   **技术符合性测试：** 通过 Windows 应用认证工具包测试技术符合性。 （你应该始终确保先[使用 Windows 应用认证工具包测试应用](../debug-test-perf/windows-app-certification-kit.md)，然后再将其提交至应用商店。）
-   **内容合规性：** 花费的时间量大小取决于您的应用程序是多么复杂，它有多大可视内容和最近已提交多少个应用。 请务必在[认证说明](notes-for-certification.md)页中提供测试者需注意的全部信息。

认证流程完成后，你将会收到一份认证报告，告知你的应用是否已通过认证。 如果应用未通过认证，该报告将指出未能通过哪项测试，或者未能满足哪项[策略](https://docs.microsoft.com/legal/windows/agreements/store-policies)。 修复问题后，你可以为应用创建新提交以再次开始认证过程。

## <a name="release"></a>发布版本

在您的应用程序通过认证，它已准备好移动到**发布**过程。

- 如果你指出应尽快 （默认选项） 发布你的提交，将立即开始发布过程。
- 如果这是首次发布应用程序中，并指定**发布日期**中[计划](configure-precise-release-scheduling.md#release)部分中，应用将变为可用根据你**发布日期**的选择。
- 如果使用过[发布保存选项](manage-submission-options.md#publishing-hold-options)若要指定，它才会释放特定日期之前，我们等着您若要开始发布过程中，此日期前必须选择**更改发布日期**。
- 如果使用过[发布保存选项](manage-submission-options.md#publishing-hold-options)若要指定你想要手动发布中的提交，我们不会开始发布过程直到选中**立即发布**(或选择**更改发布日期**并选择特定日期)。


## <a name="publishing"></a>Publishing

你的应用包已经过数字签名，目的是防止它们在发布后遭到篡改。 一旦开始执行此阶段，你将再也无法取消提交或更改其发布日期。

对于新的应用程序和更新包括对应用程序的包的更改，将在 24 小时内完成发布过程。 对于仅更改选项，如应用商店列表详细信息，但不更改应用的包的更新，发布过程将需要一个小时内。

在发布阶段，您的应用程序时**显示详细信息**应用的提交，可以知道当新的包和应用商店列表详细信息可供客户在每个受支持操作系统上的状态列中的链接版本。 尚未完成的步骤将显示**挂起**。 您的应用程序将保留在发布阶段直到完成该过程，也就是说，新的包和/或列表详细信息可供所有应用程序的潜在客户。

## <a name="in-the-store"></a>已在应用商店 

在成功完成上述步骤后，提交的状态将从“正在发布”更改为“已在应用商店”。 你的提交将在 Microsoft Store 中提供给客户以供其下载（除非你选择了另外的[可发现性](choose-visibility-options.md#discoverability)选项）。 

> [!NOTE]
> 我们还会在应用发布后对应用进行抽查，以便可以找出潜在问题并确保你的应用符合所有 [Microsoft Store 策略](https://docs.microsoft.com/legal/windows/agreements/store-policies)。 如果我们发现任何问题，将通知你该问题及其解决方法（如果适用）或是否已从应用商店中删除。

 

 

 




