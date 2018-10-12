---
title: 玩家头像 URI
assetID: 811ab696-c433-aa54-90d8-66614ad09901
permalink: en-us/docs/xboxlive/rest/atoc-reference-gamerpic.html
author: KevinAsgari
description: " 玩家头像 URI"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: d612f2fe9cb327b792ed3ab73ad17421f394a030
ms.sourcegitcommit: 933e71a31989f8063b020746fdd16e9da94a44c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "4539673"
---
# <a name="gamerpic-uris"></a>玩家头像 URI
 
本部分提供了从*图片*的 Xbox Live 服务的详细信息的玩家图片通用资源标识符 (URI) 地址和关联的超文本传输协议 (HTTP) 方法。
 
这些 Uri 的域是`gamerpics.xboxlive.com`。
 
玩家图片服务旨在通过授予的能力，以允许用户以生成其游戏的字符的玩家图片的标题为用户提供更多个性化选项，（在此方案中的游戏字符指的是游戏内 protagonist; 它可以是一个人汽车、 宇宙飞船或用户控件在游戏中的任何其他实体)。
 
生成的游戏玩家图片的基本流程如下所示：
 
   * 标题为用户提供与能够创建其游戏内字符的图像。 
     * 如果不是，游戏可以然后消息它们没有相应的权限的用户。
     * 如果用户具有权限，用户可以继续创建其字符玩家头像。
  
   * 用户创建图像和标题向玩家头像服务发送 1080 x 1080.png 文件。
   * 该服务将存储该图像并设置为用户的新玩家图片的图像。
   * 为用户的玩家图片调用任何体验将获取更新的映像。
  
能够设置的游戏玩家图片受仅强制执行特权 (211)。 如果强制执行撤销权限，用户将无法保存的游戏的玩家图片，以及该服务将返回 403。 游戏应调用 CheckPrivilege 以验证允许用户要共享的内容 （专用 211）。
 
目前，才能使用此服务，你的游戏必须列入白名单。 若要请求批准，请发送电子邮件至`slsgamerpics@microsoft.com`。
 
<a id="ID4EGC"></a>

 
## <a name="in-this-section"></a>本部分内容

[/users/me/gamerpic](uri-usersmegamerpic.md)

&nbsp;&nbsp;访问 1080 x 1080 玩家头像。
 
<a id="ID4EMC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EOC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[统一资源标识符 (URI) 参考](../atoc-xboxlivews-reference-uris.md)

   