---
Description: Learn how to create effective and user-focused notifications that make your users productive and happy.
title: Toast UX 指南
label: Toast UX Guidance
template: detail.hbs
ms.date: 05/18/2018
ms.topic: article
keywords: windows 10，uwp，通知，集合、 组、 ux，ux 指南，指导、 操作、 toast、 操作中心、 noninterruptive、 有效通知、 非侵入式通知，操作，管理，组织
ms.localizationpriority: medium
ms.openlocfilehash: 17861760ea5640eca01d3e69c1ed36a023c8f9d3
ms.sourcegitcommit: b4c502d69a13340f6e3c887aa3c26ef2aeee9cee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "8478801"
---
# <a name="toast-notification-ux-guidance"></a>Toast 通知的 UX 指南
通知是必不可少的现代生命; 一它们可以帮助用户更高效、 应用和网站，以及使用任何更新保持当前使用的预定。 但是，通知很快就会从适用于 overbearing 和产生干扰，如果它们不设计以用户为中心的方式。 通知是远离已关闭，一个右键单击，并且处于关闭状态后，它是不太可能，它们会将重新打开。  因此请确保通知尊重用户的屏幕空间和时间，因此你可以保留此参与通道打开。

> **重要 Api**: [Windows 社区工具包通知 nuget 程序包](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Notifications/)

我们已分析我们 Windows 遥测后，以及其他第一个和第三方案例研究以拿出什么使出色通知故事周围的四个规则。  我们将这些规则普遍适用，无论该平台，并且将帮助你对你的用户产生积极影响的通知。

## <a name="1-actionable-notifications"></a>1.可操作的通知
可操作通知允许用户成效而无需打开你的应用。  时非常适合具有应用启动、 这不是唯一的度量值的成功，并使用户能够执行完成小任务而无需转到你的应用可以在 delighting 用户非常强大的工具。

![带有输入的文本框和按钮设置提醒并响应通知的可操作通知](images/actionable-notification-example01.png)

上面是通知的一个利用操作的示例。 完成任务的感觉是通用正面的感觉，和你可以通过发送通知，其中包含的可操作的内容移植到你的应用或网站的感觉。 可操作通知还有助于提高工作效率，同时在企业和消费者的情况下，通过减少向操作用户的时间介绍完成这些较小的任务。 我们建议包括你的用户定期采取，操作或尝试培训你的用户执行的操作。  一些示例如下：
* 根据需要，favoriting，标记，或者标星号内容
* 批准或拒绝费用报表、 关、 权限等的时间。
* 内联回复邮件，电子邮件，组聊天、 注释，等等。
* 完成订单使用[挂起的更新](toast-pending-update.md)
* 另一次，设置警报或提醒，以及可能在日历上预订时间

ctionable 通知是一个非常强大的工具，以帮助用户感觉高效、 完成任务，并且具有与你的应用或网站的出色且有效的体验。  有很多机会此处 ！ 如果你希望触发想法的帮助，可随意联系 windows 通知团队。  你 

## <a name="2-timing-and-urgency"></a>2.计时和紧急情况
与如何我们通常认为通知，实时不一定是最佳 ！ 我们建议考虑用户和他们正在发送的通知是否紧急信息的开发人员，或不。 用户可以轻松地重载太多信息，并获取沮丧，如果它们在中断时正在对焦。 Windows 提供了有关如何侵入你发送的通知，请考虑的几个选项：

**原始通知：** 使用[原始通知](raw-notification-overview.md)可以很有利出于多种原因，尤其是在左键最小化用户中断。  发送原始通知将唤醒你的应用在后台，这样通知有意义立即提供你的应用的上下文中是否可以访问。 如果它是某些感觉应显示给用户立即，可以从[本地 toast](send-local-toast.md)弹出。  如果这是一个用户不需要查看现在，你都能够创建[计划的 toast](https://blogs.msdn.microsoft.com/tiles_and_toasts/2016/09/30/quickstart-sending-an-alarm-in-windows-10/)将在以后触发。

**映像 toast:** 还可以引发将跳过弹出在右下角的屏幕，并改为通知直接发送到操作中心的通知。 这被通过[SuppressPopup 属性](https://docs.microsoft.com/en-us/uwp/api/windows.ui.notifications.toastnotification.suppresspopup)设置为 True。 尽管可能存在一些怀疑周围不在操作中心之外弹出通知，我们可以看到 2-3 倍更高版本上生活在操作中心的 toast 的参与度弹出 toast。  当他们已准备好接收通知，可以控制当它们中断，这是在操作中心中的内容可以是 noninvasively 通知用户得更有效的原因，用户将更具响应性。

## <a name="3-clear-out-the-clutter"></a>3.清除待筛选邮件
通知可以保留在操作中心内相当长时间 （默认值为三天）。  务必确保位于此处的内容是保持最新状态和相关，每次用户打开操作中心。 你有浪费用户的屏幕空间，以及占用本来用于更保持最新内容的空位。  我们假设用户安装你的电子邮件的管理应用，并接收十个电子邮件和以及这些电子邮件的十个通知。  具体取决于你所需的体验，你可以考虑清除这些通知，如果用户已阅读相应的电子邮件，或作为一种方法从操作中心中删除旧的待筛选邮件打开应用。

我们提供了一系列[ToastNotificationHistory](https://docs.microsoft.com/en-us/uwp/api/windows.ui.notifications.toastnotificationhistory)可让你可以查看哪些内容是在操作中心中的 Api 以及管理这些通知。 尊重用户的屏幕空间，并负责将仅显示当前的相关内容给用户。

## <a name="4-keeping-organized"></a>4.保持组织
如前面所述，在操作中心中的内容未保留为三天。  为了帮助你选取出快速寻找的信息的用户，组织中使用[标头](https://docs.microsoft.com/en-us/windows/uwp/design/shell/tiles-and-notifications/toast-headers)或[集合](https://docs.microsoft.com/en-us/uwp/api/windows.ui.notifications.toastcollection)的操作中心的通知。 你可以看到以下标头的示例。

![使用标头的 toast 示例标记为 Camping!!](images/toast-headers-action-center.png)

这两个这些 gorup 通知，因此相关的内容保持在一起的方式 （即考虑区分不同的体育联赛中的体育应用中，或按群聊对消息进行排序）。 集合与组通知，以更明显的方式，而标头是更巧妙的但同时允许用户会审和更快地选择退出通知。 

## <a name="other-resources"></a>其他资源
上述这些四个点是我们发现有效通过自己的分析遥测，并通过第一个和第三方实验的指南。 记住，但是，这些指南只是： 指南。  我们确信这些规则有助于提高参与度和效率的通知，但不是可以替代以用户为中心的考虑，并了解从自己的数据。  

如果现在将通知发送到你的 UWP 应用，你可以在[合作伙伴中心](https://partner.microsoft.com/dashboard)中通知发生了什么事情查看分析 ！ 使用[应用商店服务 SDK](https://marketplace.visualstudio.com/items?itemName=AdMediator.MicrosoftStoreServicesSDK)或[WNS Api](https://docs.microsoft.com/en-us/windows/uwp/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview)时，可以免费此数据。 这些指标将为你提供更深入通知在 windows 平台上，会发生什么情况以及如何用户通知与之交互。 访问此数据，方法转到菜单上左侧参与 > 通知，然后单击"分析"选项卡中通知页面上。  该文件位于同一位置会变为从合作伙伴中心发送通知。

## <a name="related-topics"></a>相关主题

* [Toast 内容](adaptive-interactive-toasts.md)
* [原始通知](raw-notification-overview.md)
* [挂起更新](toast-pending-update.md)
* [GitHub 上的通知库（Windows 社区工具包的一部分）](https://github.com/Microsoft/UWPCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.Notifications)
