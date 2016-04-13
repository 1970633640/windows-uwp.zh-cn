---
操作实例：使用 Direct3D 11 中的深度缓冲区实现阴影卷
本操作实例演示如何使用深度映射呈现阴影卷，并在所有 Direct3D 功能级别的设备上使用 Direct3D 11。
ms.assetid: d15e6501-1a1d-d99c-d1d8-ad79b849db90
---

# 操作实例：使用 Direct3D 11 中的深度缓冲区实现阴影卷


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

本操作实例演示如何使用深度映射呈现阴影卷，并在所有 Direct3D 功能级别的设备上使用 Direct3D 11。
## 
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
<td align="left"><p>[Create depth buffer device resources](create-depth-buffer-resource--view--and-sampler-state.md)</p></td>
<td align="left"><p>了解如何创建支持阴影卷的深度测试所需的 Direct3D 设备资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[Render the shadow map to the depth buffer](render-the-shadow-map-to-the-depth-buffer.md)</p></td>
<td align="left"><p>从光线的角度呈现，以创建一个表示阴影卷的二维深度映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[Render the scene with depth testing](render-the-scene-with-depth-testing.md)</p></td>
<td align="left"><p>通过向顶点（或几何图形）着色器和像素着色器中添加深度测试来创建阴影效果。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[Support shadow maps on a range of hardware](target-a-range-of-hardware.md)</p></td>
<td align="left"><p>在速度更快的设备上更高保真度地呈现阴影，在功能不够强大的设备上更快地呈现阴影。</p></td>
</tr>
</tbody>
</table>

 

## 阴影映射应用程序到 Direct3D 9 桌面的移植


Windows 8 为功能级别 9\_1 和 9\_3 添加了深度比较功能。 现在，你可以将具有阴影卷的呈现代码迁移到 DirectX 11，并且 Direct3D 11 呈现器将是与功能级别 9 设备兼容的下一级设备。 本操作实例介绍任何 Direct3D 11 应用或游戏如何使用深度测试实现传统的阴影卷。 代码包含以下过程：

1.  为阴影映射创建 Direct3D 设备资源。
2.  添加呈现传递以创建深度映射。
3.  将深度测试添加到主呈现传递。
4.  实现必需的着色器代码。
5.  用于在下一级硬件上快速呈现的选项。

完成本操作实例之后，你应该会熟悉如何在与功能级别 9\_1 以及更高功能级别兼容的 Direct3D 11 中实现基本的兼容阴影卷技术。

## 先决条件


应该[准备通用 Windows 平台 (UWP) DirectX 游戏开发的开发人员环境](prepare-your-dev-environment-for-windows-store-directx-game-development.md)。 目前，你还不需要模板，但需要使用 Microsoft Visual Studio 2015 为此操作实例生成代码示例。

## 相关主题


**Direct3D**

* [在 Direct3D 9 中编写 HLSL 着色器](https://msdn.microsoft.com/library/windows/desktop/bb944006)
* [创建针对 UWP 的新的 DirectX 11 项目](user-interface.md)

**阴影映射技术文章**

* [改进阴影深度映射的常见技术](https://msdn.microsoft.com/library/windows/desktop/ee416324)
* [级联阴影映射](https://msdn.microsoft.com/library/windows/desktop/ee416307)

 

 






<!--HONumber=Mar16_HO1-->


