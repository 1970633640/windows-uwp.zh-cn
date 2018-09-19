---
title: DELETE (/handles/{handleId})
assetID: 71cceff4-3a74-dc05-12db-cfe3f20a8aea
permalink: en-us/docs/xboxlive/rest/uri-handleshandleiddelete.html
author: KevinAsgari
description: " DELETE (/handles/{handleId})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 15300451495c198a1f15997bae38cb862a9b8186
ms.sourcegitcommit: 68fcac3288d5698a13dbcbd57f51b30592f24860
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2018
ms.locfileid: "4051718"
---
# <a name="delete-handleshandleid"></a>DELETE (/handles/{handleId})
句柄 ID 指定的删除句柄

> [!IMPORTANT]
> 此方法由 2015年多人游戏和应用仅向该多人游戏版本及更高版本。 它旨在用于使用模板合约 104/105 或更高版本，并且需要 X Xbl 协定版本的标头元素： 104/105 或更高版本上的每个请求。

  * [备注](#ID4ET)
  * [URI 参数](#ID4EAB)
  * [HTTP 状态代码](#ID4ELB)
  * [请求正文](#ID4ESB)
  * [响应正文](#ID4E4B)

<a id="ID4ET"></a>


## <a name="remarks"></a>备注
此 HTTP/REST 方法针对指定 ID 删除句柄，并清除会话的用户的当前活动。 此方法可以通过**Microsoft.Xbox.Services.Multiplayer.MultiplayerService.ClearActivityAsync**换行。  
<a id="ID4EAB"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 说明|
| --- | --- | --- | --- |
| handleId| GUID| 会话句柄的唯一 ID。|

<a id="ID4ELB"></a>


## <a name="http-status-codes"></a>HTTP 状态代码
该服务返回 HTTP 状态代码，因为它适用于 MPSD。  
<a id="ID4ESB"></a>


## <a name="request-body"></a>请求正文

此请求的正文中不发送任何对象。

<a id="ID4E4B"></a>


## <a name="response-body"></a>响应正文

该响应正文中不发送任何对象。

<a id="ID4EIC"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EKC"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/handles/{handleId}](uri-handleshandleid.md)
