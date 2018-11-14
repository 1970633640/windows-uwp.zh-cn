---
title: GET (/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json)
assetID: 229cabc6-3c5c-89e1-47e3-96a7f54094c9
permalink: en-us/docs/xboxlive/rest/uri-jsonusersxuidscidssciddatapathandfilenametype-get.html
author: KevinAsgari
description: " GET (/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json)"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: dcc2828487dc57f417608c7f80dde9ce650bbd51
ms.sourcegitcommit: bdc40b08cbcd46fc379feeda3c63204290e055af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2018
ms.locfileid: "6164427"
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
| scid| guid| 若要查找的服务配置 ID。| 
| pathAndFileName| 字符串| 若要访问该项目的路径和文件名。 有效的字符 （至当前阶段并包括最终正斜杠） 的路径部分包括 (A-Z) 的大写字母、 小写字母 (a-z)、 下划线 (_) 的数字 (0-9)，并且反斜杠 （/）。路径部分可能为空。有效的字符 （所有最终正斜杠后） 的文件名称部分包含大写字母 (A-Z)、 小写字母 (a-z)、 数字 (0-9)、 下划线 (_)，句点 （.） 和连字符 （-）。 文件名称不能为空，以句号结尾或包含两个连续句点。| 
  
<a id="ID4ECB"></a>

 
## <a name="authorization"></a>授权 
 
请求必须包含有效的 Xbox LIVE 授权标头。 如果调用方不允许访问此资源，该服务将返回 403 禁止访问响应。 如果标头是无效或不存在，该服务将返回 401 未经授权的响应。
  
<a id="ID4EPB"></a>

 
## <a name="optional-query-string-parameters"></a>可选的查询字符串参数 
 
因 blob 类型。 二进制文件 blob 不支持的查询参数。
 
| 参数| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | 
| 选择| 字符串| 仅 json 类型时才可用。 指定响应只应包含特定属性/值的 JSON，由此参数。 使用"点"（.） 来指定子属性，并放在方括号 ([和]) 来指定数组的索引。 例如，"array1 [4].prop2"指定"array1"数组的索引 4"prop2"属性。| 
  
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
| If-Match| 指定 ETag 符合必须要完成此操作的现有项目。| 
| If-None-Match| 指定 ETag，不匹配任何现有项目，以完成此操作。| 
| 范围| 指定要下载字节的范围。 遵循标准的 HTTP 范围标头格式。| 
  
<a id="ID4EDF"></a>

 
## <a name="request-body"></a>请求正文 
 
此请求的正文中不发送任何对象。
  
<a id="ID4EQF"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码 
 
此部分中使用此方法对此资源进行的请求的响应，该服务返回的状态代码之一。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
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
  
<a id="ID4EDDAC"></a>

 
## <a name="response-headers"></a>响应标头
 
| 标题| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| ETag| ETag 是资源的由对某一 URL 中找到的特定版本的 web 服务器分配的不透明标识符。 如果在该 URL 处的资源内容发生改变，被分配新功能和不同的 ETag。| 
| 内容区域| 如果这是部分下载，此标头指定下载的字节范围。| 
  
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

   