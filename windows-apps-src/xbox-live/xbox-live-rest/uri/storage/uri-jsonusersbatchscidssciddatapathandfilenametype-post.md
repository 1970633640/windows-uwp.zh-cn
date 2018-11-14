---
title: POST (/json/users/batch/scids/{scid}/data/{pathAndFileName},json)
assetID: fb4cff17-2721-89c5-6646-5ab76952b411
permalink: en-us/docs/xboxlive/rest/uri-jsonusersbatchscidssciddatapathandfilenametype-post.html
author: KevinAsgari
description: " POST (/json/users/batch/scids/{scid}/data/{pathAndFileName},json)"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 592467707c67e82531af31c52ba38fbfb04080db
ms.sourcegitcommit: f2c9a050a9137a473f28b613968d5782866142c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2018
ms.locfileid: "6257374"
---
# <a name="post-jsonusersbatchscidssciddatapathandfilenamejson"></a>POST (/json/users/batch/scids/{scid}/data/{pathAndFileName},json)
将多个文件下载从多个用户具有相同的文件名。 请求 URI 由确定要下载的文件。 请求正文中的包含的用户的 Xuid 列表以下载其文件。 响应正文将多个部分的 MIME 消息中，然后使用表示的特定用户的组其自己的标头文件的每个部分。 很可能是成功和失败的组合的响应的部分。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EX)
  * [授权](#ID4ECB)
  * [请求正文](#ID4EPB)
  * [HTTP 状态代码](#ID4E3C)
  * [所需的响应标头](#ID4EPAAC)
  * [可选的响应标头](#ID4ESBAC)
  * [响应正文](#ID4E3CAC)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| scid| guid| 若要查找的服务配置 ID。| 
| pathAndFileName| 字符串| 若要访问该项目的路径和文件名。 有效的字符 （至当前阶段并包括最终正斜杠） 的路径部分包括 (A-Z) 的大写字母、 小写字母 (a-z)、 下划线 (_) 的数字 (0-9)，并且反斜杠 （/）。路径部分可能为空。有效的字符 （所有最终正斜杠后） 的文件名称部分包含大写字母 (A-Z)、 小写字母 (a-z)、 数字 (0-9)、 下划线 (_)，句点 （.） 和连字符 （-）。 文件名称不能为空，以句号结尾或包含两个连续句点。| 
  
<a id="ID4ECB"></a>

 
## <a name="authorization"></a>授权 
 
请求必须包含有效的 Xbox LIVE 授权标头。 如果调用方不允许访问此资源，该服务将返回 403 禁止访问响应。 如果标头是无效或不存在，该服务将返回 401 未经授权的响应。 
  
<a id="ID4EPB"></a>

 
## <a name="request-body"></a>请求正文
 
| 属性| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | 
| xuid| 未签名的 64 位整数数组| 要下载的文件的 Xuid 列表。| 
 
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
 
此部分中使用此方法对此资源进行的请求的响应，该服务返回的状态代码之一。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| “确定” | 请求已成功。| 
| 201| 已创建 | 创建实体。| 
| 400| 错误请求 | 服务可能不理解格式不正确的请求。 通常无效参数。| 
| 401| 未授权 | 请求要求用户身份验证。| 
| 403| 已禁止 | 为用户或服务不允许该请求。| 
| 404| 找不到 | 找不到指定的资源。| 
| 406| 不允许 | 不支持资源版本。| 
| 408| 请求超时 | 请求时间太长，才能完成。| 
| 500| 内部服务器错误 | 服务器时遇到意外的情况，执行此请求将阻止它。| 
| 503| 服务不可用 | 请求已被阻止，以秒为单位 （例如 5 秒更高版本） 的客户端重试值后重试请求。| 
  
<a id="ID4EPAAC"></a>

 
## <a name="required-response-headers"></a>所需的响应标头
 
| 标题| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 内容处置| 介绍了部分的内容。 在标头的"名称"和"filename"部分是该文件属于用户的 XUID。| 
| HttpStatusCode| HTTP 状态代码与检索此特定文件。| 
  
<a id="ID4ESBAC"></a>

 
## <a name="optional-response-headers"></a>可选的响应标头
 
| 标题| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| ETag| ETag 是资源的由对某一 URL 中找到的特定版本的 web 服务器分配的不透明标识符。 如果在该 URL 处的资源内容发生改变，被分配新功能和不同的 ETag。| 
| Content-Type| 如果成功检索文件，这是文件的内容类型。| 
| 内容区域| 如果该文件已成功检索且部分下载，这是在响应中包含的文件字节范围。 | 
  
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

[/json/users/batch/scids/{scid}/data/{pathAndFileName},json](uri-jsonusersbatchscidssciddatapathandfilenametype.md)

   