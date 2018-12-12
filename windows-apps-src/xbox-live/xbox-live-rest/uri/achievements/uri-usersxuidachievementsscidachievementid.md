---
title: /users/xuid({xuid})/achievements/{scid}/{achievementid}
assetID: 656a6d63-1a11-b0a5-63d2-2b010abd62e7
permalink: en-us/docs/xboxlive/rest/uri-usersxuidachievementsscidachievementid.html
description: " /users/xuid({xuid})/achievements/{scid}/{achievementid}"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 00c577f60b67f15f75c47b5e737ca12819695110
ms.sourcegitcommit: 49d58bc66c1c9f2a4f81473bcb25af79e2b1088d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "8918762"
---
# <a name="usersxuidxuidachievementsscidachievementid"></a>/users/xuid({xuid})/achievements/{scid}/{achievementid}
返回有关成就，包括其配置的元数据和特定于用户的数据的详细信息。 

> [!NOTE] 
> 仅支持平台。 

 
这些 Uri 的域是`achievements.xboxlive.com`。
 
  * [URI 参数](#ID4E2)
 
<a id="ID4E2"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | --- | 
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 所访问的资源的用户。 必须匹配的身份验证的用户的 XUID。| 
| scid| GUID| 其成就所访问的服务配置的唯一标识符。| 
| achievementid| 32 位无符号的整数| 正在访问的成就 （中指定的 SCID) 的唯一标识符。| 
  
<a id="ID4EMC"></a>

 
## <a name="valid-methods"></a>有效的方法

[GET (/users/xuid({xuid})/achievements/{scid}/{achievementid})](uri-usersxuidachievementsscidachievementidget.md)

&nbsp;&nbsp;获取在成就的详细信息。
 
<a id="ID4EWC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EYC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[成就 URI](atoc-reference-achievementsv2.md)

   