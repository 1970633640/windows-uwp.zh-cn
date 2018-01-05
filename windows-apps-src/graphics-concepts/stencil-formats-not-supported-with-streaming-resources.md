---
title: "使用流式资源时，模板格式不受支持"
description: "使用流式资源时，包含模板的格式不受支持。"
ms.assetid: 90A572A4-3C76-4795-BAE9-FCC72B5F07AD
keywords: "使用流式资源时，模板格式不受支持"
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 330b768c0f00f36ce8ce539b9ce41c7ac812e6fc
ms.sourcegitcommit: c80b9e6589a1ee29c5032a0b942e6a024c224ea7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="stencil-formats-not-supported-with-streaming-resources"></a>使用流式资源时，模板格式不受支持


使用流式资源时，包含模板的格式不受支持。

包含模板的格式包括 DXGI\_FORMAT\_D24\_UNORM\_S8\_UINT（及 R24G8 系列中的相关格式）和 DXGI\_FORMAT\_D32\_FLOAT\_S8X24\_UINT（及 R32G8X24 系列中的相关格式）。

某些实现以独立分配方式存储深度和模板，而另一些实现将两者存储在一起。 针对两种方案的磁贴管理必须有所不同，并且任何单个 API 均不可抽象差异或使差异合理化。 我们建议使用未来的硬件，以支持独立深度和模板表面（均独立平铺）。

32 位深度磁贴大小为 128 x 128，8 位模板磁贴大小为 256 x 256。 因此，应用必须适应深度和模板之间的磁贴形状错位。 但不同的呈现器目标表面格式已经存在同样的问题。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[跨进程和设备共享的流式资源](streaming-resource-cross-process-and-device-sharing.md)

 

 




