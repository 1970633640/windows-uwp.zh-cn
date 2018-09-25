---
author: daneuber
title: 合成阴影
description: 卷影 Api 让你可以添加自定义的动态阴影 UI 内容。
ms.author: jimwalk
ms.date: 07/16/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 84e12d6c3e25a18902aaa55011949dd5b5ff97ca
ms.sourcegitcommit: 232543fba1fb30bb1489b053310ed6bd4b8f15d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2018
ms.locfileid: "4181312"
---
# <a name="shadows-in-windows-ui"></a>Windows UI 中的阴影

[DropShadow](/uwp/api/Windows.UI.Composition.DropShadow)类提供了方法创建一个可以应用于[SpriteVisual](/uwp/api/windows.ui.composition.spritevisual)或[LayerVisual](/uwp/api/windows.ui.composition.layervisual) （视觉效果的子树） 的可配置阴影。 原样习惯可视层中的对象，可以使用 Compositionanimation 动画 DropShadow 的所有属性。

## <a name="basic-drop-shadow"></a>基本投影

若要创建基本卷影，只需创建新 DropShadow，并将它与你 visual 相关联。 阴影默认为矩形。 一组标准的属性都可调整你阴影的外观和感觉。

```cs
var basicRectVisual = _compositor.CreateSpriteVisual();
basicRectVisual.Brush = _compositor.CreateColorBrush(Colors.Blue);
basicRectVisual.Offset = new Vector3(100, 100, 20);
basicRectVisual.Size = new Vector2(300, 300);

var basicShadow = _compositor.CreateDropShadow();
basicShadow.BlurRadius = 25f;
basicShadow.Offset = new Vector3(20, 20, 20);

basicRectVisual.Shadow = basicShadow;
```

![矩形可视基本 DropShadow](images/rectangular-dropshadow.png)

## <a name="shaping-the-shadow"></a>影响阴影

有几种方法，为你 DropShadow 定义形状：

- **使用默认设置**-默认情况下 DropShadow 形状由 CompositionDropShadowSourcePolicy 上的默认模式定义。 SpriteVisual，默认值为矩形，除非提供了一个掩码。 LayerVisual，默认值为继承使用视觉对象的画笔的 alpha 蒙板。
- **设置掩码**– 可能设置[掩码](/uwp/api/windows.ui.composition.dropshadow.mask)属性，以定义不透明蒙板的阴影。
- **指定要使用继承掩码**– 设置要使用[CompositionDropShadowSourcePolicy](/uwp/api/windows.ui.composition.compositiondropshadowsourcepolicy) [SourcePolicy](/uwp/api/windows.ui.composition.dropshadow.sourcepolicy)属性。 若要使用生成的视觉对象的画笔的 alpha 蒙板 InheritFromVisualContent。

## <a name="masking-to-match-your-content"></a>掩码，以匹配你的内容

如果你希望你的卷影以匹配视觉对象的内容可以使用视觉对象的画笔阴影掩码属性，或设置自动从内容继承掩码的阴影。 如果使用 LayerVisual，阴影将继承掩码，默认情况下。

```cs
var imageSurface = LoadedImageSurface.StartLoadFromUri(new Uri("ms-appx:///Assets/myImage.png"));
var imageBrush = _compositor.CreateSurfaceBrush(imageSurface);

var imageSpriteVisual = _compositor.CreateSpriteVisual();
imageSpriteVisual.Size = new Vector2(400,400);
imageSpriteVisual.Offset = new Vector3(100, 500, 20);
imageSpriteVisual.Brush = imageBrush;

var shadow = _compositor.CreateDropShadow();
shadow.Mask = imageBrush;
// or use shadow.SourcePolicy = CompositionDropShadowSourcePolicy.InheritFromVisualContent;
shadow.BlurRadius = 25f;
shadow.Offset = new Vector3(20, 20, 20);

imageSpriteVisual.Shadow = shadow;
```

![带屏蔽的投影的连接的 web 图像](images/ms-brand-web-dropshadow.png)

## <a name="using-an-alternative-mask"></a>使用备用掩码

在某些情况下，你可能想要形状阴影，以便它与视觉对象的内容不匹配。 若要实现此效果，你将需要显式设置使用具有 alpha 的画笔的掩码属性。

在以下示例中，我们加载两个表面-一个用于的视觉内容和一个用于阴影掩码：

```cs
var imageSurface = LoadedImageSurface.StartLoadFromUri(new Uri("ms-appx:///Assets/myImage.png"));
var imageBrush = _compositor.CreateSurfaceBrush(imageSurface);

var circleSurface = LoadedImageSurface.StartLoadFromUri(new Uri("ms-appx:///Assets/myCircleImage.png"));
var customMask = _compositor.CreateSurfaceBrush(circleSurface);

var imageSpriteVisual = _compositor.CreateSpriteVisual();
imageSpriteVisual.Size = new Vector2(400,400);
imageSpriteVisual.Offset = new Vector3(100, 500, 20);
imageSpriteVisual.Brush = imageBrush;

var shadow = _compositor.CreateDropShadow();
shadow.Mask = customMask;
shadow.BlurRadius = 25f;
shadow.Offset = new Vector3(20, 20, 20);

imageSpriteVisual.Shadow = shadow;
```

![具有圆形屏蔽投影的连接的 web 图像](images/ms-brand-web-masked-dropshadow.png)

## <a name="animating"></a>动态显示

是标准可视化层中，因此 DropShadow 属性可进行动画处理使用合成动画。 在下面，我们修改上方进行动画处理的阴影的模糊半径喷洒示例中的代码。

```cs
ScalarKeyFrameAnimation blurAnimation = _compositor.CreateScalarKeyFrameAnimation();
blurAnimation.InsertKeyFrame(0.0f, 25.0f);
blurAnimation.InsertKeyFrame(0.7f, 50.0f);
blurAnimation.InsertKeyFrame(1.0f, 25.0f);
blurAnimation.Duration = TimeSpan.FromSeconds(4);
blurAnimation.IterationBehavior = AnimationIterationBehavior.Forever;
shadow.StartAnimation("BlurRadius", blurAnimation);
```

## <a name="shadows-in-xaml"></a>在 XAML 中的阴影

如果你想要为更复杂的框架元素添加阴影，有几种方法，为具有阴影 XAML 和合成之间的互操作：

1. 使用 Windows 社区工具包中[DropShadowPanel](https://github.com/Microsoft/UWPCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.UI.Controls/DropShadowPanel/DropShadowPanel.Properties.cs) 。 有关如何使用它，请参阅[DropShadowPanel 文档](https://docs.microsoft.com/windows/uwpcommunitytoolkit/controls/DropShadowPanel)获取详细信息。
1. 创建一个可视，用于将用作阴影主机和将其绑定到 XAML handout 视觉对象。
1. 使用合成示例库[SamplesCommon](https://github.com/Microsoft/WindowsUIDevLabs/tree/master/SamplesCommon/SamplesCommon)自定义 CompositionShadow 控件。 请参阅此处的示例用法。

## <a name="performance"></a>性能

尽管可视化层中的位置来使效果高效且可用有许多优化，但生成阴影可能的耗费资源的操作，具体取决于你设置的选项。 下面是高级别成本不同类型的阴影。 请注意，但是某些阴影可能不太昂贵它们可能仍需要在某些情况下尽量少使用。

卷影特性| 成本
------------- | -------------
“矩形”    | 低
Shadow.Mask      | 高 
CompositionDropShadowSourcePolicy.InheritFromVisualContent | 高 
静态模糊半径 | 低
模糊半径进行动画处理 | 高 

## <a name="additional-resources"></a>其他资源

- [合成 DropShadow API](/uwp/api/Windows.UI.Composition.DropShadow)
- [WindowsUIDevLabs GitHub 存储库](https://github.com/Microsoft/WindowsUIDevLabs)