---
title: / 用户/xuid ({xuid}) /scids/ {scid} / 统计数据
assetID: 3cf9ffd4-9a8b-2658-402b-2e933f7f6f1b
permalink: en-us/docs/xboxlive/rest/uri-usersxuidscidsscidstats.html
author: KevinAsgari
description: " / 用户/xuid ({xuid}) /scids/ {scid} / 统计数据"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 2fa886078d429719eb50aa8567bfe238768ba2e3
ms.sourcegitcommit: c8f6866100a4b38fdda8394ea185b02d7af66411
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2018
ms.locfileid: "3960834"
---
# <a name="usersxuidxuidscidsscidstats"></a>/ 用户/xuid ({xuid}) /scids/ {scid} / 统计数据
访问由逗号分隔列表的代表指定用户的用户统计数据名称范围的服务配置。 这些 Uri 的域是`userstats.xboxlive.com`。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| xuid| GUID| Xbox 用户 ID (XUID) 的用户的名义访问的服务配置。| 
| scid| GUID| 服务配置，其中包含要访问的资源的标识符。| 
  
<a id="ID4E4B"></a>

 
## <a name="valid-methods"></a>有效的方法

[GET](uri-usersxuidscidsscidstatsget.md)

&nbsp;&nbsp;获取由逗号分隔列表的代表指定用户的用户统计数据名称范围的服务配置。

[获取与值元数据](uri-usersxuidscidsscidstatsgetvaluemetadata.md)

&nbsp;&nbsp;获取指定的统计数据，包括与统计信息值，指定的服务配置中的用户相关联的元数据的列表。
 
<a id="ID4EKC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EMC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[用户统计信息 Uri](atoc-reference-userstats.md)

   