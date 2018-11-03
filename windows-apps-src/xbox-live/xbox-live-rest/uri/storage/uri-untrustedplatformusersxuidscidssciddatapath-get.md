---
title: GET (/untrustedplatform/users/xuid({xuid})/scids/{scid}/data/{path})
assetID: 7f1e511b-7c99-d5e9-7829-7777fd56fefc
permalink: en-us/docs/xboxlive/rest/uri-untrustedplatformusersxuidscidssciddatapath-get.html
author: KevinAsgari
description: " GET (/untrustedplatform/users/xuid({xuid})/scids/{scid}/data/{path})"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 4fc69717c737621e83fb1a34247aeb29ca31b95f
ms.sourcegitcommit: 144f5f127fc4fbd852f2f6780ef26054192d68fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2018
ms.locfileid: "5991523"
---
# <a name="get-untrustedplatformusersxuidxuidscidssciddatapath"></a>GET (/untrustedplatform/users/xuid({xuid})/scids/{scid}/data/{path})
列出了在指定的路径的文件信息。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EX)
  * [可选的查询字符串参数](#ID4ECB)
  * [授权](#ID4EWC)
  * [需的请求标头](#ID4EDD)
  * [请求正文](#ID4EME)
  * [HTTP 状态代码](#ID4EZE)
  * [响应正文](#ID4EMCAC)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 的玩家发出请求者。| 
| scid| guid| 若要查找的服务配置 ID。| 
| path| 字符串| 要返回的数据项路径。 获取返回所有匹配的目录和子目录。 有效字符包括 (A-Z) 的大写字母、 小写字母 (a-z)、 数字 (0-9)、 下划线 (_) 和正斜杠 （/）。 可能为空。 256 的最大长度。| 
  
<a id="ID4ECB"></a>

 
## <a name="optional-query-string-parameters"></a>可选的查询字符串参数 
 
| 参数| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | 
| skipItems| int| 返回在集合中，例如，N + 1 处开始的项跳过 N 项目。| 
| ContinuationToken| 字符串| 返回在给定的延续令牌启动的项。 如果两者都提供，continuationToken 参数优先于 skipItems。 换言之，如果存在 continuationToken 参数在 skipItems 参数将被忽略。| 
| maxItems| int| 要从该集合，这可以与 skipItems 和 continuationToken 返回项目的范围结合使用返回的项数的最大数量。 如果 maxItems 不存在，并且可能会返回少于 maxItems，即使尚未返回结果的最后一页服务可能会提供一个默认值。 | 
  
<a id="ID4EWC"></a>

 
## <a name="authorization"></a>授权 
 
请求必须包含有效的 Xbox LIVE 授权标头。 如果不允许调用方访问此资源，该服务将返回 403 禁止访问响应。 如果标头是无效或不存在，该服务将返回 401 未经授权的响应。 
  
<a id="ID4EDD"></a>

 
## <a name="required-request-headers"></a>需的请求标头
 
| 标头| 值| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl 协定版本| 1| API 协定版本。| 
| 授权| XBL3.0 x = [哈希];[令牌]| STS 身份验证令牌。 STSTokenString 替换为由身份验证请求返回的令牌。 有关检索 STS 令牌和创建授权标头的其他信息，请参阅 Authenticating 和授权 Xbox LIVE 服务请求。| 
  
<a id="ID4EME"></a>

 
## <a name="request-body"></a>请求正文 
 
此请求的正文中不发送任何对象。
  
<a id="ID4EZE"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码 
 
本部分中使用此方法对此资源区域设置发出请求的响应，该服务返回的状态代码之一。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| “确定” | 请求已成功。| 
| 201| 已创建 | 已创建的实体。| 
| 400| 错误请求 | 服务可能不理解的格式不正确的请求。 通常参数无效。| 
| 401| 未授权 | 请求要求用户身份验证。| 
| 403| 已禁止 | 为用户或服务不允许该请求。| 
| 404| 找不到 | 找不到指定的资源。| 
| 406| 不允许 | 资源版本不受支持。| 
| 408| 请求超时 | 请求所花的时间太长，才能完成。| 
| 500| 内部服务器错误 | 服务器时遇到意外的情况，执行此请求将阻止它。| 
| 503| 服务不可用 | 请求已被阻止，以秒为单位 （例如 5 秒更高版本） 客户端重试值后重试请求。| 
  
<a id="ID4EMCAC"></a>

 
## <a name="response-body"></a>响应正文
 
如果在调用成功，该服务将返回[TitleBlob](../../json/json-titleblob.md)对象的数组。 
 
<a id="ID4E1CAC"></a>

 
### <a name="sample-response"></a>示例响应
 

```cpp
{
"blobs":
[
    {
        "fileName":"foo\bar\blob.txt,binary",
        "clientFileTime":"2012-01-01T01:02:03.1234567Z",
        "displayName":"Friendly Name",
        "size":12,
        "etag":"0x8CEB3E4F8F3A5BF"
    },
    {
        "fileName":"foo\bar\blob2.txt,binary",
        "displayName":"Blob 2",
        "size":4,
        "etag":"0x8CEB3FE57F1A142"
    },
    {
        "fileName":"foo\jsonblob.txt,json",
        "size":15,
        "etag":"0x8CEB40152B4A6F8"
    }
],
"pagingInfo":
    {
        "continuationToken":"54",
    }
}
         
```

   
<a id="ID4EGDAC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EIDAC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘）  

[/untrustedplatform/users/xuid({xuid})/scids/{scid}/data/{path}](uri-untrustedplatformusersxuidscidssciddatapath.md)

  
<a id="ID4EUDAC"></a>

 
##### <a name="reference--titleblob-jsonjsonjson-titleblobmd"></a>引用[TitleBlob (JSON)](../../json/json-titleblob.md)

 [PagingInfo (JSON)](../../json/json-paginginfo.md)

   