---
title: POST (/untrustedplatform/users/batch/scids/{scid}/data/{pathAndFileName},{type})
assetID: 6e28d794-b5c6-0b70-6d46-957e8ae6e8ac
permalink: en-us/docs/xboxlive/rest/uri-untrustedplatformusersbatchscidssciddatapathandfilenametype-post.html
author: KevinAsgari
description: " POST (/untrustedplatform/users/batch/scids/{scid}/data/{pathAndFileName},{type})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 17d037e05e7d0817d51d2c63beaf00ae91d10567
ms.sourcegitcommit: fbdc9372dea898a01c7686be54bea47125bab6c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2018
ms.locfileid: "4419337"
---
# <a name="post-untrustedplatformusersbatchscidssciddatapathandfilenametype"></a>POST (/untrustedplatform/users/batch/scids/{scid}/data/{pathAndFileName},{type})
将多个文件下载从多个用户具有相同的文件名。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EX)
  * [授权](#ID4ECB)
  * [请求正文](#ID4EPB)
  * [HTTP 状态代码](#ID4E3C)
  * [所需的响应标头](#ID4EPAAC)
  * [可选的响应标头](#ID4ESBAC)
  * [响应正文](#ID4E3CAC)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | 
| scid| guid| 若要查找的服务配置 ID。| 
| pathAndFileName| 字符串| 若要访问该项目的路径和文件名称。 有效的字符 （达且包括最终正斜杠） 的路径部分包括 (A-Z) 的大写字母、 小写字母 (a-z)、 数字 (0-9)，下划线 (_) 和正斜杠 （/）。路径部分可能为空。有效的字符的文件名称部分 （最终正斜杠后面的所有内容） 包含大写字母 (A-Z)、 小写字母 (a-z)、 数字 (0-9)，下划线 (_)，句点 （.） 和连字符 （-）。 文件名称不能为空，以句号结尾或包含两个连续句点。| 
| type| 字符串| 数据的格式。 可能的值为二进制文件的 json。| 
  
<a id="ID4ECB"></a>

 
## <a name="authorization"></a>授权 
 
请求必须包含有效的 Xbox LIVE 授权标头。 如果调用方不允许访问此资源，该服务将返回 403 禁止访问响应。 如果在标头丢失或无效，该服务将返回 401 未经授权的响应。 
  
<a id="ID4EPB"></a>

 
## <a name="request-body"></a>请求正文
 
| 属性| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | 
| xuid| 未签名的 64 位整数数组| 要下载文件的 Xuid 列表。| 
 
<a id="ID4EQC"></a>

 
### <a name="sample-request"></a>示例请求
 

```cpp
{
    "xuids" : 
    [
      12345,
      45678,
      78901
    ]
}
      
```

   
<a id="ID4E3C"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码 
 
该服务返回的状态代码之一此部分中使用此方法对此资源所做的请求的响应。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| “确定” | 请求已成功。| 
| 201| 已创建 | 创建实体。| 
| 400| 错误请求 | 服务可能不理解格式不正确的请求。 通常无效参数。| 
| 401| 未授权 | 请求要求用户身份验证。| 
| 403| 已禁止 | 为用户或服务不允许该请求。| 
| 404| 找不到 | 找不到指定的资源。| 
| 406| 不允许 | 不支持资源版本。| 
| 408| 请求超时 | 请求所花的时间太长，才能完成。| 
| 500| 内部服务器错误 | 服务器时遇到意外的情况，执行此请求将阻止它。| 
| 503| 服务不可用 | 请求已被阻止，以秒为单位 （例如 5 秒更高版本） 的客户端重试值后重试请求。| 
  
<a id="ID4EPAAC"></a>

 
## <a name="required-response-headers"></a>所需的响应标头
 
| 标题| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 内容处置| 介绍了部分的内容。 在标头的"名称"和"filename"部分是该文件属于用户的 XUID。| 
| HttpStatusCode| HTTP 状态代码与检索此特定文件相关。| 
  
<a id="ID4ESBAC"></a>

 
## <a name="optional-response-headers"></a>可选的响应标头
 
| 标题| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| ETag| ETag 是由对某一 URL 找到资源的特定版本的 web 服务器分配一个不透明标识符。 如果在该 URL 处的资源内容发生改变，被分配新功能和不同的 ETag。| 
| Content-Type| 如果成功检索文件，这是文件的内容类型。| 
| 内容区域| 如果文件已成功检索，并且是部分下载，这是在响应中包含的文件的字节范围。 | 
  
<a id="ID4E3CAC"></a>

 
## <a name="response-body"></a>响应正文
 
如果在调用成功，该服务将多部分响应中返回所请求文件的内容。
 
<a id="ID4EGDAC"></a>

 
### <a name="sample-response"></a>示例响应 
 

```cpp
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Content-Type: multipart/form-data; boundary=c0a9fd75-d036-4294-8b7b-85fea15a31bb

228
--c0a9fd75-d036-4294-8b7b-85fea15a31bb
Content-Disposition: binary; name="123"; filename="123"
HttpStatusCode: 200
ETag: 0x8CF327717411C31
Content-Type: application/octet-stream

asdf123
--c0a9fd75-d036-4294-8b7b-85fea15a31bb
Content-Disposition: binary; name="456"; filename="456"
HttpStatusCode: 200
ETag: 0x8CF32771E954BB8
Content-Type: application/octet-stream

asdf456
--c0a9fd75-d036-4294-8b7b-85fea15a31bb
Content-Disposition: binary; name="789"; filename="789"
HttpStatusCode: 404


--c0a9fd75-d036-4294-8b7b-85fea15a31bb--

0

```

   
<a id="ID4EUDAC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EWDAC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[/untrustedplatform/users/batch/scids/{scid}/data/{pathAndFileName},{type}](uri-untrustedplatformusersbatchscidssciddatapathandfilenametype.md)

   