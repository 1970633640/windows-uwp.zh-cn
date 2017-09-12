---
author: jnHs
Description: "在 Windows 开发人员中心仪表板中管理和查看与每一个应用相关的详细信息，并配置通知、A/B 测试和地图等服务。"
title: "应用管理和服务"
ms.assetid: 99DA2BC1-9B5D-4746-8BC0-EC723D516EEF
ms.author: wdg-dev-content
ms.date: 06/19/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, uwp
ms.openlocfilehash: 2ff75a5e85a37f4f47b6b32f3e8338524752bb2f
ms.sourcegitcommit: fadde8afee46238443ec1cb71846d36c91db9fb9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2017
---
# <a name="app-management-and-services"></a>应用管理和服务

你可以在 Windows 开发人员中心仪表板中管理和查看与每一个应用相关的详细信息，并配置通知、A/B 测试和地图等服务。

在仪表板中使用应用时，将在左侧导航菜单中看到**服务**和**应用管理**部分。 可以展开这些部分，访问如下所述的功能。

## <a name="services"></a>服务

**服务**部分让你可以管理多个不同的应用服务。

## <a name="push-notifications"></a>推送通知

**推送通知**部分支持创建通知以及将其发送到应用客户。 可将这些通知发送到所有应用客户，或者发送到满足[客户类别](create-customer-segments.md)中所定义条件的 Windows 10 客户的子集。 有关详细信息，请参阅[将通知发送到应用客户](send-push-notifications-to-your-apps-customers.md)。

还可在左侧导航菜单中单击 **WNS/MPNS**，将以下选项的其中一项用于推送通知，具体取决于应用包类型及其特定要求： 

-   可使用 **Windows 推送通知服务 (WNS)** 从自己的云服务中发送 Toast、磁贴、锁屏提醒和原始更新。 有关详细信息，请参阅 [Windows 推送通知服务 (WNS) 概述](https://msdn.microsoft.com/library/windows/apps/mt187203)。

-   你可以使用 **Microsoft Azure 移动应用**发送推送通知、验证和管理应用用户，以及将应用数据存储在云中。 有关详细信息，请参阅[“移动应用”文档](http://go.microsoft.com/fwlink/p/?LinkId=221116)。

-   **Microsoft 推送通知服务 (MPNS)** 可以和 Windows Phone 的 .xap 程序包结合使用。 你可以在此处发送有限数量的未经验证的通知而不进行任何配置，不过为了避免节流限制，我们建议使用经过验证的通知。 如果你使用的是 MPNS，则需要将证书上传到**“推送通知”**页面上所提供的字段中。 有关详细信息，请参阅[设置经过验证的 Web 服务以发送 Windows Phone 8 的推送通知](http://go.microsoft.com/fwlink/p/?LinkId=528736)。

## <a name="experimentation"></a>实验

将**实验**页和 A/B 测试结合，用于创建并运行通用 Windows 平台 (UWP) 应用的实验。 在 A/B 测试中，你先衡量应用更改对某些客户的有效性，然后再为所有用户启用更改。

有关详细信息，请参阅[通过 A/B 测试运行应用实验](../monetize/run-app-experiments-with-a-b-testing.md)。

## <a name="maps"></a>地图

若要在适用于 Windows Phone 8.1 及更早版本的应用中使用地图服务，需要在应用代码中包含地图服务应用程序 ID 和令牌。 可在**服务**部分的**地图**页面上获取此令牌。

> [!NOTE]
> 若要在面向 Windows 10 或 Windows 8.x 的应用中使用地图服务，请访问[必应地图开发人员中心](http://go.microsoft.com/fwlink/p/?LinkId=614880)。 有关详细信息，请参阅[请求地图身份验证密钥](https://msdn.microsoft.com/library/windows/apps/mt219694)。

有关详细信息，请参阅[使用地图服务](use-map-services.md)。

## <a name="product-collections-and-purchases"></a>产品收集和购买

若要使用 Windows 应用商店收集 API 和 Windows 应用商店购买 API 来访问应用和加载项的所有权信息，需要在此处输入相关联的 Azure AD 客户端 ID。 请注意，需要 16 个小时才能使这些更改生效。

有关详细信息，请参阅[管理来自服务的产品授权](../monetize/view-and-grant-products-from-a-service.md)。

## <a name="app-management"></a>应用管理

可以使用**应用管理**部分查看标识和软件包详细信息，并管理你的应用的名称。

## <a name="app-identity"></a>应用标识

此页面向你显示了你的应用在应用商店中的唯一标识的相关详细信息，包括用于链接到应用一览的 URL。

有关详细信息，请参阅[查看应用标识详细信息](view-app-identity-details.md)。

## <a name="manage-app-names"></a>管理应用名称

这是查看已为应用保留的所有名称的位置。 你可以从中保留额外名称，或删除将不再使用的名称。

有关详细信息，请参阅[管理应用名称](manage-app-names.md)。

## <a name="current-packages"></a>当前程序包

可以使用此页面查看与所有已发布程序包相关的详细信息。

> [!NOTE]
> 直到你的应用完成发布后，你才会在此处看到信息。

将显示每个程序包的名称、版本和体系结构。 单击**详细信息**可显示支持的语言、应用功能和文件大小等其他信息。 所见到的每个程序包的具体信息可能有所不同，具体取决于目标操作系统和其他因素。 

具有 OEM 权限的开发人员还可以在**当前程序包**页面[生成预安装程序包](generate-preinstall-packages-for-oems.md)。

 

 
