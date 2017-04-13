---
author: jnHs
Description: "你可以使用其他开发人员发布的应用交叉推广你的应用。 我们将此功能称为社区广告。"
title: "有关社区广告"
ms.assetid: F55CE478-99AF-4B70-90D1-D16419562136
ms.author: wdg-dev-content
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.openlocfilehash: 708f46dc0be53961d8fd26f41a933e5756720a98
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="about-community-ads"></a>有关社区广告

如果你的应用使用 **AdMediatorControl** 或 **AdControl** 显示横幅广告，可以在 Windows 应用商店中通过应用与其他开发人员一起免费交叉推广你的应用。 我们将此功能称为*社区广告*。  

以下是此计划的运作方式：

* 在你[选择加入社区广告](#how-to-opt-in-to-community-ads)并[创建免费的社区广告市场活动](create-an-ad-campaign-for-your-app.md)后，你的应用将与其他同样选择加入社区广告的开发人员共享推广广告空间。 你的应用将会显示其他加入社区广告的开发人员发布的应用的广告，而他们的应用也会显示你的应用的广告。
* 通过在你的应用中显示社区广告，你可以获取在其他应用中拥有推广广告空间的信用。 信用根据以下过程计算：
  * 对于每个有提供社区广告的应用的国家或地区，该国家或地区的当前市场行情 eCPM（每千次印象有效成本）值乘以你的应用在该国家或地区进行的社区广告请求数。 此值就是你在该国家或地区为你的应用获取的信用。
  * 你在给定时间段内获取的总信用等于每个提供社区广告的应用在每个国家或地区获取的所有信用之和。
* 你的信用会在所有活动社区广告市场活动中平均分配，并且会根据你的社区广告市场活动面向的国家/地区的当前市场行情 eCPM 值转换为应用广告印象。
* 若要在应用中跟踪社区广告的性能，请参阅[帐户级别的广告性能报告](advertising-performance-report.md#account-level-advertising-performance-report)。

## <a name="how-to-opt-in-to-community-ads"></a>如何选择加入社区广告

若要选择加入社区广告，请执行以下操作：

1. 在 Windows 开发人员中心仪表板中转到“盈利”****&gt;“利用广告来盈利”****页。
2. 在“社区广告”****部分中，选中“在我的应用中显示社区广告”****框。
   > **注意**  选中或取消选中此框后，无需重新发布应用来使更改生效。

3. 为你的应用[创建广告市场活动](create-an-ad-campaign-for-your-app.md)。 对于市场活动类型，选择“免费社区广告”****。


## <a name="related-topics"></a>相关主题

* [利用广告来盈利](monetize-with-ads.md)
* [为你的应用创建广告市场活动](create-an-ad-campaign-for-your-app.md)
