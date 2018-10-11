---
title: /users/xuid({xuid})/inbox
assetID: 352740c6-42e2-0000-495d-bf384dc3e941
permalink: en-us/docs/xboxlive/rest/uri-usersxuidinbox.html
author: KevinAsgari
description: " /users/xuid({xuid})/inbox"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 944b2c9f0e5758444295ef9ec189d84728a3845d
ms.sourcegitcommit: 933e71a31989f8063b020746fdd16e9da94a44c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "4528832"
---
# <a name="usersxuidxuidinbox"></a>/users/xuid({xuid})/inbox
提供访问用户的 Xbox LIVE 服务的邮件收件箱。 这些 Uri 的域是`msg.xboxlive.com`。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数 
 
| 参数| 类型| 描述| 
| --- | --- | --- | 
| xuid | 64 位无符号的整数 | Xbox 用户 ID (XUID) 发出请求的玩家。 | 
| 邮件 Id | 字符串 [50] | 要检索或删除该消息的 ID。 | 
  
<a id="ID4EDC"></a>

 
## <a name="valid-methods"></a>有效的方法 

[GET (/users/xuid({xuid})/inbox)](uri-usersxuidinboxget.md)

&nbsp;&nbsp;从服务检索指定的数量的用户消息摘要。 

[DELETE (/users/xuid({xuid})/inbox/{messageId})](uri-usersxuidinboxmessageiddelete.md)

&nbsp;&nbsp;删除用户的收件箱中用户消息。

[GET (/users/xuid({xuid})/inbox/{messageId})](uri-usersxuidinboxmessageidget.md)

&nbsp;&nbsp;检索特定用户消息，将其标记为已在服务上的读的详细的消息文本。 
 
<a id="ID4EVC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EXC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘）  

[用户 URI](atoc-reference-users.md)

   