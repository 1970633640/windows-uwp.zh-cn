---
ms.assetid: 9630AF6D-6887-4BE3-A3CB-D058F275B58F
description: 了解如何使用 Windows.Services.Store 命名空间获取当前应用及其加载项的许可证信息。
title: 获取应用和加载项的许可证信息
ms.date: 12/04/2017
ms.topic: article
keywords: windows 10, uwp, 许可证, 应用, 加载项, 应用内购买, IAP, Windows.Services.Store
ms.localizationpriority: medium
ms.openlocfilehash: 4d7c832907af17436d588f0fac6c5039d4affa82
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57641912"
---
# <a name="get-license-info-for-apps-and-add-ons"></a>获取应用和加载项的许可证信息

本文介绍了如何使用 [Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx) 命名空间中 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 类的方法，来获取当前应用及其加载项的许可证信息。 例如，你可以使用此信息来确定应用或其加载项的许可证是否处于活动状态，或确定它们是否是试用许可证。

> [!NOTE]
> **Windows.Services.Store** 命名空间在 Windows 10 版本 1607 中引入，它仅可用于面向 **Windows 10 周年纪念版（10.0；版本 14393）或 Visual Studio** 更高版本的项目中。 如果你的应用面向 Windows 10 的较早版本，则必须使用 [Windows.ApplicationModel.Store](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.store.aspx) 命名空间来替代 **Windows.Services.Store** 命名空间。 有关详细信息，请参阅[此文章](in-app-purchases-and-trials-using-the-windows-applicationmodel-store-namespace.md)。

## <a name="prerequisites"></a>必备条件

本示例有以下先决条件：
* 适用于面向 **Windows 10 周年纪念版（10.0；版本 14393）或**更高版本的通用 Windows 平台 (UWP) 应用的 Visual Studio 项目。
* 你有[创建应用程序提交](https://msdn.microsoft.com/windows/uwp/publish/app-submissions)在合作伙伴中心和此应用程序发布的存储区中。 在测试应用期间，你可以选择将应用配置为在 Microsoft Store 中隐藏。 有关详细信息，请参阅我们的[测试指南](in-app-purchases-and-trials.md#testing)。
* 如果你想获取许可证信息的应用外接程序，您必须还[在合作伙伴中心中创建外接程序](../publish/add-on-submissions.md)。

此示例中的代码假设：
* 代码在含有 [ProgressRing](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.progressring.aspx)（名为 ```workingProgressRing```）和 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)（名为 ```textBlock```）的 [Page](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.page.aspx) 上下文中运行。 这些对象分别用于指示是否正在进行异步操作和显示输出消息。
* 代码文件有一个适用于 **Windows.Services.Store** 命名空间的 **using** 语句。
* 该应用是单用户应用，仅在启动该应用的用户上下文中运行。 有关详细信息，请参阅[应用内购买和试用](in-app-purchases-and-trials.md#api_intro)。

> [!NOTE]
> 如果你有使用[桌面桥](https://developer.microsoft.com/windows/bridges/desktop)的桌面应用程序，可能需要添加不在此示例中显示的额外代码来配置 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 对象。 有关详细信息，请参阅[在使用桌面桥的桌面应用程序中使用 StoreContext 类](in-app-purchases-and-trials.md#desktop)。

## <a name="code-example"></a>代码示例

若要获取当前应用的许可证信息，请使用 [GetAppLicenseAsync](https://docs.microsoft.com/uwp/api/windows.services.store.storecontext.getapplicenseasync) 方法。 这是一种异步方法，它返回提供应用的许可证信息的 [StoreAppLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.aspx) 对象，其中包括指示用户当前是否具有使用应用的有效许可证的属性 ([IsActive](https://docs.microsoft.com/uwp/api/windows.services.store.storeapplicense.isactive)) 和指示许可证是否用于试用版的属性 ([IsTrial](https://docs.microsoft.com/uwp/api/windows.services.store.storeapplicense.istrial))。

若要访问用户有权使用的当前应用的持久性加载项的许可证，请使用 [StoreAppLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.aspx) 对象的 [AddOnLicenses](https://docs.microsoft.com/uwp/api/windows.services.store.storeapplicense.addonlicenses) 属性。 此属性返回 [StoreLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storelicense.aspx) 对象集合，表示加载项许可证。

> [!div class="tabbedCodeSnippets"]
[!code-cs[GetLicenseInfo](./code/InAppPurchasesAndLicenses_RS1/cs/GetLicenseInfoPage.xaml.cs#GetLicenseInfo)]

有关完整的示例应用程序，请参阅[应用商店示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Store)。

## <a name="related-topics"></a>相关主题

* [应用内购买和试用版](in-app-purchases-and-trials.md)
* [获取产品信息的应用程序和外接程序](get-product-info-for-apps-and-add-ons.md)
* [启用应用内购买的应用程序和外接程序](enable-in-app-purchases-of-apps-and-add-ons.md)
* [启用可使用外接程序购买](enable-consumable-add-on-purchases.md)
* [实现您的应用程序的试用版](implement-a-trial-version-of-your-app.md)
* [应用商店示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Store)
