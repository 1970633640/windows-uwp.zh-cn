---
author: mcleanbyron
ms.assetid: 08b4ae43-69e8-4424-b3c0-a07c93d275c3
description: "了解如何在应用中捕获 AdControl 错误。"
title: "JavaScript 演练中的错误处理"
translationtype: Human Translation
ms.sourcegitcommit: cf695b5c20378f7bbadafb5b98cdd3327bcb0be6
ms.openlocfilehash: d26a8efeb253c6c793d8edd21d7452bbf15da261


---

# JavaScript 演练中的错误处理


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

本主题演示如何在应用中捕获 [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx) 错误。

这些示例假定你拥有一个 JavaScript/HTML 应用，它包含一个 **AdControl**。 有关演示如何向你的应用添加 **AdControl** 的分步说明，请参阅 [HTML 5 和 Javascript 中的 AdControl](adcontrol-in-html-5-and-javascript.md)。 有关演示如何将横幅广告添加到 JavaScript/HTML 应用的完整示例项目，请参阅 [GitHub 上的广告示例](http://aka.ms/githubads)。

1.  在 default.html 文件中，在 **div** 中针对 **AdControl** 定义 **data-win-options** 的所在位置添加适用于 **onErrorOccurred** 事件的值。 在 default.html 文件中找到以下代码。

    ``` syntax
    <div id="myAd" style="position: absolute; top: 53px; left: 0px; width: 300px; height: 250px; z-index: 1"
         data-win-control="MicrosoftNSJS.Advertising.AdControl"
         data-win-options="{applicationId: '3f83fe91-d6be-434d-a0ae-7351c5a997f1', adUnitId: '10865270'}">
    </div>
    ```

    在 **adUnitId** 之后，添加适用于 **onErrorOccurred** 事件的值。

    ``` syntax
    onErrorOccurred: errorLogger
    ```

    以下是 **div** 的完整代码。

    ``` syntax
    <div id="myAd" style="position: absolute; top: 53px; left: 0px; width: 300px; height: 250px; z-index: 1"
         data-win-control="MicrosoftNSJS.Advertising.AdControl"
         data-win-options="{applicationId: '3f83fe91-d6be-434d-a0ae-7351c5a997f1', adUnitId: '10865270', onErrorOccurred: errorLogger}">
    </div>
    ```

2.  创建将显示文本的 **div**，以便你可以看到所生成的消息。 为此，在 **div** 后面添加用于 **myAd** 的以下代码。

    ``` syntax
    <div style="position:absolute; width:100%; height:130px; top:300px; left:0px">
        <b>Ad Events</b><br />
        <div id="adEvents" style="width:100%; height:110px; overflow:auto"></div>
    </div>
    ```

3.  创建将触发错误事件的 **AdControl**。 对于应用中的所有 **AdControl** 对象，只可以有一个应用程序 ID。 因此创建具有不同应用程序 ID 的其他对象将在运行时触发错误。 为此，在先前添加的 **div** 部分的后面，将以下代码添加到 default.html 页面的正文中。

    ``` syntax
    <!-- since only one applicationId can be used, the following ad control will fire an error event -->
    <div id="liveAd" style="position: absolute; top:500px; left:0px; width:480px; height:80px"
        data-win-control="MicrosoftNSJS.Advertising.AdControl"
        data-win-options="{applicationId: '00000000-0000-0000-0000-000000000000',
        adUnitId: '10865270', onErrorOccurred: errorLogger }" >
    </div>
    ```

4.  在项目的 default.js 文件中，在默认的初始化函数的后面，需要添加用于 **errorLogger** 的事件处理程序。 滚动到文件末尾，在最后一个分号的后面就是你要添加以下代码的位置。

    ``` syntax
    WinJS.Utilities.markSupportedForProcessing(
    window.errorLogger = function (sender, evt) {
        adEvents.innerHTML = (new Date()).toLocaleTimeString() + ": " +
        sender.element.id + " error: " + evt.errorMessage + " error code: " +
        evt.errorCode + "<br>" + adEvents.innerHTML;
        console.log("errorhandler hit. \n");
    });
    ```

5.  生成并运行该文件。

你将看到来自你先前生成的示例应用中的原始广告，以及该广告下描述错误的文本。 你将不会看到具有 **liveAd** 的 ID 的广告。

## 相关主题

* [GitHub 上的广告示例](http://aka.ms/githubads)

 



<!--HONumber=Jun16_HO4-->


