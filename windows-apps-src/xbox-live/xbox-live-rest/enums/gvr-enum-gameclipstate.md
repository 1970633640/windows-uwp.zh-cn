---
title: GameClipState 枚举
assetID: 97fe5c1e-f7b5-537e-69eb-8284b69cd3e1
permalink: en-us/docs/xboxlive/rest/gvr-enum-gameclipstate.html
author: KevinAsgari
description: " GameClipState 枚举"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 9ce2ec90377dcd78797fa5708577f24028c3ccf2
ms.sourcegitcommit: cd00bb829306871e5103db481cf224ea7fb613f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "5870854"
---
# <a name="gameclipstate-enumeration"></a>GameClipState 枚举
详细介绍 GameClipState 枚举。 
<a id="ID4ET"></a>

 
## <a name="gameclipstate"></a>GameClipState
 
| <b>枚举</b>| <b>说明</b>| 
| --- | --- | 
| 无 | 游戏剪辑服务状态为未知或未设置。| 
| PendingUpload | 游戏剪辑服务正在等待资源上传。| 
| PendingDelete | 在队列中删除的游戏剪辑。 （有效即"删除"）。| 
| 已处理 | 游戏剪辑已完成所有处理。| 
| Processing| 正在处理游戏剪辑 （编码，缩略图等。）。| 
| 发布| 正在发布游戏剪辑资产。| 
| Published| 发布游戏剪辑资产 – 此状态表明它是所有组来查看。| 
| 标记| 被用于强制标记游戏剪辑。| 
| 禁止| 已禁止游戏剪辑，但尚未删除。| 
| Uploaded| 游戏剪辑已完成上传。| 
| 删除| 游戏剪辑已被删除。| 
| 错误| 游戏剪辑处于错误状态和不可用。| 
  