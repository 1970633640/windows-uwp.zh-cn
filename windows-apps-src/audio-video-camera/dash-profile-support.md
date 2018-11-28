---
ms.assetid: 3E0FBB43-F6A4-4558-AA89-20E7760BA73F
description: 本文列出了 UWP 应用支持的 HTTP 动态自适应流式处理 (DASH) 配置文件。
title: HTTP 动态自适应流式处理 (DASH) 配置文件支持
ms.date: 02/15/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: d680f7d4a3510f66cba74d1c8b30d8883b07369a
ms.sourcegitcommit: b5c9c18e70625ab770946b8243f3465ee1013184
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "7966662"
---
# <a name="dynamic-adaptive-streaming-over-http-dash-profile-support"></a>HTTP 动态自适应流式处理 (DASH) 配置文件支持


## <a name="supported-dash-profiles"></a>支持的 DASH 配置文件
下表列出了 UWP 应用支持的 DASH 配置文件。

|标记 | 清单类型 | 备注|7 月发布的 Windows 10|Windows 10 版本 1511|Windows 10 版本 1607 |Windows 10 版本 1607 |Windows 10 版本 1703|
|----------------|------|-------|-----------|--------------|---------|-------|--------|
|urn:mpeg&#58;dash:profile:isoff-live:2011 | 静态 |     |支持            |  支持              | 支持        |支持| 受支持|
|urn:mpeg&#58;dash:profile:isoff-main:2011 |        | 最大努力 | 支持            |  支持              | 支持        |支持| 受支持|
|urn:mpeg&#58;dash:profile:isoff-live:2011 | 动态 | $Time$ 受支持，但 $Number$ 在类别模板中不受支持 | 不支持            | 不支持              | 不支持        |不支持| 受支持|


## <a name="unsupported-dash-profiles"></a>不支持的 DASH 配置文件
上表中未列出的即为不支持的配置文件，包括但不限于以下配置文件：

* urn:mpeg&#58;dash:profile:full:2011
* urn:mpeg&#58;dash:profile:isoff-on-demand:2011
* urn:mpeg&#58;dash:profile:mp2t-main:2011
* urn:mpeg&#58;dash:profile:mp2t-simple:2011


## <a name="related-topics"></a>相关主题

* [媒体播放](media-playback.md)
* [自适应流式处理](adaptive-streaming.md)
 

 




