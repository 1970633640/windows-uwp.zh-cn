---
title: 市场 URI
assetID: 27b6035f-84b9-67a8-6a12-85c450d18a58
permalink: en-us/docs/xboxlive/rest/atoc-reference-marketplace.html
author: KevinAsgari
description: " 市场 URI"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 96055bd7a2d4169c15e37b55aa70a94fab128a59
ms.sourcegitcommit: 144f5f127fc4fbd852f2f6780ef26054192d68fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2018
ms.locfileid: "5994964"
---
# <a name="marketplace-uris"></a>市场 URI

本部分提供有关统一资源标识符 (URI) 地址和关联的超文本传输协议 (HTTP) 方法的详细信息，从 Xbox Live 服务的*应用商店*服务，也称为娱乐发现服务 (EDS)。

仅 Xbox 360、 Windows Phone 设备，或在 Xbox.com 上运行的游戏均可使用此服务。

这些 Uri 的域是 eds.xboxlive.com 和 inventory.xboxlive.com。

<a id="ID4EPB"></a>

 
## <a name="in-this-section"></a>本部分内容

[/users/me/inventory](uri-inventory.md)

&nbsp;&nbsp;访问当前与提供的用户相关联的清单的集。

[/users/me/consumables/{itemID}](uri-inventoryconsumablesitemurl.md)

&nbsp;&nbsp;访问完整的一组特定的易耗型库存项目的详细信息。

[/inventory/{itemID}](uri-inventoryitemurl.md)

&nbsp;&nbsp;访问完整的一组特定的库存项目的详细信息。

[/media/{marketplaceId}/crossMediaGroupSearch](uri-localecrossmediagroupsearch.md)

&nbsp;&nbsp;访问多个不同的媒体组中的项。

[/media/{marketplaceId}/browse](uri-medialocalebrowse.md)

&nbsp;&nbsp;允许浏览单个媒体组中的项。

[/media/{marketplaceId}/contentRating](uri-medialocalecontentrating.md)

&nbsp;&nbsp;访问内容分级令牌。

[/media/{marketplaceId}/details](uri-medialocaledetails.md)

&nbsp;&nbsp;详细信息和元数据，产品/服务返回有关的一个或多个项目。

[/media/{marketplaceId}/fields](uri-medialocalefields.md)

&nbsp;&nbsp;访问字段令牌。

[/media/{marketplaceId}/metadata/mediaGroups](uri-medialocalemetadatamediagroups.md)

&nbsp;&nbsp;列出所有受支持的 mediaGroups 给定 EDS 版本。

[/media/{marketplaceId}/metadata/mediaGroups/{mediagroup}/mediaItemTypes](uri-medialocalemetadatamediagroupsmediaitemtypes.md)

&nbsp;&nbsp;访问每个媒体组可用 mediaItemTypes EDS 的给定版本。

[/media/{marketplaceId}/metadata/mediaItemTypes/{mediaItemType}/fields](uri-medialocalemetadatamediaitemtypefields.md)

&nbsp;&nbsp;访问从其中一个期待看到的数据，为给定的 mediaitemtype 和 EDS 给定的版本字段。

[/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners](uri-medialocalemetadatamediaitemtypequeryrefiners.md)

&nbsp;&nbsp;对于给定的媒体项的类型，请访问查询优化器。

[/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners/{queryrefinername}](uri-medialocalemetadatamediaitemtypequeryrefinersqueryrefinername.md)

&nbsp;&nbsp;访问可接受的值为给定的查询精选名称和给定的媒体项的类型。

[/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/queryrefiners/{queryRefiner}/subQueryRefinerValues](uri-medialocalemediaitemtypequeryrefinersubqueryrefinervalues.md)

&nbsp;&nbsp;为某个给定的查询精选值 (例如，"subgenres 在给定流派") 的访问权限的子值列表。

[/media/{marketplaceId}/metadata/mediaItemTypes](uri-medialocalemetadatamediaitemtypes.md)

&nbsp;&nbsp;访问所有受支持的 mediaItemTypes 给定 EDS 版本。

[/media/{marketplaceId}/metadata/mediaItemTypes/{mediaitemtype}/sortorders](uri-medialocalemetadatamediaitemtypesortorders.md)

&nbsp;&nbsp;可用的访问排序给定的 mediaitem 类型和 EDS 给定的版本。

[/media/{marketplaceId}/singleMediaGroupSearch](uri-medialocalesinglemediagroupsearch.md)

&nbsp;&nbsp;允许搜索单个媒体组中的项。

<a id="ID4EFD"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EHD"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[统一资源标识符 (URI) 参考](../atoc-xboxlivews-reference-uris.md)


<a id="ID4ERD"></a>


##### <a name="further-information"></a>详细信息

[其他参考](../../additional/atoc-xboxlivews-reference-additional.md)
