---
ms.assetid: 7a16b0ca-6b8e-4ade-9853-85690e06bda6
description: 了解如何使用 C# 启动间隙广告。
title: C# 间隙广告示例代码
ms.date: 03/22/2018
ms.topic: article
keywords: windows 10, uwp, 广告, 间隙, c#, 示例代码
ms.localizationpriority: medium
ms.openlocfilehash: a8276e1a9639b23a965c5a608fb951d1e1035133
ms.sourcegitcommit: d2517e522cacc5240f7dffd5bc1eaa278e3f7768
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "8345161"
---
# <a name="interstitial-ad-sample-code-in-c"></a>C\# 间隙广告示例代码 #  

本主题提供了显示间隙视频广告的基本 C# 和 XAML 通用 Windows 平台 (UWP) 应用的完整示例代码。 有关显示如何配置项目以使用此代码的分步说明，请参阅[间隙广告](interstitial-ads.md)。 有关完整示例项目，请参阅 [GitHub 上的广告示例](http://aka.ms/githubads)。

## <a name="code-example"></a>代码示例

本部分显示了显示间隙广告的基本应用中的 MainPage.xaml 和 MainPage.xaml.cs 文件内容。 若要使用这些示例，请将代码复制到 Visual Studio 中的 Visual C# **空白应用（通用 Windows）** 项目中。

此示例应用使用两个按钮请求和启动间隙广告。 值替换为```myAppId```和```myAdUnitId```字段从合作伙伴中心提交到应用商店应用之前的实时值。 有关详细信息，请参阅[在应用中设置广告单元](set-up-ad-units-in-your-app.md#live-ad-units)。

> [!NOTE]
> 若要更改此示例以显示间隙横幅广告而不是间隙视频广告，请将值 **AdType.Display** 传递至 [RequestAd](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.interstitialad.requestad) 方法的第一个参数而不是 **AdType.Video**。 有关详细信息，请参阅[间隙广告](interstitial-ads.md)。

### <a name="mainpagexaml"></a>MainPage.xaml

> [!div class="tabbedCodeSnippets"]
[!code-xml[InterstitialAd](./code/AdvertisingSamples/InterstitialAdSamples/cs/MainPage.xaml#L1-L13)]

### <a name="mainpagexamlcs"></a>MainPage.xaml.cs

> [!div class="tabbedCodeSnippets"]
[!code-cs[InterstitialAd](./code/AdvertisingSamples/InterstitialAdSamples/cs/MainPage.xaml.cs#CompleteSample)]

 
## <a name="related-topics"></a>相关主题

* [GitHub 上的广告示例](http://aka.ms/githubads)
 
