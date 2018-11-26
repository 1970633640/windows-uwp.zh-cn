---
title: GET (/json/users/xuid({xuid})/scids/{scid})
assetID: a015fb75-f072-ee9b-000b-e6e93beed903
permalink: en-us/docs/xboxlive/rest/uri-jsonusersxuidscidsscid-get.html
description: " GET (/json/users/xuid({xuid})/scids/{scid})"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 77cb9089eda1cc5efd6fac321ad2162250dcb824
ms.sourcegitcommit: 681c70f964210ab49ac5d06357ae96505bb78741
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2018
ms.locfileid: "7720046"
---
# <a name="get-jsonusersxuidxuidscidsscid"></a>GET (/json/users/xuid({xuid})/scids/{scid})
检索此存储类型的配额信息。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EX)
  * [授权](#ID4ECB)
  * [需的请求标头](#ID4ENB)
  * [请求正文](#ID4EWC)
  * [HTTP 状态代码](#ID4EBD)
  * [响应正文](#ID4EUAAC)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | 
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 的玩家用户发出请求。| 
| scid| guid| 若要查找的服务配置 ID。| 
  
<a id="ID4ECB"></a>

 
## <a name="authorization"></a>授权
 
请求必须包含有效的 Xbox LIVE 授权标头。 如果调用方不允许访问此资源，该服务将返回 403 禁止访问响应。 如果在标头丢失或无效，该服务将返回 401 未经授权的响应。 
  
<a id="ID4ENB"></a>

 
## <a name="required-request-headers"></a>需的请求标头
 
| 标头| 值| 描述| 
| --- | --- | --- | --- | --- | --- | 
| x xbl 协定版本| 1| API 协定版本。| 
| 授权| XBL3.0 x = [哈希];[令牌]| STS 身份验证令牌。 STSTokenString 替换为由身份验证请求返回的令牌。 有关检索 STS 令牌和创建授权标头的其他信息，请参阅 Authenticating 和授权 Xbox LIVE 服务请求。| 
  
<a id="ID4EWC"></a>

 
## <a name="request-body"></a>请求正文
 
此请求的正文中不发送任何对象。
  
<a id="ID4EBD"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码 
 
此部分中使用此方法对此资源区域设置发出请求的响应，该服务返回的状态代码之一。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| “确定” | 请求已成功。| 
| 201| 已创建 | 创建实体。| 
| 400| 错误请求 | 服务可能不理解格式不正确的请求。 通常参数无效。| 
| 401| 未授权 | 请求要求用户身份验证。| 
| 403| 已禁止 | 为用户或服务不允许该请求。| 
| 404| 找不到 | 找不到指定的资源。| 
| 406| 不允许 | 不支持资源版本。| 
| 408| 请求超时 | 请求所花的时间太长，才能完成。| 
| 500| 内部服务器错误 | 服务器时遇到意外的情况，执行此请求将阻止它。| 
| 503| 服务不可用 | 请求已被阻止，以秒为单位 （例如 5 秒更高版本） 的客户端重试值后重试请求。| 
  
<a id="ID4EUAAC"></a>

 
## <a name="response-body"></a>响应正文
 
如果在调用成功，该服务将返回一个[quotaInfo](../../json/json-quota.md)对象。 
 
<a id="ID4ECBAC"></a>

 
### <a name="sample-response"></a>示例响应
 

```cpp
{
  "quotaInfo" :
  {
    "usedBytes" : 619,
    "quotaBytes" : 16777216
  }
}
         
```

   
<a id="ID4EOBAC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EQBAC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[/json/users/xuid({xuid})/scids/{scid}](uri-jsonusersxuidscidsscid.md)

  
<a id="ID4E1BAC"></a>

 
##### <a name="reference"></a>参考 

[quotaInfo (JSON)](../../json/json-quota.md)

   