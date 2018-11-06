---
title: DELETE (/users/xuid({xuid})/inbox/{messageId})
assetID: c54eede3-3e3b-2cbe-1be9-8bf3a48171bc
permalink: en-us/docs/xboxlive/rest/uri-usersxuidinboxmessageiddelete.html
author: KevinAsgari
description: " DELETE (/users/xuid({xuid})/inbox/{messageId})"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 9d550147fe18a0233fd4f0a62ccb2826ef2a5c03
ms.sourcegitcommit: e814a13978f33654d8e995584f4b047cb53e0aef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "6026881"
---
# <a name="delete-usersxuidxuidinboxmessageid"></a>DELETE (/users/xuid({xuid})/inbox/{messageId})
删除用户的收件箱中用户消息。 这些 Uri 的域是`msg.xboxlive.com`。
 
  * [备注](#ID4EV)
  * [URI 参数](#ID4ECB)
  * [授权](#ID4EPB)
  * [请求正文](#ID4E1B)
  * [HTTP 状态代码](#ID4EHC)
  * [JavaScript 对象表示法 (JSON) 响应](#ID4EAE)
  * [在资源的隐私设置的效果](#ID4EYF)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>备注 
 
删除操作是幂等。
 
此 API 支持仅内容类型是"application/json"，其中每个调用的 HTTP 标头中必需的。 
  
<a id="ID4ECB"></a>

 
## <a name="uri-parameters"></a>URI 参数 
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| xuid | 64 位无符号的整数 | Xbox 用户 ID (XUID) 发出请求的玩家。 | 
| 邮件 Id | string [50] | 要检索或删除该消息的 ID。 | 
  
<a id="ID4EPB"></a>

 
## <a name="authorization"></a>授权 
 
你必须拥有自己声明要删除的用户的消息的用户。
  
<a id="ID4E1B"></a>

 
## <a name="request-body"></a>请求正文 
 
此请求的正文中不发送任何对象。
  
<a id="ID4EHC"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码 
 
本部分中使用此方法对此资源区域设置发出请求的响应，该服务返回的状态代码之一。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 说明| 
| --- | --- | --- | --- | --- | 
| 204| 成功。| 
| 403| 不能转换 XUID 或找不到有效的 XUID 声明。| 
| 404| URI 中的消息 ID 不能将得到解析或 XUID 是 URI 中丢失。| 
| 500| 常规的服务器端错误。| 
  
<a id="ID4EAE"></a>

 
## <a name="javascript-object-notation-json-response"></a>JavaScript 对象表示法 (JSON) 响应 
 
发生错误，该服务可能会返回一个服务器对象，其中可能包含从该服务的环境的值。
 
| 属性| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | 
| 错误码| 字符串| 指示错误的来源。| 
| errorCode| int| 与 （可以为 null） 的错误相关联的数字代码。| 
| errorMessage| 字符串| 如果配置为显示详细信息的错误的详细信息。| 
  
<a id="ID4EYF"></a>

 
## <a name="effect-of-privacy-settings-on-resource"></a>在资源的隐私设置的效果 
 
仅可以删除自己用户的消息。 
  
<a id="ID4EDG"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EFG"></a>

 
##### <a name="parent"></a>Parent 的子磁盘）  

[/users/xuid({xuid})/inbox](uri-usersxuidinbox.md)

  
<a id="ID4ETG"></a>

 
##### <a name="reference--standard-http-status-codesadditionalhttpstatuscodesmd"></a>引用[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)

   