---
title: 流式资源区域的平铺方式
description: 创建流式资源时，尺寸、格式元素大小以及 mipmap 和/或数组切片的数量（如适用）决定了支持整个图面区域所需的磁贴数量。
ms.assetid: 3485FD8D-2A06-4B0A-8810-ECF37736F94B
keywords:
- 流式资源区域的平铺方式
- 资源区域, 平铺
- 尺寸表, 资源, 平铺
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 7251d4595a3e87a8629d6e717bb4f52e5b7c35fe
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57615362"
---
# <a name="how-a-streaming-resources-area-is-tiled"></a>流式资源区域的平铺方式


创建流式资源时，尺寸、格式元素大小以及 mipmap 和/或数组切片的数量（如适用）决定了支持整个图面区域所需的磁贴数量。 磁贴内的像素/字节布局由实现来确定。 适合磁贴的像素数量取决于格式元素大小，并且是固定和相同的，无论你是否使用标准重排。

以下部分中的表已明确定义给定图面大小和格式元素宽度使用的磁贴数，并且可根据这些表预测磁贴数。 对于包含 mipmap 的资源或图面尺寸不填充磁贴的情况，存在一些限制；请参阅 [Mipmap 打包](mipmap-packing.md)。

只要应用程序不依赖于用一种格式写入内存并用另一种格式读取内存所产生的结果，不同的流式资源就可以指向具有不同格式的相同内存。 但是，如果格式属于相同的格式系列（即，格式具有相同的无类型父格式），则应用程序可以依赖于用一种格式写入内存并用另一种格式读取内存所产生的结果。 例如，DXGI\_格式\_R8G8B8A8\_UNORM 和 DXGI\_格式\_R8G8B8A8\_UINT 是兼容但不能使用 DXGI\_格式\_R16G16\_UNORM。

例外情况是，来自别名为另一种格式的格式中的出血数据已被明确定义：如果磁贴的所有位都完全包含 0，则该磁贴可以使用将内存内容解释为 0 的任何格式（不考虑内存布局）。 因此，使用格式 DXGI 0x00 到无法清除磁贴\_格式\_R8\_UNORM 和随后用于一格式，如 DXGI\_格式\_R32G32\_浮点型和它将显示的内容可能会仍 （0.0f，0.0f）。

磁贴内的数据布局不取决于磁贴在资源整体中映射到的位置。 例如，可以一次性在图面的不同位置重新使用磁贴，且磁贴在所有位置都具有一致的行为。

## <a name="span-idin-this-sectionspanin-this-section"></a><span id="in-this-section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="texture2d-and-texture2darray-subresource-tiling.md">Texture2D 和 Texture2DArray 子资源平铺</a></p></td>
<td align="left"><p>这些表说明了 <a href="https://msdn.microsoft.com/library/windows/desktop/ff471525"><strong>Texture2D</strong></a> 和 <a href="https://msdn.microsoft.com/library/windows/desktop/ff471526"><strong>Texture2DArray</strong></a> 子资源的平铺方式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="texture3d-subresource-tiling.md">Texture3D 子资源平铺</a></p></td>
<td align="left"><p>此表说明了 <a href="https://msdn.microsoft.com/library/windows/desktop/ff471562"><strong>Texture3D</strong></a> 子资源的平铺方式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="buffer-tiling.md">缓冲区平铺</a></p></td>
<td align="left"><p>一个<a href="introduction-to-buffers.md">缓冲区</a>资源分为多个 64KB 的磁贴，如果最后一个磁贴的大小不是 64KB 的倍数，其中会有一些空白空间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="mipmap-packing.md">Mipmap 装箱</a></p></td>
<td align="left"><p>可将一定数量的 mip（每个数组切片）打包到一定数量的磁贴中，这取决于流式资源的尺寸、格式、mipmap 的数量和数组切片。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[创建流式处理资源](creating-streaming-resources.md)

 

 




