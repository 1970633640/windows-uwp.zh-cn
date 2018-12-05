---
title: MatchTicket (JSON)
assetID: 12617677-47f2-e517-af53-5ab9687eea2a
permalink: en-us/docs/xboxlive/rest/json-matchticket.html
description: " MatchTicket (JSON)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 4bc638dfe7735856295ed92f35e244213be7bc1e
ms.sourcegitcommit: d7613c791107f74b6a3dc12a372d9de916c0454b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2018
ms.locfileid: "8750492"
---
# <a name="matchticket-json"></a>MatchTicket (JSON)
表示玩家用于查找其他玩家通过多人游戏会话目录 (MPSD) 的匹配票证的 JSON 对象。 
<a id="ID4EN"></a>

  
 
MatchTicket JSON 对象具有以下规范。
 
| 成员| 类型| 描述| 
| --- | --- | --- | 
| serviceConfig| GUID| 服务配置标识符 (SCID) 的会话。| 
| hopperName| 字符串| 应在其中放置此票证的漏斗的名称。| 
| giveUpDuration| 32 位有符号整数| 最大的等待时间 （不可或缺的秒数）。| 
| preserveSession| 枚举| 指示会话是否必须为以匹配到会话重复使用的值。 可能的值为"始终"，或"从不"。 | 
| ticketSessionRef| MultiplayerSessionReference| <b>MultiplayerSessionReference</b>会话的玩家或组当前正在播放的对象。 此成员始终是必需的。 | 
| ticketAttributes| 对象数组| 玩家的用户提供的属性和有关票证的值的集合。| 
| 玩家| 对象数组| 玩家对象的集合，每个都有一个属性包的用户提供的属性。 | 
  
<a id="ID4EW"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 

```json
{
        "serviceConfig": "07617C5B-3423-4505-B6C6-10A16E1E5DDB",
        "hopperName": "TestHopper",
        "giveUpDuration": 10,
        "preserveSession": "never",
        "ticketSessionRef": {
        "scid": "AFFEABDF-0000-0000-0000-000000000001",
        "templateName": "TestTemplate",
        "sessionName": "5E551041-0000-0000-0000-000000000001"
    },
    "ticketAttributes": {
        "desiredMap": "Test Map",
        "desiredGameType": "Test GameType"
    },
    "players": [
        {
            "xuid": 123412345123,
            "playerAttributes": {
                "skill": 5,
                "ageRange": "teenager"
            }
        },
        {
          "xuid": 123412345124,
          "playerAttributes": {
              "skill": 15,
              "ageRange": "twenty-something"
          }
        }
      ]
    }
  
    
```

  
<a id="ID4EEB"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EGB"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

   