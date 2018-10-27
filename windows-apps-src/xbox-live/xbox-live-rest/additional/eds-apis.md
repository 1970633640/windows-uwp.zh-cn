---
title: 辅助 EDS API
assetID: 5729ab80-e88d-0190-fb61-bd0cc4f134f6
permalink: en-us/docs/xboxlive/rest/eds-apis.html
author: KevinAsgari
description: " 辅助 EDS API"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 791ec5e593d90cf52b91cca863df02da2db97f5f
ms.sourcegitcommit: 086001cffaf436e6e4324761d59bcc5e598c15ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2018
ms.locfileid: "5691853"
---
# <a name="auxiliary-eds-apis"></a>辅助 EDS API

有几个娱乐发现服务 (EDS) Api 不直接提供信息的内容，但提供了有关如何使用该服务或帮助驱动器常见 UI 模型的常规信息。

<a id="ID4EQ"></a>


## <a name="auxiliary-apis"></a>辅助 Api

| API| URI| 说明|
| --- | --- | --- |
| API 参数值| / {区域设置} / 元数据| 可以在服务的调用中使用的参数的可能值的枚举|
| 结合使用内容分级生成器| / {区域设置} / contentRating| 创建一个可用于其他 Api 为筛选出可能令人反感或显式的内容。 有关详细信息，请参阅下文。|
| 组合的字段名称生成器| / {区域设置} / 字段| 创建一个值，可在控制返回哪些字段的详细信息 Api。 有关详细信息，请参阅下文。|

<a id="ID4EBC"></a>


### <a name="api-parameter-values"></a>API 参数值

此 API 介绍了可以使用该服务的参数。 返回的信息是由客户端 UI，因为本地化的文本随每个参数。

无以下 Api 接受任何查询参数。

| API| URI| 说明|
| --- | --- | --- | --- | --- | --- |
| 类型| / {区域设置} / 元数据/mediaGroups| 媒体组的完整列表|
| 媒体项的每个媒体组的类型| / {区域设置} / /metadata/mediagroups/ {mediaItemTypeGroup} / mediaItemTypes| 媒体的列表项给定的媒体组内包含的类型。|
| 所有媒体项类型| / {区域设置} / 元数据/mediaItemTypes| 媒体项类型的完整列表|
| 每个媒体项类型的字段| / {区域设置} / /metadata/mediaitemtypes/ {mediaItemType} / 字段| 单个媒体项类型中的字段列表|
| 查询优化器| / {区域设置} / /metadata/mediaitemtypes/ {mediaItemType} / queryRefiners| 查询优化器支持给定的媒体项类型的列表|
| 所有查询精选值| / {区域设置} / 元数据/mediaItemTypes / {mediaItemType} /queryRefiners/ {queryRefiner}| 为给定的媒体指定的查询精选的值项类型|
| 所有查询精选子值| / {区域设置} / 元数据/mediaItemTypes / {mediaItemType} /queryRefiners/ {queryRefiner} / subQueryRefinerValues| 对于给定的查询精选值 (例如"subgenres 在给定流派") 的子值的列表。 名为"queryRefinerValue"，这是为了允许查询精选值以禁止在 URI 杆传递的字符的查询字符串参数传入查询精选值。|
| 排序| / {区域设置} / /metadata/mediaitemtypes/ {mediaItemType} / sortOrders| 对于给定的媒体项类型排序的列表|

<a id="ID4EEF"></a>


### <a name="combined-content-rating-generator"></a>结合使用内容分级生成器

强制执行家长控制子级被允许看到的内容是在复杂的任务。 每个媒体项类型具有其自己的分级系统，不仅这些分级系统可能会有所不同，从国家/地区为国家/地区。 这意味着需要指定正确筛选的所有项目的数据的多个不同部分。

而不是在所有 API 调用中指定的所有参数，此 API 生成一个值，以将传递到其他 Api 中的 combinedContentRating 参数，仍传达相同信息。 这被设计使 Api 更易于使用和维护，如传递到此 API 的多个参数处于折叠状态转换为单个、 可重复使用的值为其他 Api。

尽管此 API 返回的确切值可能会最终更改，他们应该很少更改 （例如 EDS 版本），并因此可能很长一段时间为缓存。 接受 combinedContentRating 参数将提供有意义的错误消息如果传入的值无效，即表明调用方只是任何 API 需要调用此 API 再次来获取更新的值。 如果 API 接受 combinedContentRating 参数，但一个未提供，未筛选的内容将基于家长控制

> [!NOTE]
> 这并不意味着，返回仅"安全"内容-这意味着，返回所有内容，包括潜在显式内容）。



<a id="ID4EWF"></a>


### <a name="combined-field-name"></a>组合的字段名称

EDS Api 中，默认情况下返回一组很少最小的每个项目的字段：

   * 媒体项类型
   * 媒体组
   * ID
   * 姓名

若要获取详细信息，这些 Api 接受指定应返回的数据的其他部分的"字段"参数。 有许多可能的域，因为它们的名称指定为每个 API 调用的完整会大大膨胀请求。 相反，可以将名称传递到此 API，这会生成可以传递到其他 Api 的很多较小的值。

对于接受此参数的任何 API，所提供的值必须中指定的媒体项的所有类型的所有字段的超集。 不能指定不同的用于不同的媒体项类型的字段集。 但是，如果字段适用于一个媒体项类型，但不是另一个，它将仅出现在媒体项类型存在数据 (例如仅 AvatarItems"AvatarBodyType"包含到组合的字段名称 API 的调用中，如果将包含该字段)。

从该 API 返回的值是高度缓存-实际上，它们不应更改除之间的 EDS 部署。 建议，如果缓存，缓存的最后一个不会超过用户的会话。

除了接受的实际的字段名称，此 API 接受"全部"作为有效的值。 这将生成包含可指定每个字段的值。 "全部"值很可能仅用于开发、 调试和测试目的。

<a id="ID4ERG"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4ETG"></a>


##### <a name="parent"></a>Parent 的子磁盘）  

[其他参考](atoc-xboxlivews-reference-additional.md)


<a id="ID4E6G"></a>


##### <a name="further-information"></a>详细信息

[市场 URI](../uri/marketplace/atoc-reference-marketplace.md)
