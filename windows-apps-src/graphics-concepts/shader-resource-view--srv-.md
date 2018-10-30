---
title: 着色器资源视图 (SRV) 和无序的访问视图 (UAV)
description: 着色器资源视图通常以方便着色器访问纹理的方式围绕纹理。 无序的访问视图提供类似的功能，但支持以任何顺序读取和写入纹理（或其他资源）。
ms.assetid: 4505BCD2-0EDA-40F2-887C-EC081FE32E8F
keywords:
- 着色器资源视图 (SRV)
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: e98b9942dfc14604c061a036cd3c9803abaf3915
ms.sourcegitcommit: 753e0a7160a88830d9908b446ef0907cc71c64e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "5757807"
---
# <a name="shader-resource-view-srv-and-unordered-access-view-uav"></a>着色器资源视图 (SRV) 和无序的访问视图 (UAV)


着色器资源视图通常以方便着色器访问纹理的方式围绕纹理。 无序的访问视图提供类似的功能，但支持以任何顺序读取和写入纹理（或其他资源）。

环绕单个纹理可能是着色器资源视图最简单的形式。 更为复杂的示例包括子资源集合（细化纹理的个别阵列、平面或颜色）、3D 纹理、1D 纹理颜色渐变等。

无序的访问视图在性能方面费用稍高，但支持同时读/写纹理等功能。 借此，图形管道可将已更新的纹理用于其他目的。 着色器资源视图具有只读用法（这是最常见的资源用法）。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[视图](views.md)

 

 




