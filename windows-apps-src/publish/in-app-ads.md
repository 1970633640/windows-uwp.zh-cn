---
Description: 如果您的应用程序显示广告使用 Microsoft Advertising SDK，使用合作伙伴中心的应用内广告页管理的广告使用。
title: 应用内广告
ms.assetid: 09970DE3-461A-4E2A-88E3-68F2399BBCC8
ms.date: 10/31/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: cfdc4bd81a96d3bbdb2dd369cbdd0444ca22ea4c
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57658022"
---
# <a name="in-app-ads"></a>应用内广告

使用**Monetize** &gt; **应用内广告**页[合作伙伴中心](https://partner.microsoft.com/dashboard)来创建和管理有关的广告单元：

* 使用 [Microsoft 广告 SDK](https://aka.ms/ads-sdk-uwp) 的通用 Windows 平台 (UWP) 应用。
* 以前发布的 Windows 8.x 和 Windows Phone 8.x 应用使用的[Microsoft 广告 SDK 的 Windows 和 Windows Phone 8.x](https://aka.ms/store-8-sdk)。

> [!IMPORTANT]
> 自 2018 年 10 月 31 日起，新创建的产品不能包括面向 Windows 8.x/Windows 包 Phone 8.x 或更早版本。 有关详细信息，请参阅此[博客文章](https://blogs.windows.com/buildingapps/2018/08/20/important-dates-regarding-apps-with-windows-phone-8-x-and-earlier-and-windows-8-8-1-packages-submitted-to-microsoft-store/#SzKghBbqDMlmAO4c.97)。

有关如何将这些 SDK 与你的应用集成以显示广告的详细信息，请参阅[使用 Microsoft 广告 SDK 在你的应用中显示广告](../monetize/display-ads-in-your-app.md)。

<span id="create-ad-unit" />

## <a name="create-ad-units"></a>创建广告单元

若要在你的应用中为[横幅广告](../monetize/banner-ads.md)、[间隙广告](../monetize/interstitial-ads.md)或[本机广告](../monetize/native-ads.md)创建广告单元，请执行以下操作：

1.  转到**Monetize** &gt; **应用内广告**在合作伙伴中心页，然后单击**创建 ad 单元**。
2.  在**应用名称**下拉列表中，选择将在其中使用广告单元的应用。
3.  在**广告单元名称**字段中，输入广告单元的名称。 这可以是希望因报告目的而用来标识广告单元的任意描述性字符串。
4.  在**广告单元类型**下拉列表中，选择广告类型。

    * 如果应用程序中显示横幅广告时，选择**横幅**。
    * 如果显示插播式视频广告或插播式横幅广告应用程序中，选择**插播式视频**或**横幅插播式**（请务必选择适当的选项的类型插播式 ad 想要显示)。
    * 如果应用程序中显示本机 ad 时，选择**本机**。

5. 在**设备系列**下拉框中，选择将在其中使用广告单元的应用所适用的设备系列。 可用选项包括：**UWP (Windows 10)**， **PC/平板电脑 (Windows 8.1)**，或**Mobile (Windows Phone 8.x)**。

6. 根据需要配置以下其他设置：

    * 如果你为广告单元选择 **UWP (Windows 10)** 设备系列，则可以选择为广告单元配置[中介设置](#mediation)。
    * 如果你为横幅广告单元选择**电脑/平板电脑 (Windows 8.1)** 或**移动设备 (Windows Phone 8.x)** 设备系列，则可以选择 **Show community ads in your app** 以选择加入[社区广告](about-community-ads.md)。

7.  如果还没有为所选的应用设置 COPPA 合规性，请在 [COPPA 合规性](#coppa)部分中选择一个选项。
8.  单击“创建广告单元”。

创建新的 ad 单元后，它会显示可用的 ad 单位中的表中**Monetize** &gt; **应用内广告**页。

<span id="available-ad-units" />

## <a name="review-and-edit-ad-units"></a>查看和编辑广告单元

在帐户中创建一个或多个应用的广告单元后，在底部的表中显示这些广告单元**Monetize** &gt; **应用内广告**页。 此表显示每个广告单元的**应用程序 ID** 和**广告单元 ID** 以及其他信息。 若要在应用中显示广告，需要在你的代码中使用这些值。 有关详细信息，请参阅[在应用中设置广告单元](../monetize/set-up-ad-units-in-your-app.md)。

* 如果你的应用显示[横幅广告](../monetize/banner-ads.md)，请将这些值分配给 [AdControl](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol) 对象的 [ApplicationId](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.applicationid) 和 [AdUnitId](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.adunitid) 属性。
* 如果你的应用显示[间隙广告](../monetize/interstitial-ads.md)，请将这些值传递给 [InterstitialAd](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.interstitialad) 对象的 [RequestAd](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.interstitialad.requestad) 方法。
* 如果您的应用程序显示[本机广告](../monetize/native-ads.md)，将对这些值传递**NativeAdsManagerV2**构造函数。
  > [!IMPORTANT]
  > 每个广告单元都只能在一个应用中使用。 如果在多个应用中使用某个广告单元，将不为该广告单元提供广告。

  > [!NOTE]
  > 你可以在单个应用中使用多个横幅广告、间隙广告和本机广告控件。 在此情况下，我们建议你为每个控件分配不同的广告单元。 对每个控件使用不同的广告单元使你可以分别[配置中介设置](../publish/in-app-ads.md#mediation)并获取每个控件的独立[报告数据](../publish/advertising-performance-report.md)。 这还使我们的服务能够更好地优化我们为应用提供的广告。

若要编辑 UWP 广告单元的[中介设置](#mediation)或此广告单元所用于的应用的 [COPPA 合规性](#coppa)，请单击广告单元的名称。

> [!NOTE]
> 如果广告单元的过去 6 个月没有任何活动，我们会将将其作为标记**非活动**，并将最终从合作伙伴中心将其删除。 你可以使用筛选器来仅显示**活动**或**停用**广告单位。 如果看到你认为被不准确地标记为**停用**的任何广告单元，请[联系支持人员](https://aka.ms/storesupport)。

<span id="mediation" />

## <a name="mediation-settings"></a>中介设置

当您[创建新的 UWP ad 单元](#create-ad-unit)或[编辑现有 UWP ad 单元](#available-ad-units)，使用在本部分中的选项来配置[ad 中介](../monetize/ad-mediation-service.md)ad 单元。 广告中介显示来自多个广告网络（包括其他付费广告网络）的广告以及 Microsoft 应用促销活动的非盈利性广告，能够最大化广告收益和应用促销能力。 我们负责调停来自所选广告网络的横幅广告请求。 如果已在应用中拥有与横幅广告、间隙广告或本机广告相关联的 UWP 广告单元，则启用广告中介无需在应用中进行任何代码更改。

> [!NOTE]
> 为 UWP 广告单元启用广告中介时，不需要从第三方广告网络获取广告单元。 我们的广告中介服务会自动创建任何必要的第三方广告单元。

若要为应用中的 UWP 广告单元配置广告中介设置，请执行以下操作：

1. [创建广告单元](#create-ad-unit)或[选择现有广告单元](#available-ad-units)。
2. 上**应用内广告**页上，转到**中介设置**部分，并配置你的设置。

    * 默认情况下**告知 Microsoft 优化我的设置**复选框处于选中状态。 我们建议你使用此选项。 此选项会使用机器学习算法自动为你的应用选择广告中介设置，以帮助最大化你在你的应用所支持的各市场中的广告收益。 当使用此选项时，还可以选择你想要在配置中使用的 ad 网络。 取消选中不想要配置的一部分，我们的算法将确保您的应用程序仅从所选的 ad 网络接收广告的广告网络。
    * 如果你想要选择你自己的 ad 中介设置，请选择**修改默认设置**。

    > [!NOTE]
    > 在本部分中的剩余步骤才适用则选择**修改默认设置**。

3. 在**目标**下拉框中，选择**基线**为你的广告中介设置配置默认配置。 此默认配置将应用于除你在其中定义了市场特定配置之外的所有市场。
4. 接下来，指定你希望在控件中显示的来自付费网络（针对广告印象向你支付收益）和其他广告网络（不针对广告印象向你支付收益）的广告的比例。 要执行此操作，请在**付费广告网络**和**其他广告网络**的**权重**字段中输入介于 0 至 100 之间的值。  
5. 在**付费广告网络**部分中，针对要使用的每种[付费网络](#paid-networks)，选中**活动**列中的复选框，然后使用**排名**列中的箭头按名次为网络排序（这指定控件应使用每种网络的频率）。
6. 如果选择了**横幅**或**横幅间隙**广告单元，也将看到一个**其他广告网络**部分。 此部分中的网络不会因广告曝光而为你挣取收益。 相反，这些网络显示来自应用促销市场活动等来源的广告。

    在**其他广告网络**部分中，针对希望使用的每种[其他网络](#other-networks)，选中**活动**列中的复选框，然后使用**排名**列中的箭头按名次为网络排序（这指定控件应使用每种网络的频率）。 当前支持以下其他网络：

7. 对于你想要为其替代默认中介配置的每个市场，请在**目标**下拉框中选择市场，然后更新广告网络选择和排名。
8. 单击**创建广告单元**（如果你要创建新的广告单元）或**保存**（如果正在编辑现有广告单元）。

<span id="paid-networks" />

### <a name="supported-paid-ad-networks"></a>支持的付费广告网络

下表列出了我们当前针对每种广告类型支持的付费网络。 请注意，这之中的某些网络[并非适用于所有市场](#network-markets)。

|  广告网络  |  描述  |  支持的广告类型  |
|--------------|---------------|---------------------|
| Oath 和 AppNexus |  这是提供网络： Oath 和 AppNexus 的广告通过我们的合作伙伴的 Microsoft 托管 ad 网络。<p/>**注意**：Oath 和 AppNexus 始终排名第一次在**付费广告网络**横幅广告单元，和它的列表不能更改为这些类型的广告的较低排名。 | 横幅、视频间隙 |
| AppNexus（直接） | 选择此选项可提供从广告[AppNexus](https://www.appnexus.com)。 | 视频间隙、本机  |
| Microsoft 应用安装广告 | 选择此选项以提供由 Windows 生态系统中[为其应用创建促销广告市场活动](create-an-ad-campaign-for-your-app.md)的其他开发人员创建的应用安装广告或应用重新参与广告。  |  横幅、横幅间隙、本机  |
| MSN 内容建议 |  选择此选项可从 MSN 内容建议提供广告。 |  横幅、横幅间隙  |
| Outbrain |  选择此选项以提供来自 [Outbrain](https://www.outbrain.com/) 的广告。 |  横幅、横幅间隙  |
| Revcontent |  选择此选项以提供来自 [Revcontent](https://www.revcontent.com/) 的广告。 |  横幅、本机  |
| Smaato |  选择此选项以提供来自 [Smaato](https://www.smaato.com/) 的广告。 |  横幅  |
| smartclip |  选择此选项以提供来自 [smartclip](https://www.smartclip.com/) 的广告。 |  视频间隙  |
| SpotX |  选择此选项以提供来自 [SpotX](https://www.spotx.tv/) 的广告。 |  视频间隙  |
| Taboola |  选择此选项以提供来自 [Taboola](https://www.taboola.com/) 的广告。 |  横幅  |
| Undertone | 选择此选项可提供从广告[Undertone](https://www.undertone.com/)。 | 插播式横幅 |


<span id="other-networks" />

### <a name="other-ad-networks"></a>其他广告网络

下表列出了我们当前针对每种广告类型支持的其他网络。

|  广告网络  |  描述  |  支持的广告类型  |
|--------------|---------------|---------------------|
| Microsoft 社区广告 |  如果[为应用之一创建促销广告市场活动](create-an-ad-campaign-for-your-app.md)并将此市场活动配置为[社区广告市场活动](about-community-ads.md)，则选择此选项以显示来自此市场活动的广告。 | 横幅、横幅间隙 |
| Microsoft 自家广告 | 如果[为应用之一创建促销广告市场活动](create-an-ad-campaign-for-your-app.md)并将此市场活动配置为[自家广告市场活动](about-house-ads.md)，则选择此选项以显示来自此市场活动的广告。 | 横幅、横幅间隙  |


<span id="network-markets" />

### <a name="supported-markets-for-ad-networks"></a>广告网络支持的市场

可用的广告网络在所有[支持的市场](define-market-selection.md#microsoft-store-consumer-markets)中提供广告，以下市场例外。

|  广告网络  |  支持的市场  |
|--------------|---------------------|
| Revcontent | 巴西、加拿大、法国、德国、印度、日本、西班牙、英国、美国  |
| Smaato | 巴西、加拿大、法国、德国、印度、日本、西班牙、英国、美国 |
| smartclip | 奥地利、比利时、丹麦、芬兰、德国、意大利、荷兰、挪威、瑞典、瑞士  |
| Undertone | 美国 |

<span id="coppa" />

## <a name="coppa-compliance"></a>COPPA 合规性

时您[创建广告单元](#create-ad-unit)或[选择现有 ad 单元](#available-ad-units)，则**COPPA 法规遵从性**节，显示在页面底部，如果至少有适用于 ad 单位的所选的应用已达到的一个提交[存储区中](../publish/the-app-certification-process.md#in-the-store)应用认证过程中的步骤。

根据《儿童在线隐私保护法》（“COPPA”），如果你的应用面向 13 岁以下的儿童，则你必须在这个部分选择**此应用程序面向 13 岁以下的儿童**。 如果选择此选项，则 Microsoft 将采取措施以在向你的应用发送广告时禁用其行为广告服务。

你选择的 **COPPA 合规性**设置将自动应用于所选应用的所有广告单元。

> [!IMPORTANT]
> 如果你的应用面向 13 岁以下的儿童，则你承担 COPPA 规定的某些义务。 有关你的义务的详细信息，请参阅[此页面](https://go.microsoft.com/fwlink/p/?linkid=536558)。
