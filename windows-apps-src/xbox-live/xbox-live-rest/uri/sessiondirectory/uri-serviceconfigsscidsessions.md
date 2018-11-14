---
title: /serviceconfigs/{scid}/sessions
assetID: d1932817-dcce-5a5c-d7e4-9fd97e1d287c
permalink: en-us/docs/xboxlive/rest/uri-serviceconfigsscidsessions.html
author: KevinAsgari
description: " /serviceconfigs/{scid}/sessions"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: fa14d1d12ee951dfcaf6cd7beb91e09e39e11d93
ms.sourcegitcommit: f2c9a050a9137a473f28b613968d5782866142c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2018
ms.locfileid: "6257355"
---
# <a name="serviceconfigsscidsessions"></a>/serviceconfigs/{scid}/sessions
支持 GET 操作来检索一组会话文档。 
<a id="ID4EO"></a>

 
## <a name="domain"></a>域
sessiondirectory.xboxlive.com  
<a id="ID4ET"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| scid| GUID| 服务配置标识符 (SCID)。 第 1 部分会话的 id。| 
| 关键字| 字符串| 用于筛选结果以标识与该字符串的只是会话的关键字。| 
| xuid| GUID| 为其检索会话的用户的 Xbox 用户 Id。 用户必须在会话处于活动状态。| 
| 预订| 字符串| 值，该值指示如果会话列表包括用户具有不接受。 仅可以将此参数设置为 true。 此设置要求调用方拥有对会话，服务器级访问权限或调用方的 XUID 声明以匹配的 Xbox 用户 ID 筛选器。 | 
| 处于非活动状态| 字符串| 指示会话列表包括用户已接受，但不会主动玩游戏的值。 仅可以将此参数设置为 true。| 
| 专用| 字符串| 值，指示会话列表是否包含专用会话。 仅可以将此参数设置为 true。 仅在查询你自己的会话，或进行服务器到服务器查询时，它是有效。 将此参数设置为 true 要求调用方拥有对会话，服务器级访问权限或调用方的 XUID 声明以匹配的 Xbox 用户 ID 筛选器。 | 
| 可见性| 字符串| 指示用于筛选结果的可见性状态的枚举值。 当前此参数可以仅在设置为打开包含打开的会话。 请参阅<b>MultiplayerSessionVisibility</b>。| 
| version| 字符串| 正整数指示主要的会话版本或较低的会话以包括。 值必须小于或等于 100 模请求的协定版本。| 
| 参加| 字符串| 正整数指示会话最大数量来检索。| 
  
<a id="ID4E1D"></a>

 
## <a name="valid-methods"></a>有效的方法

[GET (/serviceconfigs/{scid}/sessions)](uri-serviceconfigsscidsessionsget.md)

&nbsp;&nbsp;检索指定会话信息。
 
<a id="ID4EEE"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EGE"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[会话目录 URI](atoc-reference-sessiondirectory.md)

   