---
title: User (JSON)
assetID: dbc733e4-0348-0e3d-1f55-17b465e599d6
permalink: en-us/docs/xboxlive/rest/json-user.html
description: " User (JSON)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 5c1b3a34ef329696d51e615dd79d57783a132d05
ms.sourcegitcommit: d7613c791107f74b6a3dc12a372d9de916c0454b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2018
ms.locfileid: "8744932"
---
# <a name="user-json"></a>User (JSON)
包含用户排行榜数据。 
<a id="ID4EN"></a>

 
## <a name="user"></a>用户
 
用户对象具有以下规范。
 
| 成员| 类型| 描述| 
| --- | --- | --- | 
| 玩家代号| 字符串| （最多 15 个字符） 的玩家的玩家代号。 在确定玩家时，客户端应在 UI 中使用此值。| 
| 排名| 32 位有符号整数| 对相对于请求排行榜数据的用户的用户进行分级。| 
| rating| 字符串| 该用户的评分。| 
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 的用户。| 
  
<a id="ID4EMC"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 

```json
{ 
   "gamertag":"TrueBlue402",
   "rank":2,
   "rating":"2:19:21.17",
   "xuid":1234567890123456 
}
    
```

  
<a id="ID4EVC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EXC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

   