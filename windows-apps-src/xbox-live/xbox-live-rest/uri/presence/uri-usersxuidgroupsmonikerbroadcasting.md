---
title: /users/xuid({xuid})/groups/{moniker}/broadcasting
assetID: cf8319f6-46a2-b263-ea4c-f1ce403b571b
permalink: en-us/docs/xboxlive/rest/uri-usersxuidgroupsmonikerbroadcasting.html
author: KevinAsgari
description: " /users/xuid({xuid})/groups/{moniker}/broadcasting"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 8df1812871272526c8b7d4242aa64a97610fc4cc
ms.sourcegitcommit: e814a13978f33654d8e995584f4b047cb53e0aef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "6042444"
---
# <a name="usersxuidxuidgroupsmonikerbroadcasting"></a>/users/xuid({xuid})/groups/{moniker}/broadcasting
访问组名字对象由指定的广播用户的状态记录相关出现在 URI 中的 XUID。 这些 Uri 的域是`userpresence.xboxlive.com`。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| xuid| 字符串| Xbox 用户 ID (XUID) 相关的组中的 Xuid 的用户。| 
| 名字对象| 字符串| 定义的用户组的字符串。 目前仅接受名字对象大写 P 是"People"。| 
  
<a id="ID4E4B"></a>

 
## <a name="valid-methods"></a>有效的方法

[GET (/users/xuid({xuid})/groups/{moniker}/broadcasting )](uri-usersxuidgroupsmonikerbroadcastingget.md)

&nbsp;&nbsp;检索与在 URI 中出现的 XUID 相关的组名字对象由指定的广播用户的状态记录。
 
<a id="ID4EHC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EJC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[状态 URI](atoc-reference-presence.md)

   