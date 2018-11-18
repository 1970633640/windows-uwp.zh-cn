---
title: /users/xuid({xuid})/deleteuserdata
assetID: 1925da6f-f6c1-ae5b-5af9-e143b70e6717
permalink: en-us/docs/xboxlive/rest/uri-usersxuiddeleteuserdata.html
author: KevinAsgari
description: " /users/xuid({xuid})/deleteuserdata"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 5eaba6a02fa2ebb00ef4861a5bf37963796b78b5
ms.sourcegitcommit: 3257416aebb5a7b1515e107866806f8bd57845a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2018
ms.locfileid: "7146180"
---
# <a name="usersxuidxuiddeleteuserdata"></a>/users/xuid({xuid})/deleteuserdata
完全重置为测试用户信誉数据。 仅供测试。 这些 Uri 的域是`reputation.xboxlive.com`。 端口 10443 上始终调用此 URI。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| xuid| 64 位无符号的整数| Xbox 用户 ID (XUID) 正在删除其数据的用户。| 
  
<a id="ID4EYB"></a>

 
## <a name="valid-methods"></a>有效的方法

[POST (/users/xuid({xuid})/deleteuserdata)](uri-usersxuiddeleteuserdatapost.md)

&nbsp;&nbsp;完全重置为测试用户信誉数据。 仅供测试。
 
<a id="ID4ECC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EEC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[信誉 URI](atoc-reference-reputation.md)

   