---
title: POST (/users/xuid({xuid})/feedback)
assetID: 48a7a510-a658-f2a3-c6bc-28a3610006e7
permalink: en-us/docs/xboxlive/rest/uri-reputationusersxuidfeedbackpost.html
description: " POST (/users/xuid({xuid})/feedback)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: d8a6e118811203fd34c310840e8688c2255c6beb
ms.sourcegitcommit: d2517e522cacc5240f7dffd5bc1eaa278e3f7768
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2018
ms.locfileid: "8340203"
---
# <a name="post-usersxuidxuidfeedback"></a>POST (/users/xuid({xuid})/feedback)
如果你希望能够在游戏中，而不是使用 shell 添加反馈选项，用于从你的游戏。 这些 Uri 的域是`reputation.xboxlive.com`。
 
  * [URI 参数](#ID4EZ)
  * [需的请求标头](#ID4EEB)
  * [请求正文](#ID4ENC)
  * [所需的标头](#ID4EDE)
  * [授权](#ID4EXF)
  * [HTTP 状态代码](#ID4EEG)
  * [响应正文](#ID4EZH)
 
<a id="ID4EZ"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | 
| xuid| ulong| Xbox 用户 ID (XUID) 所报告的用户。| 
  
<a id="ID4EEB"></a>

 
## <a name="required-request-headers"></a>需的请求标头
 
| 标头| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | 
| 授权| 字符串| HTTP 身份验证的身份验证凭据。 示例值:"XBL3.0 x =&lt;userhash >;&lt;令牌 >"。| 
| X RequestedServiceVersion|  | 生成此请求应定向到 Xbox LIVE 的服务的名称/数。 请求将仅可路由到的服务验证该标头，身份验证令牌中的声明的有效性后，依次类推。 默认值： 101。| 
  
<a id="ID4ENC"></a>

 
## <a name="request-body"></a>请求正文 
 
<a id="ID4EVC"></a>

 
### <a name="required-members"></a>所需的成员 
 
请求应包含一个[反馈](../../json/json-feedback.md)对象。 
  
<a id="ID4EED"></a>

 
### <a name="prohibited-members"></a>禁止的成员 
 
所有其他成员被禁止在请求中。
  
<a id="ID4ETD"></a>

 
### <a name="sample-request"></a>示例请求 
 

```cpp
{
    "sessionRef":
    {
        "scid": "372D829B-FA8E-471F-B696-07B61F09EC20",
        "templateName": "CaptureFlag5",
        "name": "Halo556932",
    },
    "feedbackType": "CommsAbusiveVoice",
    "textReason": "He called me a doodoo-head!",
    "voiceReasonId": null,
    "evidenceId": null
}

      
```

   
<a id="ID4EDE"></a>

 
## <a name="required-headers"></a>所需的标头
 
在 Xbox Live 服务请求时，以下标头是必需的。
 
| <b>标头</b>| <b>值</b>| <b>Deacription</b>| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl 协定版本| 101| API 协定版本。| 
| 授权| XBL3.0 x = [哈希];[令牌]| STS 身份验证令牌。 STSTokenString 替换为由身份验证请求返回的令牌。| 
内容类型| 
应用程序/json| 
在提交的数据的类型。| 
  
<a id="ID4EXF"></a>

 
## <a name="authorization"></a>授权
 
请求必须包含有效的 Xbox Live 授权标头。 如果调用方不允许访问此资源，该服务返回 403 禁止访问代码。 如果在标头无效或不存在，该服务返回 401 未经授权的代码。
  
<a id="ID4EEG"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码
 
此部分中使用此方法对此资源所做的请求的响应，该服务返回一个状态代码。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 204| 任何内容| 请求已完成，但没有要返回的内容。| 
| 401| 未授权| 请求要求用户身份验证。| 
| 404| 找不到| 找不到指定的资源。| 
| 406| 不允许| 资源版本不受支持。| 
| 408| 请求超时| 请求所花的时间太长，才能完成。| 
| 409| 冲突| 延续令牌不再有效。| 
  
<a id="ID4EZH"></a>

 
## <a name="response-body"></a>响应正文 
 
如果在调用成功，此响应中不返回任何对象。 否则，该服务返回[ServiceError](../../json/json-serviceerror.md)对象。
  
<a id="ID4EOAAC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EQAAC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[/users/xuid({xuid})/feedback](uri-reputationusersxuidfeedback.md)

  
<a id="ID4E3AAC"></a>

 
##### <a name="reference"></a>参考 

[Feedback (JSON)](../../json/json-feedback.md)

 [ServiceError (JSON)](../../json/json-serviceerror.md)

   