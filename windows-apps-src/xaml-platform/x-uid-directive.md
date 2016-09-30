---
author: jwmsft
description: "为标记元素提供一个唯一标识符。 对于通用 Windows 平台 (UWP) XAML，这个唯一标识符供 XAML 本地化过程和工具使用（例如，使用 .resw 资源文件中的资源）。"
title: "xUid 指令"
ms.assetid: 9FD6B62E-D345-44C6-B739-17ED1A187D69
translationtype: Human Translation
ms.sourcegitcommit: 6530fa257ea3735453a97eb5d916524e750e62fc
ms.openlocfilehash: 4f8aa553c99b6071cedc4f9d93cf8258b75eca49

---

# x&#58;Uid 指令

\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 的文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

为标记元素提供一个唯一标识符。 对于通用 Windows 平台 (UWP) XAML，这个唯一标识符供 XAML 本地化过程和工具使用（例如，使用 .resw 资源文件中的资源）。

## XAML 属性使用方法

``` syntax
<object x:Uid="stringID".../>
```

## XAML 值

| 术语 | 说明 |
|------|-------------|
| stringID | 一个唯一标识应用中的 XAML 元素并且是资源文件中资源路径一部分的字符串。 请参阅备注。| 

## 备注

使用 **x:Uid** 可以标识 XAML 中的对象元素。 此对象元素通常是 UI 中显示的控件类或其他元素的实例。 用在 **x:Uid** 中的字符串与用在资源文件中的字符串之间的关系是：资源文件字符串包括 **x:Uid**，其后面是一个点 (.)，然后是正本地化的元素的特定属性名。 考虑此示例：

``` syntax
<Button x:Uid="GoButton" Content="Go"/>
```

若要指定要替换显示文本**“Go”**的内容，必须指定来自资源文件的新资源。 资源文件中应当包含一个与名为“GoButton.Content”的资源相对应的条目。 在本例中，[**Content**](https://msdn.microsoft.com/library/windows/apps/br209366) 是由 [**Button**](https://msdn.microsoft.com/library/windows/apps/br209265) 类继承的特定属性。 你还可以为该按钮的其他属性提供本地化值，例如，可以为“GoButton.FlowDirection”提供基于资源的值。 有关如何将 **x:Uid** 与资源文件一起使用的详细信息，请参阅[快速入门：翻译 UI 资源](https://msdn.microsoft.com/library/windows/apps/xaml/hh965329)。

在实际意义上，要证明哪些字符串可用于 **x:Uid** 值，这取决于哪些字符串是 resw 文件和资源路径中的合法标识符。

在规定的 XAML 本地化场景中，**x:Uid** 与 **x:Name** 是分离的，所以用于本地化的标识符对 **x:Name** 的编程模型含义没有任何依赖性。 而且，**x:Name** 由 XAML 名称范围这一概念控制，而 **x:Uid** 的唯一性由数据包资源索引 (PRI) 系统来控制。 有关详细信息，请参阅[资源管理系统](https://msdn.microsoft.com/library/windows/apps/jj552947)。

UWP XAML 在 **x:Uid** 唯一性上使用的规则不同于以前利用 XAML 的技术所使用的规则。 对于 UWP XAML，在多个 XAML 元素上使用相同的 **x:Uid** ID 值作为指令是合法的。 但是，每个这样的元素必须在解析资源文件中的资源时共享相同的解析逻辑。 另外，一个项目中的所有 XAML 文件共享一个资源范围来解析 **x:Uid**，因此没有针对各个 XAML 文件的 **x:Uid** 范围概念。

在某些情况下，你将使用资源路径，而不是数据包资源索引 (PRI) 系统的内置功能。 用作 **x:Uid** 值的任何字符串都会定义一个资源路径，该路径以 ms-resource:///Resources/ 开头并包括 **x:Uid** 字符串。 该路径以你在资源文件中指定的属性名或者在其他情况下作为目标的属性名结尾。

请勿将 **x:Uid** 放在属性元素上，Windows 运行时 XAML 中不允许这样做。




<!--HONumber=Jun16_HO4-->


