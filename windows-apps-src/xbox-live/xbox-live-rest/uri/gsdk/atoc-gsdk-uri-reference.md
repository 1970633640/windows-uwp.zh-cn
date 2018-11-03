---
title: 游戏服务器统一资源标识符 (URI) 参考
assetID: bbd7e3f3-77ac-6ffd-8951-fe4b8b48eb4c
permalink: en-us/docs/xboxlive/rest/atoc-gsdk-uri-reference.html
author: KevinAsgari
description: " 游戏服务器统一资源标识符 (URI) 参考"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 9eff98593c122001cab591b9f45793aa6649736a
ms.sourcegitcommit: 144f5f127fc4fbd852f2f6780ef26054192d68fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2018
ms.locfileid: "5981508"
---
# <a name="game-server-universal-resource-identifier-uri-reference"></a>游戏服务器统一资源标识符 (URI) 参考
客户端用于创建游戏的游戏服务器开发工具包服务器实例的 Uri。 这些 Uri 的域是`gameserverds.xboxlive.com`和`gameserverms.xboxlive.com`。
 
<a id="ID4EY"></a>

 
## <a name="in-this-section"></a>本部分内容

[/qosservers](uri-qosservers.md)

&nbsp;&nbsp;URI 由客户端使用 Xbox Live 计算获取可用的 QoS 服务器的列表。

[/titles/{titleId}/clusters](uri-titlestitleidclusters.md)

&nbsp;&nbsp;允许客户端创建游戏的 Xbox Live 计算服务器实例的 URI。

[/titles/{titleId}/variants](uri-titlestitleidvariants.md)

&nbsp;&nbsp;获取可用的变体游戏的客户端调用的 URI。

[/titles/{titleId}/sessionhosts](uri-titlestitleidsessionhosts.md)

&nbsp;&nbsp;请求 Xbox Live 计算 sessionhost，若要为给定的主题作品 id 分配。

[/titles/{titleId}/sessions/{sessionId}/allocationStatus](uri-titlestitleidsessionssessionidallocationstatus.md)

&nbsp;&nbsp;对于给定的作品 id 和会话 id，获取票证请求的状态。
 