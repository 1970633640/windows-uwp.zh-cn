---
title: GET (/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json)
assetID: 229cabc6-3c5c-89e1-47e3-96a7f54094c9
permalink: en-us/docs/xboxlive/rest/uri-jsonusersxuidscidssciddatapathandfilenametype-get.html
author: KevinAsgari
description: " GET (/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: ef854d2ed803b82197bee740ceb284c6f789c883
ms.sourcegitcommit: 4f6dc806229a8226894c55ceb6d6eab391ec8ab6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2018
ms.locfileid: "4092270"
---
# <a name="get-jsonusersxuidxuidscidssciddatapathandfilenamejson"></a>GET (/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json)
下载文件。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EX)
  * [授权](#ID4ECB)
  * [可选的查询字符串参数](#ID4EPB)
  * [需的请求标头](#ID4EQC)
  * [可选的请求标头](#ID4EZD)
  * [请求正文](#ID4EDF)
  * [HTTP 状态代码](#ID4EQF)
  * [响应标头](#ID4EDDAC)
  * [响应正文](#ID4EGEAC)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 的玩家用户发出请求。| 
| scid| guid| 要查找的服务配置 ID。| 
| pathAndFileName| 字符串| 若要访问该项目的路径和文件名称。 有效的字符 （达且包括最终正斜杠） 的路径部分包括 (A-Z) 的大写字母、 小写字母 (a-z)、 数字 (0-9)，下划线 (_)，并且正斜杠 （/）。路径部分可能为空。有效的字符的文件名称部分 （在最终的正斜杠后的所有内容） 包含大写字母 (A-Z)、 小写字母 (a-z)、 数字 (0-9)，下划线 (_)，句点 （.） 和连字符 （-）。 文件名称不能为空，以句号结尾或包含两个连续的句点。| 
  
<a id="ID4ECB"></a>

 
## <a name="authorization"></a>授权 
 
请求必须包含有效的 Xbox LIVE 授权标头。 如果调用方不允许访问此资源，该服务将返回 403 禁止访问响应。 如果标头无效或不存在，该服务将返回 401 未经授权的响应。
  
<a id="ID4EPB"></a>

 
## <a name="optional-query-string-parameters"></a>可选的查询字符串参数 
 
因 blob 类型。 二进制文件 blob 不支持查询参数。
 
| 参数| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | 
| 选择| 字符串| 仅 json 类型时才可用。 指定响应只应包含某个属性/值的 JSON，由此参数。 使用"点"（.） 来指定子属性，并放在方括号 ([和]) 来指定数组索引。 例如，"array1 [4].prop2"指定"array1"数组索引 4"prop2"属性。| 
  
<a id="ID4EQC"></a>

 
## <a name="required-request-headers"></a>需的请求标头
 
| 标头| 值| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl 协定版本| 1| API 协定版本。| 
| 授权| XBL3.0 x = [哈希];[令牌]| STS 身份验证令牌。 STSTokenString 替换为由身份验证请求返回的令牌。 有关检索 STS 令牌和创建授权标头的其他信息，请参阅 Authenticating 和授权 Xbox LIVE 服务请求。| 
  
<a id="ID4EZD"></a>

 
## <a name="optional-request-headers"></a>可选的请求标头
 
| 标题| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| If-Match| 指定必须与要完成此操作的现有项目 ETag。| 
| If-None-Match| 指定 ETag，不匹配任何现有项目，以完成此操作。| 
| 范围| 指定要下载字节的范围。 遵循标准的 HTTP 范围标头格式。| 
  
<a id="ID4EDF"></a>

 
## <a name="request-body"></a>请求正文 
 
此请求的正文中不发送任何对象。
  
<a id="ID4EQF"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码 
 
该服务返回的状态代码之一此部分中使用此方法对此资源进行的请求的响应。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
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
  
<a id="ID4EDDAC"></a>

 
## <a name="response-headers"></a>响应标头
 
| 标题| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| ETag| ETag 是资源的由对某一 URL 中找到的特定版本的 web 服务器分配的不透明标识符。 如果在该 URL 处的资源内容发生改变，新功能和不同的 ETag 分配。| 
| 内容区域| 如果这部分下载，此标头指定下载的字节范围。| 
  
<a id="ID4EGEAC"></a>

 
## <a name="response-body"></a>响应正文
 
如果在调用成功，该服务将返回文件的内容。
  
<a id="ID4EREAC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ETEAC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘）  

[/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json](uri-jsonusersxuidscidssciddatapathandfilenametype.md)

  
<a id="ID4E6EAC"></a>

 
##### <a name="reference--titleblob-jsonjsonjson-titleblobmd"></a>引用[TitleBlob (JSON)](../../json/json-titleblob.md)

   