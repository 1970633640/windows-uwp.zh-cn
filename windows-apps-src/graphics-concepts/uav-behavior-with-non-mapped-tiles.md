---
title: 使用非映射磁贴的 UAV 行为
description: 无序访问视图 (UAV) 读取和写入的行为依赖于硬件支持的级别。
ms.assetid: CDB224E2-CC07-4568-9AAC-C8DC74536561
keywords:
- 使用非映射磁贴的 UAV 行为
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: c72931d2f6bf1e892e174bc409f20a042d5e4c92
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57631622"
---
# <a name="span-iddirect3dconceptsuavbehaviorwithnon-mappedtilesspanuav-behavior-with-non-mapped-tiles"></a><span id="direct3dconcepts.uav_behavior_with_non-mapped_tiles"></span>UAV 行为与非映射磁贴


无序访问视图 (UAV) 读取和写入的行为依赖于硬件支持的级别。 有关具体要求，请参阅[流式资源功能层](streaming-resources-features-tiers.md)的整体读取和写入行为。 此部分总结理想行为。

从 UAV 中的非映射磁贴读取的着色器操作将在格式的所有未缺失组件中返回 0，并为缺失组件返回默认值。

尝试对非映射磁贴进行写入的着色器操作将导致不会将任何内容写入非映射区域（而继续对映射区域进行写入）。 写入处理的此理想定义不是[第 2 层](tier-2.md)要求的；对非映射磁贴的写入可能在后续读取可能选取的缓存中结束。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[管道到流式处理资源的访问权限](pipeline-access-to-streaming-resources.md)

 

 




