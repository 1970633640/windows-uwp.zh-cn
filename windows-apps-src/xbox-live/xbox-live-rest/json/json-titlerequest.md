---
title: TitleRequest (JSON)
assetID: 43aeb6f9-726d-9260-e2ba-f005ea688bf1
permalink: en-us/docs/xboxlive/rest/json-titlerequest.html
description: " TitleRequest (JSON)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: a90f42c2f830ba6f04f77a1acaba067a2746a062
ms.sourcegitcommit: 8921a9cc0dd3e5665345ae8eca7ab7aeb83ccc6f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "8877585"
---
# <a name="titlerequest-json"></a>TitleRequest (JSON)
有关游戏的请求。 
<a id="ID4EN"></a>

 
## <a name="titlerequest"></a>TitleRequest
 
TitleRequest 对象具有以下规范。
 
| 成员| 类型| 描述| 
| --- | --- | --- | 
| id| 32 位无符号的整数| 标题的标识符。| 
| 活动| [ActivityRequest](json-activityrequest.md)| 游戏内信息，包括丰富的状态和媒体信息，如果可用。| 
| 状态| 字符串| 无论用户是否处于活动状态。 若要将标记为非活动用户，需要此字段。 默认值为"活动"。| 
| 放置| 字符串| 游戏放置模式。 可能的值包括"完全"、"fill"，"贴靠"或"background"。 默认值为"完全"。| 
  
<a id="ID4EJC"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 

```json
{
  id:"12341234",
  placement:"snapped",
  state:"active",
  activity:
  {
    richPresence:
    {
      id:"playingMapWeapon",
      scid:"82b11353-08ba-48ca-9f1a-21627b189b0f"
    }
  }
}
    
```

  
<a id="ID4ESC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EUC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

  
<a id="ID4E5C"></a>

 
##### <a name="reference"></a>参考 

[POST (/users/xuid({xuid})/devices/current/titles/current)](../uri/presence/uri-usersxuiddevicescurrenttitlescurrentpost.md)

   