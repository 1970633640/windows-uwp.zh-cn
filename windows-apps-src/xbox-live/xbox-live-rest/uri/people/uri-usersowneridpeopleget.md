---
title: 获取 (/users/ {ownerId} / 个人)
assetID: c948d031-ec19-7571-31ef-23cb9c5ebfaf
permalink: en-us/docs/xboxlive/rest/uri-usersowneridpeopleget.html
author: KevinAsgari
description: " 获取 (/users/ {ownerId} / 个人)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: d08a8ff9e04b255944128ffc1cd1c0b101180d8f
ms.sourcegitcommit: 2a63ee6770413bc35ace09b14f56b60007be7433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3935323"
---
# <a name="get-usersowneridpeople"></a>获取 (/users/ {ownerId} / 个人)
获取调用方的用户集合。
这些 Uri 的域是`social.xboxlive.com`。

  * [备注](#ID4EV)
  * [URI 参数](#ID4E5)
  * [查询字符串参数](#ID4EJB)
  * [授权](#ID4ERD)
  * [需的请求标头](#ID4EZE)
  * [可选的请求标头](#ID4EYF)
  * [请求正文](#ID4E5G)
  * [HTTP 状态代码](#ID4EJH)
  * [所需的响应标头](#ID4EBBAC)
  * [响应正文](#ID4ENCAC)

<a id="ID4EV"></a>


## <a name="remarks"></a>备注

获取操作不会修改任何资源，因此如果执行一次或多次，这将产生相同的结果。

<a id="ID4E5"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 说明|
| --- | --- | --- |
| ownerId| 字符串| 正在访问其资源的用户的标识符。 必须匹配身份验证的用户。 可能的值为"me"、 xuid({xuid}) 或 gt({gamertag})。|

<a id="ID4EJB"></a>


## <a name="query-string-parameters"></a>查询字符串参数

| 参数| 类型| 说明|
| --- | --- | --- | --- | --- | --- |
| 视图| 字符串| 返回与视图关联的用户。 默认值是"全部"。 可能的值为： <ul><li><b>所有</b>-返回用户联系人列表中的所有人。 这是默认值。</li><li><b>最喜爱</b>的用户的人脉列表拥有最喜爱的人物属性返回的所有人。</li><li><b>LegacyXboxLiveFriends</b> -返回用户的人脉列表中的用户也是旧 Xbox LIVE 好友的所有人。</li></br>**注意：** 如果调用用户位于不同所属的用户，支持仅**所有**的值。|
| startIndex| 32 位无符号的整数| 返回给定索引处开始的项目。  
| maxItems| 32 位无符号的整数| 用户从开始菜单索引的集合返回的最大数量。 如果<b>maxItems</b>不存在，并且可能会返回<b>maxItems</b>少于 （即使尚未返回结果的最后一页），该服务可能会提供一个默认值。|

<a id="ID4ERD"></a>


## <a name="authorization"></a>授权

| 类型| 必需| 描述| 如果缺少的响应|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| XUID| 是| 调用方具有用户的 Xbox 用户 ID (XUID)。| 401 未授权|

<a id="ID4EZE"></a>


## <a name="required-request-headers"></a>需的请求标头

| 标题| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 授权| 字符串。 授权 Xbox LIVE 的数据。 这通常是加密的 XSTS 令牌。 示例值： <b>XBL3.0 x =&lt;userhash >;&lt;令牌 ></b>。|

<a id="ID4EYF"></a>


## <a name="optional-request-headers"></a>可选的请求标头

| 标题| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| X RequestedServiceVersion| 生成此请求应定向到的 Xbox LIVE 的服务的名称/号码。 验证标头、 身份验证令牌等中的声明的有效性后仅为请求路由到该服务。默认值： 1。|
| 接受| 字符串。 内容类型的调用方接受在响应中。 所有响应都是<b>应用程序/json</b>。|

<a id="ID4E5G"></a>


## <a name="request-body"></a>请求正文

此请求的正文中不发送任何对象。

<a id="ID4EJH"></a>


## <a name="http-status-codes"></a>HTTP 状态代码

该服务返回的状态代码之一此部分中使用此方法对此资源进行的请求的响应。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。

| 代码| 原因短语| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 200| “确定”| 成功。|
| 400| 错误请求| 查询参数或用户 Id 的格式不正确。|
| 403| 已禁止| 无法分析 XUID 声明与授权标头中。|

<a id="ID4EBBAC"></a>


## <a name="required-response-headers"></a>所需的响应标头

| 标头| 类型| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Content-Length| 32 位无符号的整数| 长度，以字节为单位，响应正文。 示例值： 22。|
| Content-Type| 字符串| 响应正文的 MIME 类型。 这将始终为<b>应用程序/json</b>。|

<a id="ID4ENCAC"></a>


## <a name="response-body"></a>响应正文

如果调用成功，该服务的调用方的用户集合和数组，其中包含调用方的用户集合中返回用户的总数。 请参阅[PeopleList (JSON)](../../json/json-peoplelist.md)。

<a id="ID4EZCAC"></a>


### <a name="sample-response"></a>示例响应


```cpp
{
    "people": [
        {
            "xuid": "2603643534573573",
            "isFavorite": true,
            "isFollowingCaller": false,
            "socialNetworks": ["LegacyXboxLive"]
        },
        {
            "xuid": "2603643534573572",
            "isFavorite": true,
            "isFollowingCaller": false,
            "socialNetworks": ["LegacyXboxLive"]
        },
        {
            "xuid": "2603643534573577",
            "isFollowingCaller": false,
            "isFavorite": false
        },
    ],
    "totalCount": 3
}

```


<a id="ID4EDDAC"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EFDAC"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/users/ {ownerId} / 个人](uri-usersowneridpeople.md)
