---
title: MultiplayerSessionRequest (JSON)
assetID: 2e311c6d-3427-5a39-1989-06dc08483057
permalink: en-us/docs/xboxlive/rest/json-multiplayersessionrequest.html
author: KevinAsgari
description: " MultiplayerSessionRequest (JSON)"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 889db33ff81d3bf10743376118a0fab00ae44d8d
ms.sourcegitcommit: 753e0a7160a88830d9908b446ef0907cc71c64e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2018
ms.locfileid: "5745996"
---
# <a name="multiplayersessionrequest-json"></a>MultiplayerSessionRequest (JSON)
请求的 JSON 对象传递**MultiplayerSession**对象的操作。 
<a id="ID4EQ"></a>

  
 
MultiplayerSessionRequest JSON 对象具有以下规范。
 
| 成员| 类型| 说明| 
| --- | --- | --- | 
| 常量| object| 会话模板，以产生会话常量与合并的只读的设置。 | 
| 属性 | object | 合并到的会话属性更改。| 
| members.me | object| 常量和大量的属性，例如其顶级对应项。 任何 PUT 方法需要用户是会话的成员，并添加用户，如有必要。 "我"指定为 null，如果是从会话中删除发出请求的成员。 | 
| 成员 | object| 表示用户添加到会话中，从零开始的索引键控其他对象。 在请求中的成员数开始时始终具有 0，即使会话已包含成员。 成员将添加到会话中请求中的显示的顺序。 成员属性只能由用户属于其设置。 | 
| 服务器 | object| 关联的服务器参与者的设置的值，该值指示更新和添加到会话。 服务器指定为 null，如果是从会话中删除该服务器条目。 | 
  
<a id="ID4EZ"></a>

 
## <a name="request-structure"></a>请求的结构
 

```json
{
  "constants": { /* Property Bag */ },
  "properties": { /* Property Bag */ },
  "members": {
    // Requires a service principal. Existing members can be deleted by index.
    // Not available on large sessions.
    "5": null,

    // Reservation requests must start with zero. New users will get added in order to the end of the session's member list.
    // Large sessions don't support reservations.
    "reserve_0": {
      "constants": { /* Property Bag */ }
    },
    "reserve_1": {
      "constants": { /* Property Bag */ }
    },

    // Requires a user principal with a xuid claim. Can be 'null' to remove myself from the session.
    "me": {
      "constants": { /* Property Bag */ },
      "properties": { /* Property Bag */ },
    }
  },

  // Requires a server principal.
  "servers": {
    // Can be any name. The value can be 'null' to remove the server from the session.
    "name": {
      "constants": {  /* Property Bag */ },
      "properties": {  /* Property Bag */ }
    }
  }
}
```

  
<a id="ID4EAB"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ECB"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

  
<a id="ID4EMB"></a>

 
##### <a name="reference"></a>参考 

[MultiplayerSession (JSON)](json-multiplayersession.md)

 [PUT (/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}/sessions/{sessionName})](../uri/sessiondirectory/uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionssessionnameput.md)

   