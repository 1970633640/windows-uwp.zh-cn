---
author: mcleanbyron
ms.assetid: 646977ed-1705-4ea7-a3db-a6b9aac70703
description: "了解如何使用 JavaScript/HTML 启动间隙广告。"
title: "JavaScript 中的间隙广告示例代码"
ms.author: mcleans
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "windows 10, uwp, 广告, 间隙, javascript, 示例代码"
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: 91a54bdd2e41b3e7df0ee0aad32448ab9ed66ac0
ms.lasthandoff: 02/07/2017

---

# <a name="interstitial-ad-sample-code-in-javascript"></a>JavaScript 中的间隙广告示例代码

本主题提供了显示间隙广告的基本 JavaScript 和 HTML 通用 Windows 平台 (UWP) 应用的完整示例代码。 有关显示如何配置项目以使用此代码的分步说明，请参阅[间隙广告](interstitial-ads.md)。 有关完整示例项目，请参阅 [GitHub 上的广告示例](http://aka.ms/githubads)。

## <a name="code-example"></a>代码示例

本部分显示了显示间隙广告的基本应用中的 HTML 和 JavaScript 文件内容。 若要使用这些示例，请将代码复制到 Visual Studio 2015 中的 JavaScript **WinJS 应用（通用 Windows）**项目中。

此示例应用使用两个按钮请求和启动间隙广告。 Visual Studio 生成的 main.js 和 index.html 文件已修改，如下所示。 script.js 文件（如下所示）包含示例中的大部分代码，应该将此文件添加到项目的 **js** 文件夹中。

>**Windows 8.x 和 Windows Phone 8.1 的注意事项**&nbsp;&nbsp;如果你的项目面向 Windows 8.1 或 Windows Phone 8.1，则项目中的默认 HTML 文件名为 default.html 而不是 index.html，且项目中的默认 JavaScript 文件名为 default.js 而不是 main.j。

将应用提交到应用商店之前，将 ```applicationId``` 和 ```adUnitId``` 变量的值替换为 Windows 开发人员中心的实时值。有关详细信息，请参阅[在应用中设置广告单元](set-up-ad-units-in-your-app.md)。

### <a name="indexhtml"></a>index.html

> [!div class="tabbedCodeSnippets"]
[!code-html[InterstitialAd](./code/AdvertisingSamples/InterstitialAdSamples/js/index.html#L1-L21)]

<span/>
>**Windows 8.x 和 Windows Phone 8.1 的注意事项**&nbsp;&nbsp;如果你的项目面向 Windows 8.1 或 Windows Phone 8.1，请将示例中的 ```<script src="//Microsoft.Advertising.JavaScript/ad.js"></script>``` 行替换为 ```<script src="/MSAdvertisingJS/ads/ad.js"></script>```。

### <a name="scriptjs"></a>script.js

> [!div class="tabbedCodeSnippets"]
[!code-javascript[InterstitialAd](./code/AdvertisingSamples/InterstitialAdSamples/js/script.js#script)]

### <a name="mainjs"></a>main.js

> [!div class="tabbedCodeSnippets"]
[!code-javascript[InterstitialAd](./code/AdvertisingSamples/InterstitialAdSamples/js/main.js#main)]

## <a name="related-topics"></a>相关主题

* [GitHub 上的广告示例](http://aka.ms/githubads)

 

