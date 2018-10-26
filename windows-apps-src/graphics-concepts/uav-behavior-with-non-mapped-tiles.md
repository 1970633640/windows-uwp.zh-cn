---
title: 使用非映射磁贴的 UAV 行为
description: 无序访问视图 (UAV) 读取和写入的行为依赖于硬件支持的级别。
ms.assetid: CDB224E2-CC07-4568-9AAC-C8DC74536561
keywords:
- 使用非映射磁贴的 UAV 行为
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: a5418de3646f70a815f5c482f9063ea3e48ddfa1
ms.sourcegitcommit: 6cc275f2151f78db40c11ace381ee2d35f0155f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "5549871"
---
# <a name="span-iddirect3dconceptsuavbehaviorwithnon-mappedtilesspanuav-behavior-with-non-mapped-tiles"></a><span id="direct3dconcepts.uav_behavior_with_non-mapped_tiles"></span>使用非映射磁贴的 UAV 行为


无序访问视图 (UAV) 读取和写入的行为依赖于硬件支持的级别。 有关具体要求，请参阅[流式资源功能层](streaming-resources-features-tiers.md)的整体读取和写入行为。 此部分总结理想行为。

从 UAV 中的非映射磁贴读取的着色器操作将在格式的所有未缺失组件中返回 0，并为缺失组件返回默认值。

尝试对非映射磁贴进行写入的着色器操作将导致不会将任何内容写入非映射区域（而继续对映射区域进行写入）。 写入处理的此理想定义不是[第 2 层](tier-2.md)要求的；对非映射磁贴的写入可能在后续读取可能选取的缓存中结束。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[对流式资源的管道访问](pipeline-access-to-streaming-resources.md)

 

 




