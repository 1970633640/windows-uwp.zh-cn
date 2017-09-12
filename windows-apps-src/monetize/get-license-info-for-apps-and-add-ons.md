---
author: mcleanbyron
ms.assetid: 9630AF6D-6887-4BE3-A3CB-D058F275B58F
description: "了解如何使用 Windows.Services.Store 命名空间获取当前应用及其加载项的许可证信息。"
title: "获取应用和加载项的许可证信息"
ms.author: mcleans
ms.date: 06/26/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "windows 10, uwp, 许可证, 应用, 加载项, 应用内购买, IAP, Windows.Services.Store"
ms.openlocfilehash: dbd37ed219d47ad2c7631170c4299af708404243
ms.sourcegitcommit: 6c6f3c265498d7651fcc4081c04c41fafcbaa5e7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2017
---
# <a name="get-license-info-for-apps-and-add-ons"></a>获取应用和加载项的许可证信息

面向 Windows10 版本 1607 或更高版本的应用可以使用 [Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx) 命名空间中 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 类的方法，以获取当前应用及其加载项的许可证信息。 例如，你可以使用此信息来确定应用或其加载项的许可证是否处于活动状态，或确定它们是否是试用许可证。

> [!NOTE]
> 本文适用于面向 Windows 10 版本 1607 或更高版本的应用。 如果你的应用面向 Windows 10 的较早版本，则必须使用 [Windows.ApplicationModel.Store](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.store.aspx) 命名空间来替代 **Windows.Services.Store** 命名空间。 有关详细信息，请参阅[使用 Windows.ApplicationModel.Store 命名空间进行应用内购买和试用](in-app-purchases-and-trials-using-the-windows-applicationmodel-store-namespace.md)。

## <a name="prerequisites"></a>先决条件

本示例有以下先决条件：
* 适用于面向 Windows10 版本 1607 或更高版本的通用 Windows 平台 (UWP) 应用的 Visual Studio 项目。
* 你已在 Windows 开发人员中心仪表板中[创建了一个应用提交](https://msdn.microsoft.com/windows/uwp/publish/app-submissions)，并且该应用已发布到应用商店中。 在测试应用期间，你可以选择将应用配置为在应用商店中隐藏。 有关详细信息，请参阅[测试指南](in-app-purchases-and-trials.md#testing)。
* 如果你想要获取应用的某个加载项的许可证信息，还必须[在开发人员中心仪表板中创建加载项](../publish/add-on-submissions.md)。 

此示例中的代码假设：
* 代码在含有 [ProgressRing](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.progressring.aspx)（名为 ```workingProgressRing```）和 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)（名为 ```textBlock```）的 [Page](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.page.aspx) 上下文中运行。 这些对象分别用于指示是否正在进行异步操作和显示输出消息。
* 代码文件有一个适用于 **Windows.Services.Store** 命名空间的 **using** 语句。
* 该应用是单用户应用，仅在启动该应用的用户上下文中运行。 有关详细信息，请参阅[应用内购买和试用](in-app-purchases-and-trials.md#api_intro)。

> [!NOTE]
> 如果你有使用[桌面桥](https://developer.microsoft.com/windows/bridges/desktop)的桌面应用程序，可能需要添加不在此示例中显示的额外代码来配置 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 对象。 有关详细信息，请参阅[在使用桌面桥的桌面应用程序中使用 StoreContext 类](in-app-purchases-and-trials.md#desktop)。

## <a name="code-example"></a>代码示例

若要获取当前应用的许可证信息，请使用 [GetAppLicenseAsync](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.getapplicenseasync.aspx) 方法。 这是一种异步方法，可返回提供应用的许可证信息的 [StoreAppLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.aspx) 对象，其中包括指示用户是否具有使用应用的许可证的属性 ([IsActive](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.isactive.aspx)) 和指示许可证是否用于试用版的属性 ([IsTrial](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.istrial.aspx))。

若要检索应用的加载项许可证，请使用 [StoreAppLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.aspx) 对象的 [AddOnLicenses](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.addonlicenses.aspx) 属性。 此属性返回 [StoreLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storelicense.aspx) 对象集合，表示应用的加载项许可证。 若要确定用户是否具有使用加载项的许可证，请使用 [IsActive](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storelicense.isactive.aspx) 属性。

> [!div class="tabbedCodeSnippets"]
[!code-cs[GetLicenseInfo](./code/InAppPurchasesAndLicenses_RS1/cs/GetLicenseInfoPage.xaml.cs#GetLicenseInfo)]

有关完整的示例应用程序，请参阅[应用商店示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Store)。

## <a name="related-topics"></a>相关主题

* [应用内购买和试用](in-app-purchases-and-trials.md)
* [获取应用和加载项的产品信息](get-product-info-for-apps-and-add-ons.md)
* [支持应用内购买应用和加载项](enable-in-app-purchases-of-apps-and-add-ons.md)
* [支持购买易耗型加载项](enable-consumable-add-on-purchases.md)
* [实现应用的试用版](implement-a-trial-version-of-your-app.md)
* [应用商店示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Store)
