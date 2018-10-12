---
title: GET (/users/{ownerId}/summary)
assetID: 754190c9-b15d-f34b-1dca-5c92f6f67d12
permalink: en-us/docs/xboxlive/rest/uri-usersowneridsummaryget.html
author: KevinAsgari
description: " GET (/users/{ownerId}/summary)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 73ba0cd060b3432de1cbb641a8991283974da192
ms.sourcegitcommit: 933e71a31989f8063b020746fdd16e9da94a44c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "4538307"
---
# <a name="get-usersowneridsummary"></a>GET (/users/{ownerId}/summary)
从调用方的角度来看，获取有关所有者的摘要数据。

  * [URI 参数](#ID4EQ)
  * [授权](#ID4E2)
  * [需的请求标头](#ID4EBC)
  * [可选的请求标头](#ID4EHD)
  * [请求正文](#ID4EXE)
  * [HTTP 状态代码](#ID4ECF)
  * [所需的响应标头](#ID4EZG)
  * [响应正文](#ID4EGAAC)

<a id="ID4EQ"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 描述|
| --- | --- | --- |
| ownerId| 字符串| 正在访问其资源的用户的标识符。 可能的值为"我"、 xuid({xuid}) 或 gt({gamertag})。 示例值： <code>me</code>， <code>xuid(2603643534573581)</code>， <code>gt(SomeGamertag)</code>|

<a id="ID4E2"></a>


## <a name="authorization"></a>授权

| <b>名称</b>| <b>类型</b>| <b>描述</b>|
| --- | --- | --- | --- | --- | --- |
| xuid| 64 位无符号的整数| 必需。 调用方的用户标识符。 示例值： 2533274790395904|

<a id="ID4EBC"></a>


## <a name="required-request-headers"></a>需的请求标头

| 标头| 类型| 描述|
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 授权| 字符串| 授权的数据。 这通常是加密的 XSTS 令牌。 示例值： <b>XBL3.0 x = [哈希]; [令牌]</b>。|

<a id="ID4EHD"></a>


## <a name="optional-request-headers"></a>可选的请求标头

| 标头| 类型| 描述|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| x xbl 协定版本| 字符串| 名称/的内部版本号此请求应定向到该服务。 验证在标头、 身份验证令牌等中的声明的有效性后仅为请求路由到该服务。示例值： 1|
| 接受| 字符串| 内容类型可接受。 所有回复将都对<code>application/json</code>。|

<a id="ID4EXE"></a>


## <a name="request-body"></a>请求正文

此请求的正文中不发送任何对象。

<a id="ID4ECF"></a>


## <a name="http-status-codes"></a>HTTP 状态代码

该服务返回的状态代码之一此部分中使用此方法对此资源所做的请求的响应。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。

| 代码| 原因短语| 描述|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 200| “确定”| 已成功检索会话。|
| 400| 错误请求| 用户 Id 的格式不正确。|
| 403| 已禁止| 无法分析 XUID 声明与授权标头中。|

<a id="ID4EZG"></a>


## <a name="required-response-headers"></a>所需的响应标头

| 标头| 类型| 描述|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Content-Length| 字符串| 正在发送响应中的字节数。 示例值： 232。|
| Content-Type| 字符串| 响应正文的 MIME 类型。 这必须是<b>应用程序/json</b>。|

<a id="ID4EGAAC"></a>


## <a name="response-body"></a>响应正文

请参阅[PersonSummary (JSON)](../../json/json-personsummary.md)。

<a id="ID4ESAAC"></a>


### <a name="sample-response"></a>示例响应


```cpp
{
    "targetFollowingCount": 87,
    "targetFollowerCount": 19,
    "isCallerFollowingTarget": true,
    "isTargetFollowingCaller": false,
    "hasCallerMarkedTargetAsFavorite": true,
    "hasCallerMarkedTargetAsKnown": true,
    "legacyFriendStatus": "None",
    "recentChangeCount": 5,
    "watermark": "5246775845000319351"
}

```


<a id="ID4E3AAC"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4E5AAC"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/users/{ownerId}/summary](uri-usersowneridsummary.md)
