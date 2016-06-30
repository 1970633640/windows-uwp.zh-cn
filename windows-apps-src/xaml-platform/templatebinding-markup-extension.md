---
author: jwmsft
description: "将一个控件模板中的属性值链接到模板控件上的某个其他公开的属性的值。 TemplateBinding 只能在 XAML 中的 ControlTemplate 定义中使用。"
title: "TemplateBinding 标记扩展"
ms.assetid: FDE71086-9D42-4287-89ED-8FBFCDF169DC
translationtype: Human Translation
ms.sourcegitcommit: 6530fa257ea3735453a97eb5d916524e750e62fc
ms.openlocfilehash: 1a8006e58391c41568731810d9b1901474e8d18f

---

# {TemplateBinding} 标记扩展

\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

将一个控件模板中的属性值链接到模板控件上的某个其他公开的属性的值。 **TemplateBinding** 只能在 XAML 中的 [**ControlTemplate**](https://msdn.microsoft.com/library/windows/apps/br209391) 定义中使用。

## XAML 属性使用方法

``` syntax
<object propertyName="{TemplateBinding sourceProperty}" .../>
```

## XAML 属性使用方法（针对模板或样式中的 Setter 属性）

``` syntax
<Setter Property="propertyName" Value="{TemplateBinding sourceProperty}" .../>
```

## XAML 值

| 术语 | 说明 |
|------|-------------|
| propertyName | 在 setter 语法中设置的属性的名称。 这必须是一个依赖属性。 |
| sourceProperty | 存在于模板化的类型上的其他依赖属性的名称。 |

## 备注

如果你是自定义控件的作者或者要替换现有控件的控件模板，使用 **TemplateBinding** 是如何定义控件模板的基础部分。 有关详细信息，请参阅[快速入门：控件模板](https://msdn.microsoft.com/library/windows/apps/xaml/hh465374)。

*propertyName* 和 *targetProperty* 常常使用相同的属性名称。 在此情况下，一个控件可以在自身定义一个属性，并将该属性转发到其组件部分之一的直观命名的现有属性。 例如，一个在其结构中合并了 [**TextBlock**](https://msdn.microsoft.com/library/windows/apps/br209652) 的控件（用于显示控件自己的 **Text** 属性）可能包含此 XAML 作为控件模板的一部分： `<TextBlock Text="{TemplateBinding Text}" .... />`

用作源属性值和目标属性值的类型必须匹配。 使用 **TemplateBinding** 时，无法引入转换器。 解析 XAML 时，无法匹配值将导致错误。 如果你需要一个可将详细语法用于模板绑定的转换器，例如： `{Binding RelativeSource={RelativeSource TemplatedParent}, Converter="..." ...}`

尝试在 XAML 中的 [**ControlTemplate**](https://msdn.microsoft.com/library/windows/apps/br209391) 定义外使用 **TemplateBinding** 将导致分析器错误。

在模板化父值还会因为其他绑定而推迟的情况下可以使用 **TemplateBinding**。 **TemplateBinding** 的评估可以等待任何所需运行时绑定都具有值。

**TemplateBinding** 始终是单向绑定。 涉及的这两个属性都必须是依赖属性。

**TemplateBinding** 是标记扩展。 当需要将属性值转义为除文字值或处理程序名称之外的值时，以及当需求更具全局性而不是仅仅将类型转换器放在某些类型或属性上时，通常需要实现标记扩展。 XAML 中的所有标记扩展在其属性语法中都使用“{”和“}”字符，通过此约定，XAML 处理器可以知道标记扩展必须处理属性。

**注意** 在 Windows 运行时 XAML 处理器实现中，**TemplateBinding** 没有支持类表示。 **TemplateBinding** 专用于 XAML 标记中。 无法通过一种简单的方式来重现代码中的行为。

## 相关主题

* [快速入门：控件模板](https://msdn.microsoft.com/library/windows/apps/xaml/hh465374)
* [深入了解数据绑定](https://msdn.microsoft.com/library/windows/apps/mt210946)
* [**ControlTemplate**](https://msdn.microsoft.com/library/windows/apps/br209391)
* [XAML 概述](xaml-overview.md)
* [依赖属性概述](dependency-properties-overview.md)
 




<!--HONumber=Jun16_HO4-->


