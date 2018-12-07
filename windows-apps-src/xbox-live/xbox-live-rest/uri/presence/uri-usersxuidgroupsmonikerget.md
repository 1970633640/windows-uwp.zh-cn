---
title: GET (/users/xuid({xuid})/groups/{moniker} )
assetID: 63aa7e5d-0599-5850-756d-3079c0772238
permalink: en-us/docs/xboxlive/rest/uri-usersxuidgroupsmonikerget.html
description: " GET (/users/xuid({xuid})/groups/{moniker} )"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: df967677ce779fc128a8956f137a027a108d313d
ms.sourcegitcommit: a3dc929858415b933943bba5aa7487ffa721899f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2018
ms.locfileid: "8792696"
---
# <a name="get-usersxuidxuidgroupsmoniker-"></a>GET (/users/xuid({xuid})/groups/{moniker} )
获取 presencerecord，他的一组。 这些 Uri 的域是`userpresence.xboxlive.com`。
 
  * [备注](#ID4EV)
  * [URI 参数](#ID4E5)
  * [查询字符串参数](#ID4EJB)
  * [授权](#ID4EKC)
  * [资源上的隐私设置的效果](#ID4EQD)
  * [需的请求标头](#ID4EEH)
  * [可选的请求标头](#ID4EMBAC)
  * [请求正文](#ID4EMCAC)
  * [HTTP 状态代码](#ID4EXCAC)
  * [所需的响应标头](#ID4E3GAC)
  * [可选的响应标头](#ID4EMJAC)
  * [响应正文](#ID4E5KAC)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>备注
 
检索相关 URI 中用户的名字对象由指定的组中的用户，并返回这些用户的 presencerecord，他。 受隐私或内容隔离的数据将只需不会返回。
  
<a id="ID4E5"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | 
| xuid| 字符串| Xbox 用户 ID (XUID) 相关的组中的 Xuid 的用户。| 
| 名字对象| 字符串| 定义的用户组的字符串。 目前仅接受名字对象以大写 P 是"People"。| 
  
<a id="ID4EJB"></a>

 
## <a name="query-string-parameters"></a>查询字符串参数
 
| 参数| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | 
| level| 字符串| 返回所指定的此查询字符串的详细的级别。 有效选项包括"用户"、"设备"、"标题"和"全部"。在级别"用户"是没有 DeviceRecord 嵌套对象的 presencerecord，他的对象。 级别"设备"是 presencerecord，他的和 DeviceRecord 的对象，而无需 TitleRecord 嵌套对象。 级别"标题"是没有 ActivityRecord 嵌套对象的 presencerecord，他、 DeviceRecord 和 TitleRecord 对象。 "全部"级别是整个记录，包括所有嵌套的对象。如果未提供此参数，该服务将默认为标题级别 （即，它将返回为标题的详细信息向此用户的状态）。| 
  
<a id="ID4EKC"></a>

 
## <a name="authorization"></a>授权
 
使用授权声明 | 声明| 类型| 是否必需？| 示例值| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| <b>Xuid</b>| 64 位有符号整数| 是| 1234567890| 
  
<a id="ID4EQD"></a>

 
## <a name="effect-of-privacy-settings-on-resource"></a>资源上的隐私设置的效果
 
该服务将始终返回 200 正常如果请求本身是标准格式。 但是，它将筛选出信息从响应时不能将隐私检查。
 
资源上的隐私设置的效果 | 请求的用户| 目标用户的隐私设置| 行为| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 我| -| 所述。| 
| 好友| 每个人都| 所述。| 
| 好友| 仅好友| 所述。| 
| 好友| 阻止| 所述的服务将筛选出的数据。| 
| 非好友用户| 每个人都| 所述。| 
| 非好友用户| 仅好友| 所述的服务将筛选出的数据。| 
| 非好友用户| 阻止| 所述的服务将筛选出的数据。| 
| 第三方网站| 每个人都| 所述的服务将筛选出的数据。| 
| 第三方网站| 仅好友| 所述的服务将筛选出的数据。| 
| 第三方网站| 阻止| 所述的服务将筛选出的数据。| 
  
<a id="ID4EEH"></a>

 
## <a name="required-request-headers"></a>需的请求标头
 
| 标头| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 授权| 字符串| HTTP 身份验证的身份验证凭据。 示例值:"XBL3.0 x =&lt;userhash >;&lt;令牌 >"。| 
| x xbl 协定版本| 字符串| 名称/的内部版本号应指向此请求的 Xbox LIVE 的服务。 请求将仅可路由到的服务验证该标头，身份验证令牌中的声明的有效性后，依此类推。 示例值： 3，vnext。| 
| 接受| 字符串| 内容类型的可接受。 只有一个存在支持<b>application/json</b>，但它仍然必须指定在标头中。| 
| 接受的语言| 字符串| 在响应中的字符串的可接受区域设置。 示例值： EN-US。| 
| Host| 字符串| 服务器的域名。 示例值： userpresence.xboxlive.com。| 
  
<a id="ID4EMBAC"></a>

 
## <a name="optional-request-headers"></a>可选的请求标头
 
| 标头| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| X RequestedServiceVersion|  | 名称/的内部版本号应指向此请求的 Xbox LIVE 的服务。 请求将仅可路由到的服务验证该标头，身份验证令牌中的声明的有效性后，依此类推。 默认值： 1。| 
  
<a id="ID4EMCAC"></a>

 
## <a name="request-body"></a>请求正文
 
此请求的正文中不发送任何对象。
  
<a id="ID4EXCAC"></a>

 
## <a name="http-status-codes"></a>HTTP 状态代码
 
此部分中使用此方法对此资源所做的请求的响应，该服务返回的状态代码之一。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。
 
| 代码| 原因短语| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| “确定”| 已成功检索会话。| 
| 400| 错误请求| 服务可能不理解格式不正确的请求。 通常无效参数。| 
| 401| 未授权| 请求要求用户身份验证。| 
| 403| 已禁止| 为用户或服务不允许该请求。| 
| 404| 找不到| 找不到指定的资源。| 
| 405| 不允许的方法| 不受支持的内容类型上所使用的 HTTP 方法。| 
| 406| 不允许| 资源版本不受支持。| 
| 500| 请求超时| 服务可能不理解格式不正确的请求。 通常无效参数。| 
| 503| 请求超时| 服务可能不理解格式不正确的请求。 通常无效参数。| 
  
<a id="ID4E3GAC"></a>

 
## <a name="required-response-headers"></a>所需的响应标头
 
| 标头| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl 协定版本| 字符串| 名称/的内部版本号应指向此请求的 Xbox LIVE 的服务。 请求将仅可路由到的服务验证该标头，身份验证令牌中的声明的有效性后，依此类推。 示例值： 1，vnext。| 
| Content-Type| 字符串| 请求正文中的 mime 类型。 示例值： <b>application/json</b>。| 
| 缓存控制| 字符串| 若要指定缓存行为的礼貌请求。 示例值:"无缓存"。| 
| X XblCorrelationId| 字符串| 将服务器的返回并什么由客户端接收关联起来的服务生成的值。 示例值:"4106d0bc-1cb3-47bd-83fd-57d041c6febe"。| 
| X 内容类型选项| 字符串| 返回符合 SDL 的值。 示例值:"nosniff"。| 
| 日期| 字符串| 日期/时间已发送消息。 示例值:"星期二，11 月 2012 年 17 10:33:31 格林威治标准时间"。| 
  
<a id="ID4EMJAC"></a>

 
## <a name="optional-response-headers"></a>可选的响应标头
 
| 标头| 类型| 描述| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 重试后| 字符串| 返回 503 HTTP 错误。 允许知道多长时间重试调用之前要等待的客户端。 示例值:"120"。| 
| Content-Length| 字符串| 响应正文的长度。 示例值:"第 527"。| 
| 内容编码| 字符串| 该响应的编码类型。 示例值:"gzip"。| 
  
<a id="ID4E5KAC"></a>

 
## <a name="response-body"></a>响应正文
 
此 API 返回 presencerecord，他的对象，一个用于每个请求中的 Xuid 的数组。
 
<a id="ID4EGLAC"></a>

 
### <a name="sample-response"></a>示例响应
 

```cpp
[
     {
         xuid:"0123456789",
         state:"online",
         devices:
         [
             {
                 type:"D",
                 titles:
                 [
                     {
                         id:"12341234",
                         name:"Contoso 5",
                         lastModified:"2012-09-17T07:15:23.4930000",
                         placement:"full",
                         state:"active",
                         activity:
                         {
                             richPresence:"Playing on Nirvana"
                         },
                     }
                 ]
             }
         ]
     },
     {
         xuid:"0123456780",
         state:"online",
         devices:
         [
             {
                 type:"D",
                 titles:
                 [
                     {
                         id:"12341235",
                         name:"Contoso Waypoint",
                         lastModified:"2012-09-17T07:15:23.4930000",
                         placement;"full",
                         state:"active",
                         activity:
                         {
                             richPresence:"Viewing stats"
                         },
                     }
                 ]
             }
         ]
     },
     {
         xuid:"0123456781",
         state:"online",
         devices:
         [
             {
                 type:"Win8",
                 titles:
                 [
                     {
                         id:"23452345",
                         name:"Contoso Gamehelp",
                         state:"active",
                         timestamp:"2012-09-17T07:15:23.4930000",
                         activity:
                         {
                             richPresence:"Viewing help"
                         }
                     }
                 ]
             }
         ]
     }
 ]
         
```

   
<a id="ID4EQLAC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ESLAC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[/users/xuid({xuid})/groups/{moniker}](uri-usersxuidgroupsmoniker.md)

   