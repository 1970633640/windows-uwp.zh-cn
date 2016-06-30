---
author: mcleblanc
ms.assetid: 83b4be37-6613-4d00-a48a-0451a24a30fb
title: "数据绑定"
description: "数据绑定是你的应用 UI 用来显示数据的一种方法，可以选择与该数据保持同步。"
translationtype: Human Translation
ms.sourcegitcommit: 6530fa257ea3735453a97eb5d916524e750e62fc
ms.openlocfilehash: d1fbc7376b3505d39e757a1b65ae0f0890948078

---

# 数据绑定

\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

数据绑定是你的应用 UI 用来显示数据的一种方法，可以选择与该数据保持同步。 借助数据绑定，你可以将关注的数据从关注的 UI 中分离开来，从而可形成一个更简易的概念模型，并且使你的应用拥有更好的可读性、可测试性和可维护性。 在标记中，你既可以选用 [{x:Bind} 标记扩展](https://msdn.microsoft.com/library/windows/apps/Mt204783)，也可以选用 [{Binding} 标记扩展](https://msdn.microsoft.com/library/windows/apps/Mt204782)。 还可以在同一应用中（甚至是同一 UI 元素上）混合使用这两个标记扩展。 {x:Bind} 是 Windows 10 的新增内容，且具备更好的性能。 {Binding} 具有更多功能。

| 主题 | 说明 |
|-------|-------------|
| [数据绑定概述](data-binding-quickstart.md) | 本主题介绍了如何在通用 Windows 平台 (UWP) 应用中将控件（或其他 UI 元素）绑定到单个项目，或者将项目控件绑定到项目集合。 此外，我们还介绍了如何控制项的呈现、基于所选内容实现详细信息视图，以及转换数据以供显示。 有关更多详细信息，请参阅[深入了解数据绑定](data-binding-in-depth.md)。 | 
| [深入了解数据绑定](data-binding-in-depth.md) | 数据绑定是你的应用 UI 用来显示数据的一种方法，可以选择与该数据保持同步。 借助数据绑定，你可以将关注的数据从关注的 UI 中分离开来，从而可形成一个更简易的概念模型，并且使你的应用拥有更好的可读性、可测试性和可维护性。 |
| [设计面图上以及用于原型制作的示例数据](displaying-data-in-the-designer.md) | 你的应用可能无法或不需要（可能是出于隐私或性能的原因）在 Microsoft Visual Studio 或 Blend for Visual Studio 中的设计图面上显示实时数据。 为了使你的控件填充数据（以便你可以处理应用的布局、模板和其他视觉属性），你可以通过各种方式使用设计时示例数据。 如果你正要生成一个草图（或原型）应用，则示例数据可能真的非常有用而且节省时间。 你可以在运行时在草图或原型中使用示例数据来阐明你的想法，而无需连接到真实且实时的数据。 |
| [绑定分层数据和创建大纲/细节视图](how-to-bind-to-hierarchical-data-and-create-a-master-details-view.md) | 你可以通过将项目控件绑定到 [<strong>CollectionViewSource</strong>](https://msdn.microsoft.com/library/windows/apps/BR209833) 实例（它们绑定在同一个链中）来生成分层数据的多级大纲/细节（也称为列表详细信息）视图。 |




<!--HONumber=Jun16_HO4-->


