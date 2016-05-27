---
author: jnHs
Description: 当使用 Windows 开发人员中心仪表板中的应用时，可以通过 Windows 应用商店查看与分配给它的唯一标识符相关的详细信息，并获取到应用的应用商店一览的链接。
title: 查看应用标识的详细信息
ms.assetid: 86F05A79-EFBC-4705-9A71-3A056323AC65
---

# 查看应用标识的详细信息


当使用 Windows 开发人员中心仪表板中的应用时，可以通过 Windows 应用商店查看与分配给它的唯一标识符相关的详细信息，并获取到应用的应用商店一览的链接。

若要找到此信息，请导航到其中一个应用，然后展开左侧导航菜单中的“应用管理”****。 单击“应用标识”****查看这些详细信息。

> **注意** 你需要拥有应用的[保留名称](create-your-app-by-reserving-a-name.md)才能查看大部分标识的详细信息。

## 要包含在 APPX 清单中的值


以下值必须包含在 APPX 清单中。 如果你使用 Microsoft Visual Studio 生成程序包，并使用与你的开发人员帐户关联的相同 Microsoft 帐户登录，则会自动包含这些详细信息。 如果手动生成程序包，则需要将这些信息添加到程序包中。

-   **程序包/标识/名称**
-   **程序包/标识/发布者**

有关详细信息，请参阅[程序包清单架构参考](https://msdn.microsoft.com/library/windows/apps/br211473)中的 [**Identity**](https://msdn.microsoft.com/library/windows/apps/br211441)。

同时，这些元素声明应用的标识、建立了所有程序包所属于的“程序包系列”。 单个程序包将具有其他详细信息，如体系结构和版本。

## 程序包系列的其他值


以下值是指应用的程序包系列的其他值，但不包含在清单内。

-   **程序包系列名称 (PFN)**：此值与某些 Windows API 结合使用。
-   **程序包 SID**：需要该值才能向应用发送 WNS 通知。 有关详细信息，请参阅 [Windows 推送通知服务 (WNS) 概述](https://msdn.microsoft.com/library/windows/apps/mt187203)。

## 链接到应用一览

可以共享应用的页面链接来帮助客户在应用商店中查找该应用。 此链接采用格式 **`https://www.microsoft.com/store/apps/<your app's Store ID>`**。

> **注意** 此 URL 适用于你的应用可在其中提供的任何操作系统版本。 你还可能会看到适用于 Windows 8.1 及更早版本和/或 Windows Phone 8.1 及更早版本的其他链接，它们仅适用于指定的操作系统版本。

当客户单击此链接时，它将打开基于 Web 的应用一览页。 如果你的应用适用于客户的 Windows 设备，应用商店应用还将启动并显示你的应用一览。

你的应用的**应用商店 ID** 也会在本部分中显示。 此应用商店 ID 可以用来[生成应用商店锁屏提醒](http://go.microsoft.com/fwlink/p/?LinkId=534236)或标识你的应用。

 

 






<!--HONumber=May16_HO2-->


