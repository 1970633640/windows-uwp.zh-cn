---
author: mcleanbyron
ms.assetid: 2ed21281-f996-402d-a968-d1320a4691df
description: "请使用本文中的测试应用程序 ID 和广告单元 ID 值，查看应用在测试期间如何呈现广告。"
title: "测试模式值"
ms.author: mcleans
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "windows 10, uwp, 广告, 测试"
ms.openlocfilehash: 0c3e713d9a2bb7c10bda0d9517f5cb882d5e2e57
ms.sourcegitcommit: 6b772d2a224f8a9c557dc517c6ec0592545e9a43
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2017
---
# <a name="test-mode-values"></a>测试模式值

当你使用 [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx)、[InterstitialAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.interstitialad.aspx) 或 [NativeAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.nativead.aspx) 在应用中显示广告时，必须在 **AdUnitId** 和 **ApplicationId** 属性中指定广告单元 ID 和应用程序 ID。 当你开发应用时，请使用本文中的测试应用程序 ID 和广告单元 ID 值，查看应用在测试期间如何呈现广告。

如果你尝试在发布动态应用后在其中使用测试值，应用将不会收到广告。 若要在你已发布的应用中接收广告，必须更新你的代码才能使用 Windows 开发人员中心仪表板提供的应用程序 ID 和 广告单元 ID。 有关详细信息，请参阅[在应用中设置广告单元](set-up-ad-units-in-your-app.md)。
 
下面是要用于不同广告类型的测试值。

* 对于间隙广告：

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">目标操作系统</th>
    <th align="left">AdUnitId</th>
    <th align="left">ApplicationId</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>UWP (Windows 10)</p></td>
    <td align="left"><p>test</p></td>
    <td align="left"><p>d25517cb-12d4-4699-8bdc-52040c712cab</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Windows 8.x 和 Windows Phone 8.x</p></td>
    <td align="left"><p>11389925</p></td>
    <td align="left"><p>d25517cb-12d4-4699-8bdc-52040c712cab</p></td>
    </tr>
    </tbody>
    </table>

     
* 对于横幅广告：

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">目标操作系统</th>
    <th align="left">AdUnitId</th>
    <th align="left">ApplicationId</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>UWP (Windows 10)</p></td>
    <td align="left"><p>test</p></td>
    <td align="left"><p>3f83fe91-d6be-434d-a0ae-7351c5a997f1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Windows 8.x 和 Windows Phone 8.x</p></td>
    <td align="left"><p>10865270</p></td>
    <td align="left"><p>3f83fe91-d6be-434d-a0ae-7351c5a997f1</p></td>
    </tr>
    </tbody>
    </table>

* 本机广告：

    <table>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">目标操作系统</th>
    <th align="left">AdUnitId</th>
    <th align="left">ApplicationId</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>UWP (Windows 10)</p></td>
    <td align="left"><p>test</p></td>
    <td align="left"><p>d25517cb-12d4-4699-8bdc-52040c712cab</p></td>
    </tbody>
    </table>

> [!IMPORTANT]
> 对于 **AdControl**，实时广告的大小由 **Width** 和 **Height** 属性定义。 为获得最佳结果，请确保代码中的 **Width** 和 **Height** 属性是[横幅广告的受支持广告大小](supported-ad-sizes-for-banner-ads.md)之一。 **Width** 和 **Height** 属性不会根据实时广告的大小而发生更改。


 

 
