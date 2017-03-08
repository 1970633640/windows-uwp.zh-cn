---
title: "流式资源功能层"
description: "Direct3D 具有三层功能，可为流式资源提供支持。"
ms.assetid: 6AE7EA72-3929-4BB4-8780-F0CF26192D87
keywords:
- "流式资源功能层"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: ba1ec47e389f8de4bfd2ab190f1dfe078724deab
ms.lasthandoff: 02/07/2017

---

# <a name="streaming-resources-features-tiers"></a>流式资源功能层


Direct3D 具有三层功能，可为流式资源提供支持。

第 1 层提供了用于流式资源的基本功能。

第 2 层在第 1 层基础上增加了一些功能，如在大小至少为一个标准磁贴形状时保证非环绕纹理的 mipmap；具有用于固定详细信息级别 (LOD) 及用于获取着色器操作相关状态的着色器指令；此外，可读取将采样值视为零的 NULL 映射磁贴。

第 3 层功能在第 2 层的基础上增加了 Texture3D 功能。

Direct3D 版本提供查询功能，可验证支持流式资源的硬件和驱动程序及其所处的层级别。

## <a name="span-idin-this-sectionspanin-this-section"></a><span id="in-this-section"></span>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[第 1 层](tier-1.md)</p></td>
<td align="left"><p>本部分将介绍第 1 层支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[第 2 层](tier-2.md)</p></td>
<td align="left"><p>第 2 层流式资源支持在第 1 层基础上增加了一些功能，如在大小至少为一个标准磁贴形状时保证非环绕纹理的 mipmap；具有用于固定详细信息级别 (LOD) 及用于获取着色器操作相关状态的着色器指令；此外，可读取将采样值视为零的 NULL 映射磁贴。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[第 3 层](tier-3.md)</p></td>
<td align="left"><p>第 3 层除了具有[第 2 层](tier-2.md)功能之外，还增加了用于流式资源的 Texture3D 支持。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[流式资源](streaming-resources.md)

 

 





