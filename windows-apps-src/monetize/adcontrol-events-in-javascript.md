---
author: mcleanbyron
ms.assetid: 2383296e-c3d7-4b49-bcd2-621391228fdb
description: "了解如何处理 AdControl 类的事件。"
title: "JavaScript 中的 AdControl 事件"
translationtype: Human Translation
ms.sourcegitcommit: f88a71491e185aec84a86248c44e1200a65ff179
ms.openlocfilehash: e652fe6b5f295c0f4b4808e5a4605c13fdcfea68

---

# <a name="adcontrol-events-in-javascript"></a>JavaScript 中的 AdControl 事件

以下示例演示了下面 [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx) 事件（[ErrorOccurred](https://msdn.microsoft.com/library/windows/apps/xaml/microsoft.advertising.winrt.ui.adcontrol.erroroccurred.aspx)、[AdRefreshed](https://msdn.microsoft.com/library/windows/apps/xaml/microsoft.advertising.winrt.ui.adcontrol.adrefreshed.aspx) 和 [IsEngagedChanged](https://msdn.microsoft.com/library/windows/apps/xaml/microsoft.advertising.winrt.ui.adcontrol.isengagedchanged.aspx)）的基本事件处理程序。 这些示例假设你已向 HTML 标记中的事件分配了事件处理程序。 有关如何执行此操作的详细信息，请参阅 [HTML 属性示例](html-properties-example.md)。

在 JavaScript 中，**AdControl** 事件必须包含在 [MarkSupportedForProcessing](http://msdn.microsoft.com/library/windows/apps/Hh967819.aspx) 函数中。 有关处理 JavaScript 中的事件的详细信息，请参阅 [编码基本应用 (HTML)](https://msdn.microsoft.com/library/windows/apps/hh780660.aspx#adding-event-handlers)。

## <a name="examples"></a>示例

> [!div class="tabbedCodeSnippets"]
[!code-javascript[AdControl](./code/AdvertisingSamples/AdControlSamples/js/main.js#EventHandlers)]

## <a name="related-topics"></a>相关主题

* [GitHub 上的广告示例](http://aka.ms/githubads)
* [AdControl 错误处理](adcontrol-error-handling.md)
* [RoutedEventArgs 类](http://msdn.microsoft.com/library/system.windows.routedeventargs.aspx)

 

 



<!--HONumber=Dec16_HO2-->


