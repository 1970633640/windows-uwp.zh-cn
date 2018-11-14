---
title: POST (/users/xuid({xuid})/deleteuserdata)
assetID: 8be13ff9-5d42-43a1-f2fa-d550d845a552
permalink: en-us/docs/xboxlive/rest/uri-usersxuiddeleteuserdatapost.html
author: KevinAsgari
description: " POST (/users/xuid({xuid})/deleteuserdata)"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: eb3fe5b0f51867987510e49477d0c5aa8e6c1c50
ms.sourcegitcommit: 38f06f1714334273d865935d9afb80efffe97a17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "6193036"
---
# <a name="post-usersxuidxuiddeleteuserdata"></a>POST (/users/xuid({xuid})/deleteuserdata)
完全重置为测试用户信誉数据。 仅供测试。

  * [备注](#ID4EQ)
  * [URI 参数](#ID4E5)
  * [授权](#ID4EJB)
  * [需的请求标头](#ID4E3B)
  * [HTTP 状态代码](#ID4EHC)
  * [响应正文](#ID4EJF)

<a id="ID4EQ"></a>


## <a name="remarks"></a>备注

调用此 API 将删除所有反馈项目和信誉数据从用户。 合作伙伴可以通过调用此 API 针对任何除零售沙盒。 执行团队可能会调用此 API 使用任何沙盒 id。

这些 Uri 的域是`reputation.xboxlive.com`。 端口 10443 始终调用此 URI。

<a id="ID4E5"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 说明|
| --- | --- | --- |
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 正在删除其数据的用户。|

<a id="ID4EJB"></a>


## <a name="authorization"></a>授权

Retail 沙盒中，从强制执行团队**PartnerClaim** 。

对于所有其他沙盒， **PartnerClaim**和**SandboxIdClaim**。

<a id="ID4E3B"></a>


## <a name="required-request-headers"></a>需的请求标头

**Content-type: application/json**和**X Xbl 协定版本**（当前版本是 101）。

<a id="ID4EHC"></a>


## <a name="http-status-codes"></a>HTTP 状态代码

此部分中使用此方法对此资源进行的请求的响应，该服务返回的状态代码之一。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。

| 代码| 原因短语| 说明|
| --- | --- | --- | --- | --- | --- |
| 200| “确定”| 已成功检索会话。|
| 400| 错误请求| 服务可能不理解格式不正确的请求。 通常无效参数。|
| 401| 未授权| 请求要求用户身份验证。|
| 404| 找不到| 找不到指定的资源。|
| 500| 内部服务器错误| 服务器时遇到意外的情况，执行此请求将阻止它。|
| 503| 服务不可用| 请求已被阻止，以秒为单位 （例如 5 秒更高版本） 的客户端重试值后重试请求。|

<a id="ID4EJF"></a>


## <a name="response-body"></a>响应正文

无成功;否则为[ServiceError (JSON)](../../json/json-serviceerror.md)文档。

<a id="ID4EWF"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EYF"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/users/xuid({xuid})/deleteuserdata](uri-usersxuiddeleteuserdata.md)
