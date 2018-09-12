---
title: 放入 (/handles/ {句柄 id} / 会话)
assetID: d8a3d473-1192-ec0c-3935-c301f4f61e03
permalink: en-us/docs/xboxlive/rest/uri-handleshandleidsessionput.html
author: KevinAsgari
description: " 放入 (/handles/ {句柄 id} / 会话)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 89572da87f4975aeeaa1ae7506a34f2b9cb4e72a
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881169"
---
# <a name="put-handleshandle-idsession"></a>放入 (/handles/ {句柄 id} / 会话)
创建或更新会话由取消引用句柄。

> [!IMPORTANT]
> 此方法使用 2015年多人游戏和应用仅向该多人游戏版本及更高版本。 它旨在用于使用模板合约 104/105 或更高版本，并且需要 X Xbl 协定版本的标头元素： 104/105 或更高版本上的每个请求。

  * [备注](#ID4ET)
  * [URI 参数](#ID4ECB)
  * [HTTP 状态代码](#ID4ENB)
  * [请求正文](#ID4EUB)
  * [响应正文](#ID4E6B)

<a id="ID4ET"></a>


## <a name="remarks"></a>备注

此 HTTP/REST 方法将新的或更新会话写入多人游戏服务，使用提供的会话句柄 id。 结果是一个表示新的或更新会话，如从服务器返回的对象。 此方法可以由**Microsoft.Xbox.Services.Multiplayer.MultiplayerService.WriteSessionByHandleAsync**包装。

此方法的调用方从玩家的**MultiplayerActivityDetails**对象获得的句柄 ID。 或者，调用方获取的 ID 从协议激活后用户已接受游戏邀请。

<a id="ID4ECB"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 说明|
| --- | --- | --- | --- |
| handleId| GUID| 会话句柄的唯一 ID。|

<a id="ID4ENB"></a>


## <a name="http-status-codes"></a>HTTP 状态代码
该服务返回 HTTP 状态代码应用于 MPSD。  
<a id="ID4EUB"></a>


## <a name="request-body"></a>请求正文

此请求的正文中不发送任何对象。

<a id="ID4E6B"></a>


## <a name="response-body"></a>响应正文

该响应正文中不发送任何对象。

<a id="ID4EKC"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EMC"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/handles/ {handleId} / 会话](uri-handleshandleidsession.md)
