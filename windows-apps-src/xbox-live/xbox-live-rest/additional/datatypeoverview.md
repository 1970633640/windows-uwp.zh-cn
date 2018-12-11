---
title: 数据类型概述
assetID: c154a6fa-e7b2-4652-f6fc-f946f74480e9
permalink: en-us/docs/xboxlive/rest/datatypeoverview.html
description: " 数据类型概述"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 62932a921d51a988a5533d7ee08f4968bb67a29d
ms.sourcegitcommit: 8921a9cc0dd3e5665345ae8eca7ab7aeb83ccc6f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "8889772"
---
# <a name="data-type-overview"></a>数据类型概述
 
Xbox Live 服务使用各种与标识和身份验证相关的数据类型。 本主题概要介绍了这些类型。
 
| 类型| 描述| 
| --- | --- | 
| 玩家代号| 用户的独特的用户可读的屏幕名称。| 
| 玩家| 一个 JSON 对象，包含用户的 XUID 和玩家代号，以及玩家的索引中的会话 （或"固定"），无论玩家仍然参与会话，并自定义数据的小 blob。| 
| profile| 用户配置文件 URI 地址和 HTTP 方法，通常是用户的 UserSettings 通过访问，但还可能包括玩家卡片玩家代号、 XUID，以及等信息。| 
| 设置| UserSettings 对象中的特定于游戏的设置之一。| 
| UserClaims| 简单的 JSON 对象，包含用户的 XUID 和玩家代号。| 
| UserSettings| 一个 JSON 对象，包含特定于游戏的设置或当前身份验证的用户首选项的集合。 UserSettings 可以包含可能与相关的游戏内活动的任意数据。| 
| XUID| 用户的 Xbox 用户 ID，一个唯一的无符号长整型。 不是用户可读。| 
 
<a id="ID4E6D"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EBE"></a>

 
##### <a name="parent"></a>Parent 的子磁盘）  

[其他参考](atoc-xboxlivews-reference-additional.md)

  
<a id="ID4ENE"></a>

 
##### <a name="reference--player-jsonjsonjson-playermd"></a>参考[Player (JSON)](../json/json-player.md)

 [UserClaims (JSON)](../json/json-userclaims.md)

 [UserSettings (JSON)](../json/json-usersettings.md)

   