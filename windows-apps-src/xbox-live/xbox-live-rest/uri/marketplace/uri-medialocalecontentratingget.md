---
title: GET (/media/{marketplaceId}/contentRating)
assetID: e677acdb-d905-3bea-b0ca-6d8becd663c0
permalink: en-us/docs/xboxlive/rest/uri-medialocalecontentratingget.html
description: " GET (/media/{marketplaceId}/contentRating)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 8d1cb9d09de8671d4cd3d61e96a8335412237e5c
ms.sourcegitcommit: d2517e522cacc5240f7dffd5bc1eaa278e3f7768
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2018
ms.locfileid: "8328798"
---
# <a name="get-mediamarketplaceidcontentrating"></a>GET (/media/{marketplaceId}/contentRating)
获取内容分级令牌。 这些 Uri 的域是`eds.xboxlive.com`。
 
  * [备注](#ID4EV)
  * [URI 参数](#ID4ELB)
  * [查询字符串参数](#ID4EWB)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>备注
 
强制执行家长控制子级被允许看到的内容是一个复杂的任务。 每个媒体项类型具有其自己的分级系统，不仅这些分级系统可能会有所不同，随国家。 这意味着需要指定正确筛选的所有项的数据的多个不同部分。
 
而不是在所有 API 调用中指定的所有参数，此 API 生成的值，以将传递到其他 Api 中的**combinedContentRating**参数，仍传达相同的信息。 这被设计使 Api 更易于使用和维护，如传递到此 API 的多个参数处于折叠状态转换为单个、 可重复使用的值为其他 Api。
 
尽管此 api 返回的确切值最终可能会更改，他们应该很少更改 （例如版本娱乐发现服务 (EDS)），因此可能很长一段时间为缓存。 接受**combinedContentRating**参数将提供有意义的错误消息，如果传入的值是无效的这是指示任何 API 调用方只需要调用此 API 再次以获取更新的值。 如果 API 接受**combinedContentRating**参数，但其中一个未提供，未筛选的内容会发生具体取决于家长控制。 

> [!NOTE] 
> 这并不意味着，返回仅"安全"内容-这意味着，返回所有内容，包括潜在显式的内容。 


  
<a id="ID4ELB"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | --- | 
| marketplaceId| 字符串| 必需。 字符串从<b>Windows.Xbox.ApplicationModel.Store.Configuration.MarketplaceId</b>获得的值。| 
  
<a id="ID4EWB"></a>

 
## <a name="query-string-parameters"></a>查询字符串参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | --- | 
| filterExplicit| 布尔值| 可选。 筛选显式音乐。| 
| filterFamilyOnlyApps| 布尔值| 可选。 筛选未标记为系列友好的应用。| 
| filterUnrated| 布尔值| 可选。 确定是未分级的内容是否应在响应中是否包含。| 
| maxGameRating| 32 位有符号整数| 可选。 筛选游戏。| 
| maxMovieRating| 32 位有符号整数| 可选。 筛选上面某特定级别的电影。| 
| maxTVRating| 32 位有符号整数| 可选。 筛选电视。| 
  
<a id="ID4E5D"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EAE"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[/media/{marketplaceId}/contentRating](uri-medialocalecontentrating.md)

  
<a id="ID4EKE"></a>

 
##### <a name="further-information"></a>详细信息 

[EDS 通用标头](../../additional/edscommonheaders.md)

 [EDS 参数](../../additional/edsparameters.md)

 [EDS 查询优化器](../../additional/edsqueryrefiners.md)

 [市场 URI](atoc-reference-marketplace.md)

 [其他参考](../../additional/atoc-xboxlivews-reference-additional.md)

   