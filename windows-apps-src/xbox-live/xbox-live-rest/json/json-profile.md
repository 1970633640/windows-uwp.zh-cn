---
title: Profile (JSON)
assetID: b92b1750-c2df-39b6-6c5c-f9e8068c8097
permalink: en-us/docs/xboxlive/rest/json-profile.html
author: KevinAsgari
description: " Profile (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 0ae5e95befc6611c5905e6efe2bb01a396167626
ms.sourcegitcommit: 68fcac3288d5698a13dbcbd57f51b30592f24860
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2018
ms.locfileid: "4051348"
---
# <a name="profile-json"></a>Profile (JSON)
用户的个人配置文件设置。 
<a id="ID4EN"></a>

 
## <a name="profile"></a>个人资料
 
配置文件对象具有以下规范。
 
| 成员| 类型| 说明| 
| --- | --- | --- | 
| AppDisplayName| 字符串| 有关在应用中显示的名称。 这可能是用户的"真实姓名"或他们的玩家代号，具体取决于隐私。 此设置表示应显示在应用中使用的用户的标识字符串。| 
| GameDisplayName| 字符串| 用于在游戏中显示的名称。 这可能是用户的"真实姓名"或他们的玩家代号，具体取决于隐私。 此设置表示应显示在游戏中使用的用户的标识字符串。| 
| Gamertag| 字符串| 用户的玩家代号。| 
| AppDisplayPicRaw| 字符串| 原始应用显示 pic URL （如下所示）。| 
| GameDisplayPicRaw| 字符串| 原始游戏显示 pic URL （如下所示）。| 
| AccountTier| 字符串| 用户有何种帐户？ 金牌、 银牌或 FamilyGold？| 
| TenureLevel| 32 位无符号的整数| 用户已使用 Xbox Live 多少年？| 
| 玩家分数| 32 位无符号的整数| 玩家分数的用户。| 
  


> [!NOTE] 
> 图片可以是用户的真实图片或其 xbox One 玩家图片，具体取决于隐私。 这些设置表示应该用于客户端上显示的用户的图片 url。 此图像可能为空 （用于指示用户尚未设置任何图片）。 


 
原始 URL 是一个可调整大小的 URL。 它可以用于指定以下大小和格式使用通过将`&format={format}&w={width}&h={height}`为该 URI:
 
格式： png
 
大小： 64 x 64，208 x 208，424 x 424
 
<a id="ID4E2D"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4E4D"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

   