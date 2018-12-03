---
title: GET (/handles/{handle-id})
assetID: c95b5ab5-d56a-f70d-20d8-afb48d122ccd
permalink: en-us/docs/xboxlive/rest/uri-handleshandleidget.html
description: " GET (/handles/{handle-id})"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 501d36f4d1ac079af15d6bb7f35a90d5328fc8db
ms.sourcegitcommit: d2517e522cacc5240f7dffd5bc1eaa278e3f7768
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2018
ms.locfileid: "8340082"
---
# <a name="get-handleshandle-id"></a>GET (/handles/{handle-id})
检索句柄 ID 指定的句柄

> [!IMPORTANT]
> 此方法使用 2015年多人游戏，并将应用仅向该多人游戏版本及更高版本。 它旨在用于使用模板合约 104/105 或更高版本，并且需要 X Xbl 协定版本的标头元素： 104/105 或更高版本上的每个请求。

  * [备注](#ID4ET)
  * [URI 参数](#ID4EDB)
  * [HTTP 状态代码](#ID4EOB)
  * [请求正文](#ID4EUB)
  * [响应正文](#ID4E5B)

<a id="ID4ET"></a>


## <a name="remarks"></a>备注

此 HTTP/REST 方法获取用户的当前活动会话，指定的句柄。 返回会话对象，使用所有属性。 此方法可以通过**Microsoft.Xbox.Services.Multiplayer.MultiplayerService.GetCurrentSessionByHandleAsync**换行。

此方法的调用方从玩家的**MultiplayerActivityDetails**对象获得的句柄 ID。 或者，调用方获取 ID 从协议激活后用户已接受游戏邀请。

<a id="ID4EDB"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 描述|
| --- | --- | --- | --- |
| handleId| GUID| 会话句柄的唯一 ID。|

<a id="ID4EOB"></a>


## <a name="http-status-codes"></a>HTTP 状态代码
该服务返回 HTTP 状态代码，因为它适用于 MPSD。  
<a id="ID4EUB"></a>


## <a name="request-body"></a>请求正文

此请求的正文中不发送任何对象。

<a id="ID4E5B"></a>


## <a name="response-body"></a>响应正文
请参阅[MultiplayerSession (JSON)](../../json/json-multiplayersession.md)中的响应结构。  
<a id="ID4EKC"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EMC"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/handles/{handleId}](uri-handleshandleid.md)
