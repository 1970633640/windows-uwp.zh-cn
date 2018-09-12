---
title: /users/xuid({xuid})/deleteuserdata
assetID: 1925da6f-f6c1-ae5b-5af9-e143b70e6717
permalink: en-us/docs/xboxlive/rest/uri-usersxuiddeleteuserdata.html
author: KevinAsgari
description: " /users/xuid({xuid})/deleteuserdata"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: fe1129db6154d842cbadf0e7918d2fe460166ba1
ms.sourcegitcommit: 2a63ee6770413bc35ace09b14f56b60007be7433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3936239"
---
# <a name="usersxuidxuiddeleteuserdata"></a>/users/xuid({xuid})/deleteuserdata
完全重置为测试用户信誉数据。 仅供测试。 这些 Uri 的域是`reputation.xboxlive.com`。 端口 10443 始终调用此 URI。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 要删除其数据的用户。| 
  
<a id="ID4EYB"></a>

 
## <a name="valid-methods"></a>有效的方法

[POST (/users/xuid({xuid})/deleteuserdata)](uri-usersxuiddeleteuserdatapost.md)

&nbsp;&nbsp;完全重置为测试用户信誉数据。 仅供测试。
 
<a id="ID4ECC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EEC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[信誉 Uri](atoc-reference-reputation.md)

   