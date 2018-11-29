---
ms.assetid: B356C442-998F-4B2C-B550-70070C5E4487
description: 了解如何使用 Windows.Services.Store 命名空间购买应用或其加载项之一。
title: 支持应用内购买应用和加载项
keywords: windows 10, uwp, 加载项, 应用内购买, IAP, Windows.Services.Store
ms.date: 08/25/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: a64a52005221c418ea82e8fffa9ecf94b6d1bef3
ms.sourcegitcommit: b5c9c18e70625ab770946b8243f3465ee1013184
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "7980516"
---
# <a name="enable-in-app-purchases-of-apps-and-add-ons"></a>支持应用内购买应用和加载项

本文介绍了如何使用 [Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx) 命名空间中的成员，请求为用户购买当前应用或其加载项之一。 例如，如果用户当前有应用的试用版，可以使用此过程为用户购买完整版。 或者，你可以使用此过程购买加载项，如用户的新游戏关卡。

若要请求购买应用或加载项，[Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx) 命名空间提供了几个不同方法：
* 如果你知道应用或加载项的[应用商店 ID](in-app-purchases-and-trials.md#store_ids)，可以使用 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 类的 [RequestPurchaseAsync](https://docs.microsoft.com/uwp/api/windows.services.store.storecontext.requestpurchaseasync) 方法。
* 如果你已有表示应用或加载项的 [**StoreProduct**、**StoreSku** 或 **StoreAvailability** 对象](in-app-purchases-and-trials.md#products-skus)，可以使用这些对象的 **RequestPurchaseAsync** 方法。 有关可用于在你的代码中检索**StoreProduct** 的不同方法的示例，请参阅[获取应用和加载项的产品信息](get-product-info-for-apps-and-add-ons.md)。

每个方法都为用户提供标准购买 UI，随后在交易完成后异步完成这些方法。 该方法返回一个指示该交易是否已成功的对象。

> [!NOTE]
> **Windows.Services.Store** 命名空间在 Windows 10 版本 1607 中引入，它仅可用于面向 **Windows 10 周年纪念版（10.0；版本 14393）或 Visual Studio** 更高版本的项目中。 如果你的应用面向 Windows 10 的较早版本，则必须使用 [Windows.ApplicationModel.Store](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.store.aspx) 命名空间来替代 **Windows.Services.Store** 命名空间。 有关详细信息，请参阅[此文](in-app-purchases-and-trials-using-the-windows-applicationmodel-store-namespace.md)。

## <a name="prerequisites"></a>先决条件

本示例有以下先决条件：
* 适用于面向 **Windows 10 周年纪念版（10.0；版本 14393）或**更高版本的通用 Windows 平台 (UWP) 应用的 Visual Studio 项目。
* 你有合作伙伴中心中的[创建应用提交](https://msdn.microsoft.com/windows/uwp/publish/app-submissions)，并在应用商店中发布此应用。 在测试应用期间，你可以选择将应用配置为在应用商店中隐藏。 有关详细信息，请参阅我们的[测试指南](in-app-purchases-and-trials.md#testing)。
* 如果你想要启用应用的加载项的应用内购买，则必须[创建合作伙伴中心中的加载项](../publish/add-on-submissions.md)。

此示例中的代码假设：
* 代码在含有 [ProgressRing](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.progressring.aspx)（名为 ```workingProgressRing```）和 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)（名为 ```textBlock```）的 [Page](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.page.aspx) 上下文中运行。 这些对象分别用于指示是否正在进行异步操作和显示输出消息。
* 代码文件有一个适用于 **Windows.Services.Store** 命名空间的 **using** 语句。
* 该应用是单用户应用，仅在启动该应用的用户上下文中运行。 有关详细信息，请参阅[应用内购买和试用](in-app-purchases-and-trials.md#api_intro)。

> [!NOTE]
> 如果你有使用[桌面桥](https://developer.microsoft.com/windows/bridges/desktop)的桌面应用程序，可能需要添加不在此示例中显示的额外代码来配置 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 对象。 有关详细信息，请参阅[在使用桌面桥的桌面应用程序中使用 StoreContext 类](in-app-purchases-and-trials.md#desktop)。

## <a name="code-example"></a>代码示例

此示例演示如何使用 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 类的 [RequestPurchaseAsync](https://docs.microsoft.com/uwp/api/windows.services.store.storecontext.requestpurchaseasync) 方法，购置具有已知[应用商店 ID](in-app-purchases-and-trials.md#store-ids) 的应用或加载项。 有关完整的示例应用程序，请参阅[应用商店示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Store)。

> [!div class="tabbedCodeSnippets"]
[!code-cs[EnablePurchases](./code/InAppPurchasesAndLicenses_RS1/cs/PurchaseAddOnPage.xaml.cs#PurchaseAddOn)]

## <a name="video"></a>视频

观看以下视频，大致了解如何在你的应用中实现应用内购买。
<br/>
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/One-Dev-Minute/Adding-In-App-Purchases-to-Your-UWP-App/player]

## <a name="related-topics"></a>相关主题

* [应用内购买和试用](in-app-purchases-and-trials.md)
* [获取应用和加载项的产品信息](get-product-info-for-apps-and-add-ons.md)
* [获取应用和加载项的许可证信息](get-license-info-for-apps-and-add-ons.md)
* [支持购买易耗型加载项](enable-consumable-add-on-purchases.md)
* [实现应用的试用版](implement-a-trial-version-of-your-app.md)
* [应用商店示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Store)
