---
title: /media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners
assetID: 5a519314-1df1-cbdc-cb04-3a8b663003de
permalink: en-us/docs/xboxlive/rest/uri-medialocalemetadatamediaitemtypequeryrefiners.html
author: KevinAsgari
description: " /media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 9273282ab20f06998a2d510f6c3d2b7e61ecf4a9
ms.sourcegitcommit: e6daa7ff878f2f0c7015aca9787e7f2730abcfbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "4308218"
---
# <a name="mediamarketplaceidmetadatamediaitemtypesmediaitemtypequeryrefiners"></a>/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners
对于给定的媒体项类型，请访问查询优化器。 这些 Uri 的域是`eds.xboxlive.com`。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | 
| marketplaceId| 字符串| 必需。 字符串从<b>Windows.Xbox.ApplicationModel.Store.Configuration.MarketplaceId</b>获得的值。| 
| mediaitemtype| 字符串| 必需。 从值之一[GET (/media/ {marketplaceId} / /metadata/mediagroups/ {mediagroup} / mediaItemTypes)](uri-medialocalemetadatamediagroupsmediaitemtypesget.md)。| 
  
<a id="ID4EBC"></a>

 
## <a name="valid-methods"></a>有效的方法

[GET (/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners)](uri-medialocalemetadatamediaitemtypequeryrefinersget.md)

&nbsp;&nbsp;列出了给定的媒体项类型查询优化器。
 
<a id="ID4ELC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ENC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[市场 URI](atoc-reference-marketplace.md)

  
<a id="ID4EXC"></a>

 
##### <a name="further-information"></a>详细信息 

[EDS 通用标头](../../additional/edscommonheaders.md)

 [EDS 参数](../../additional/edsparameters.md)

 [EDS 查询优化器](../../additional/edsqueryrefiners.md)

 [其他参考](../../additional/atoc-xboxlivews-reference-additional.md)

   