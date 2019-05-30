---
description: 列出用于 Windows 运行时的 XAML 中对公共语言运行时 (CLR) 或 C++ 等其他编程语言中某些数据类型的语言级支持。
title: XAML 固有数据类型
ms.assetid: D50E6127-395D-4E27-BAA2-2FE627F4B711
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: dd8bd8f80be068af92d679795431cf9a938fd5f6
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372956"
---
# <a name="xaml-intrinsic-data-types"></a>XAML 固有数据类型


用于 Windows 运行时的 XAML 为多种数据类型提供了语言级支持，这些类型是公共语言运行时 (CLR) 和其他编程语言（例如 C++）中的常用原语。

XAML 固有数据类型在使用上的最大共同点体现于资源在 XAML 资源词典中定义时。 此时你可以定义常数，例如用于多个值的数字。 或者，你也可能使用通过布尔值或字符串构建动画的情节提要动画，随后还需一个用于表示该布尔值或字符串的 XAML 对象元素，以填写 [**ObjectAnimationUsingKeyFrames**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.ObjectAnimationUsingKeyFrames) 定义的关键帧。 Windows 运行时默认 XAML 模板同时采用这两种技术。

用于 Windows 运行时的 XAML 提供了对以下类型的语言级支持。

| XAML 原语 | 描述 |
|-------|-------------|
| **x:Boolean**  | 对于 CLR 支持，对应于 [**Boolean**](https://docs.microsoft.com/dotnet/api/system.boolean?redirectedfrom=MSDN)。 XAML 分析 **x:Boolean** 的值时区分大小写。 请注意，“x:Bool”不是可接受的替代原语。 |
| **x:String**   | 对于 CLR 支持来说，原语对应于 [**String**](https://docs.microsoft.com/dotnet/api/system.string?redirectedfrom=MSDN)。 对字符串的编码默认采用包围 XML 编码。 |
| **x:Double**   | 对于 CLR 支持，对应于 [**Double**](https://docs.microsoft.com/dotnet/api/system.double?redirectedfrom=MSDN)。 除了数字值，**x:Double** 的文本语法支持令牌“NaN”，这是将布局行为的“Auto”存储为资源值的方式。 对这些令牌的处理区分大小写。 你可以使用科学计数法，例如将 `1,000,000` 记为“1+E06”。 |
| **x:Int32**    | 对于 CLR 支持，对应于 [**Int32**](https://docs.microsoft.com/dotnet/api/system.int32?redirectedfrom=MSDN)。 **x:Int32** 被视为带有符号，你可以为负整数包含减号（“-”）。 在 XAML 中，文本语法中缺少符号表示有符号正值。 |

这些 XAML 语言原语一般是在 XAML 中定义使用 **x:** 前缀的对象元素的唯一情形。 所有其他 XAML 语言特性通常以属性或标记扩展的形式使用。

**请注意**  按照约定，XAML 和所有其他 XAML 语言元素的语言基元显示与"x:"前缀。 这是在真实标记中使用 XAML 语言元素的典型方式。 XAML 文档和 XAML 规范中都采用了这一惯例。

## <a name="other-xaml-primitives"></a>其他 XAML 原语

XAML 2009 规范还介绍了其他 XAML 语言级原语，例如 **x:Uri** 和 **x:Single**。 除本节表格中所列项目外，适用于 Windows 运行时的 XAML 当前不支持其他 XAML 词汇表或 XAML 2009 规格所定义的 XAML 语言原语。

**请注意**  日期和时间 (使用的属性[ **DateTime** ](https://docs.microsoft.com/uwp/api/Windows.Foundation.DateTime)或者[ **DateTimeOffset**](https://docs.microsoft.com/dotnet/api/system.datetimeoffset?redirectedfrom=MSDN)， [**时间跨度**](https://docs.microsoft.com/uwp/api/Windows.Foundation.TimeSpan)或[ **System.TimeSpan**](https://docs.microsoft.com/dotnet/api/system.timespan?redirectedfrom=MSDN)) 不是使用 XAML 基元设置。 总体而言，这些属性根本不可以采用 XAML 设置，因为 Windows 运行时 XAML 分析程序中没有用于日期和时间的从字符串转换的默认行为。 若要获取任何日期和时间属性的初始化值，必须使用在页面或元素加载时运行的代码隐藏文件。

## <a name="related-topics"></a>相关主题

* [XAML概述](xaml-overview.md)
* [XAML 语法指南](xaml-syntax-guide.md)
* [可形成演示图板动画](https://docs.microsoft.com/windows/uwp/graphics/storyboarded-animations)
 

