---
title: 深度缓冲区
description: 深度缓冲区（或 z 缓冲区）存储深度信息，以控制渲染（而不是从视图中隐藏）哪些多边形区域。
ms.assetid: BE83A1D7-D43D-4013-8817-EFD2B24DC58E
keywords:
- 深度缓冲区
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: fb7ff4b23f9735347ce75e2e565c1b420ec936d6
ms.sourcegitcommit: 38f06f1714334273d865935d9afb80efffe97a17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "6191010"
---
# <a name="depth-buffers"></a>深度缓冲区


*深度缓冲区*（或 *z 缓冲区*）存储深度信息，以控制渲染（而不是从视图中隐藏）哪些多边形区域。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


深度缓冲区（通常称为 z 缓冲区或 w 缓冲区）是存储 Direct3D 要使用的深度信息的设备的属性。 当 Direct3D 将一个场景渲染到目标图面时，它可以将关联的深度缓冲区图面中的内存用作工作区，以确定栅格化的多边形的像素如何互相遮蔽。 Direct3D 将屏幕外 Direct3D 图面用作要写入最终颜色值的目标。 与渲染目标图面关联的深度缓冲区图面用于存储深度信息，此信息可告知 Direct3D 场景中每个可见像素的深度。

在启用深度缓冲的情况下将场景栅格化时，对渲染图面中的每个点进行测试。 深度缓冲区中的值可以是点的 z 坐标或其同类 w 坐标 - 从投影空间中该点的 (x,y,z,w) 位置。 使用 z 值的深度缓冲区通常称为 z 缓冲区，使用 w 值的深度缓冲区则称为 w 缓冲区。 每种类型的深度缓冲区各有优缺点，将在本文的稍后部分讨论。

开始测试时，深度缓冲区中的深度值设置为场景的最大可能值。 将渲染图面的颜色值设置为背景颜色值或此点的背景纹理的颜色值。 场景中的每个多边形都经过测试，以查看其是否与渲染图面上的当前坐标 (x,y) 相交。

如果相交，则对当前位置的深度值（将成为 z 缓冲区中的 z 坐标和 w 缓冲区中的 w 坐标）进行测试，查看其是否小于存储在深度缓冲区中的深度值。 如果多边形值深度较小，则它存储在深度缓冲区中，并将多边形中的颜色值写入到渲染图面的当前点。 如果此位置的多边形深度值较大，则测试列表中的下一个多边形。 此过程如以下图示中所示。

![测试深度值的图示](images/zbuffer.png)

## <a name="span-idbufferingtechniquesspanspan-idbufferingtechniquesspanspan-idbufferingtechniquesspanbuffering-techniques"></a><span id="Buffering_techniques"></span><span id="buffering_techniques"></span><span id="BUFFERING_TECHNIQUES"></span>缓冲技术


虽然大多数应用程序不会使用此功能，但是你可以更改 Direct3D 用于确定哪些值先后放置于深度缓冲区和渲染目标图面的比较函数。 在某些硬件上，更改比较函数可能会禁用分层结构测试。

市场上的所有加速器几乎都支持 z 缓冲，这使 z 缓冲区成为当前最常见的深度缓冲区类型。 尽管无处不在，但 z 缓冲区也有缺点。 由于涉及数学，在 z 缓冲区生成的 z 值通常无法在 z 缓冲区范围（通常为 0.0 至 1.0，非独占）中均匀分布。

具体来说，远剪裁平面和近剪裁平面之间的比率会严重影响 z 值分布的平均情况。 如果使用的远平面距离至近平面距离比率为 100，则 90% 的深度缓冲区范围要花费在前 10% 的场景深度范围上。 典型的娱乐应用程序或有外部场景的视觉仿真通常需要任意的远平面/近平面比率在 1,000 至 10,000 之间。 比率为 1000 时，范围的 98% 花费在前 2% 的深度范围上，且高比率的分布情况更糟。 这可能会导致远对象中的隐藏图面项目（特别是使用 16 位深度缓冲区时）成为最常受支持的位深度。

另一方面，较之 z 缓冲区，基于 w 的深度缓冲区通常在近剪裁平面和远剪裁平面之间分布地更平均。 主要优势在于，远剪裁平面和近剪裁平面之间的距离比不再是问题。 这允许应用程序支持大型的最大范围，并仍然能获得靠近眼点的相对正确的深度缓冲。 基于 w 的深度缓冲区并不完美，有时可能会出现近对象的隐藏图面项目。 w 缓冲方法的另一个缺点与硬件支持有关：w 缓冲在硬件中的受支持范围不如 z 缓冲广。

渲染期间使用 z 缓冲区需要开销。 有多种技术可用于优化使用 z 缓冲区时的渲染。 通过确保按从前往后的顺序渲染场景，应用程序可以提高使用 z 缓冲和纹理时的性能。 以扫描线为基础，针对 z 缓冲区对纹理化的 z 缓冲的基元进行了预测试。 如果扫描线被之前渲染的多边形隐藏，系统会快速高效地拒绝。 Z 缓冲可以提高性能，但当场景超过一次绘制相同像素时，这一技术最为有用。 这难以精确计算，但通常可以进行近似计算。 如果相同像素的绘制次数少于两次，你可以通过关闭 z 缓冲和从后往前渲染场景实现最佳性能。

深度值的实际解释特定于其渲染器。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[深度和模板缓冲区](depth-and-stencil-buffers.md)

 

 




