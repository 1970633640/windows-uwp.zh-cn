---
title: PUT (/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type})
assetID: 40005e52-cd24-38ed-cfed-2c590cc2276f
permalink: en-us/docs/xboxlive/rest/uri-sessionssessionidscidssciddatapathandfilenametype-put.html
author: KevinAsgari
description: " PUT (/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: df924f8665424bf540eb1651cfa69737080588d5
ms.sourcegitcommit: 68fcac3288d5698a13dbcbd57f51b30592f24860
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2018
ms.locfileid: "4057468"
---
# <a name="put-sessionssessionidscidssciddatapathandfilenametype"></a>PUT (/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type})
将文件上传。 可在其中的数据和元数据发送一条消息，或作为其中的数据和元数据发送一系列的较小的块多块上载完整上载上传数据。 可以在一个消息发送仅小于 4 兆字节的文件。 多块上载不受支持的类型 json 数据。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EX)
  * [授权](#ID4EEB)
  * [可选的查询字符串参数](#ID4ERB)
  * [需的请求标头](#ID4ENE)
  * [可选的请求标头](#ID4EWF)
  * [请求正文](#ID4EZG)
  * [HTTP 状态代码](#ID4EEH)
  * [响应正文](#ID4EXEAC)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI 参数 
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| sessionId| 字符串| 若要查找会话的 ID。| 
| scid| guid| 要查找的服务配置 ID。| 
| pathAndFileName| 字符串| 若要访问该项目的路径和文件名称。 有效的字符 （达且包括最终正斜杠） 的路径部分包括 (A-Z) 的大写字母、 小写字母 (a-z)、 数字 (0-9)，下划线 (_)，并且正斜杠 （/）。路径部分可能为空。有效的字符的文件名称部分 （在最终的正斜杠后的所有内容） 包含大写字母 (A-Z)、 小写字母 (a-z)、 数字 (0-9)，下划线 (_)，句点 （.） 和连字符 （-）。 文件名称不能为空，以句号结尾或包含两个连续的句点。| 
| type| 字符串| 数据的格式。 可能的值为二进制文件或 json。| 
  
<a id="ID4EEB"></a>

 
## <a name="authorization"></a>授权 
 
请求必须包含有效的 Xbox LIVE 授权标头。 如果调用方不允许访问此资源，该服务将返回 403 禁止访问响应。 如果标头无效或不存在，该服务将返回 401 未经授权的响应。 
  
<a id="ID4ERB"></a>

 
## <a name="optional-query-string-parameters"></a>可选的查询字符串参数 
 
对于单个邮件上载，查询字符串参数是：
 
| 参数| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | 
| clientFileTime| DateTime| 日期/时间任何客户端上的文件的最后一次上载文件。| 
| 显示名称| 字符串| 应该向用户显示的文件的名称。| 
 
对于多块上载，查询字符串参数是：
 
| 参数| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| clientFileTime| DateTime| 日期/时间任何客户端上的文件的最后一次上载文件。| 
| 显示名称| 字符串| 应该向用户显示的文件的名称。| 
| ContinuationToken| 字符串| 从以前的上传请求的响应延续令牌。 如果这是第一个块，这不应指定。 | 
| finalBlock| Bool| 设置为 true 的文件的最后一个块。 设置为 false 时为所有其他块。| 
  
<a id="ID4ENE"></a>

 
## <a name="required-request-headers"></a>需的请求标头
 
| 标头| 值| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl 协定版本| 1| API 协定版本。| 
| 授权| XBL3.0 x = [哈希];[令牌]| STS 身份验证令牌。 STSTokenString 替换为由身份验证请求返回的令牌。 有关检索 STS 令牌和创建授权标头的其他信息，请参阅 Authenticating 和授权 Xbox LIVE 服务请求。| 
  
<a id="ID4EWF"></a>

 
## <a name="optional-request-headers"></a>可选的请求标头
 
| 标题| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| If-Match| 指定必须与要完成此操作的现有项目 ETag。| 
| If-None-Match| 指定 ETag，不匹配任何现有项目，以完成此操作。| 
  
<a id="ID4EZG"></a>

 
## <a name="request-body"></a>请求正文 
 
请求正文中包含上载文件的内容。 对于单个邮件上载，正文是文件的完整内容。 对于多块上载，正文是文件的查询字符串参数中指定的部分。 
  
<a id="ID4EEH"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码 
 
该服务返回的状态代码之一此部分中使用此方法对此资源进行的请求的响应。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| “确定” | 请求已成功。| 
| 201| 已创建 | 创建实体。| 
| 400| 错误请求 | 服务可能不理解格式不正确的请求。 通常是一个无效的参数。| 
| 401| 未授权 | 请求要求用户身份验证。| 
| 403| 已禁止 | 为用户或服务不允许该请求。| 
| 404| 找不到 | 找不到指定的资源。| 
| 406| 不允许 | 不支持资源版本。| 
| 408| 请求超时 | 请求所花的时间太长，才能完成。| 
| 500| 内部服务器错误 | 服务器时遇到意外的情况，无法完成请求。| 
| 503| 服务不可用 | 请求已被阻止，以秒为单位 （例如 5 秒更高版本） 客户端重试值后重试请求。| 
  
<a id="ID4EXEAC"></a>

 
## <a name="response-body"></a>响应正文 
 
如果在调用是一个多块请求成功，该服务将返回 continution 访问令牌传递与下一个块。
 
<a id="ID4EDFAC"></a>

 
### <a name="sample-response"></a>示例响应
 

```cpp
{
    "continuationToken":"abcd1234-1111-2222-3333-abcd12345678-1"
}
         
```

   
<a id="ID4EPFAC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ERFAC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘）  

[/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type}](uri-sessionssessionidscidssciddatapathandfilenametype.md)

   