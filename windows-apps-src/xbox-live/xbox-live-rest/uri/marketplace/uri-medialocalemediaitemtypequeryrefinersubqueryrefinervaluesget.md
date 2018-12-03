---
title: GET (/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners/{queryRefiner}/subQueryRefinerValues)
assetID: 0fcbef77-4607-765e-72e1-d2e7620e2c61
permalink: en-us/docs/xboxlive/rest/uri-medialocalemediaitemtypequeryrefinersubqueryrefinervaluesget.html
description: " GET (/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners/{queryRefiner}/subQueryRefinerValues)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 183d15a306d0f15fcb5f9f7fad8411772f763c13
ms.sourcegitcommit: d2517e522cacc5240f7dffd5bc1eaa278e3f7768
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2018
ms.locfileid: "8332955"
---
# <a name="get-mediamarketplaceidmetadatamediaitemtypesmediaitemtypequeryrefinersqueryrefinersubqueryrefinervalues"></a>GET (/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners/{queryRefiner}/subQueryRefinerValues)
对于给定的查询精选值 (例如，"subgenres 在给定流派") 中获取子值的列表。 这些 Uri 的域是`eds.xboxlive.com`。
 
  * [备注](#ID4EV)
  * [URI 参数](#ID4EDB)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>备注
 
名为**queryRefinerValue**，这是为了允许查询精选值以禁止在 URI 杆传递的字符的查询字符串参数传入查询精选值。
 
此 API 仅支持音乐。
  
<a id="ID4EDB"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | 
| marketplaceId| 字符串| 必需。 字符串从<b>Windows.Xbox.ApplicationModel.Store.Configuration.MarketplaceId</b>获得的值。| 
  
<a id="ID4EOB"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EQB"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners/{queryRefiner}/subQueryRefinerValues](uri-medialocalemediaitemtypequeryrefinersubqueryrefinervalues.md)

  
<a id="ID4E1B"></a>

 
##### <a name="further-information"></a>详细信息 

[EDS 通用标头](../../additional/edscommonheaders.md)

 [EDS 参数](../../additional/edsparameters.md)

 [EDS 查询优化器](../../additional/edsqueryrefiners.md)

 [市场 URI](atoc-reference-marketplace.md)

 [其他参考](../../additional/atoc-xboxlivews-reference-additional.md)

   