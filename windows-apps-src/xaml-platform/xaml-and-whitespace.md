---
description: 了解 XAML 中使用的空格处理规则。
title: XAML 与空格
ms.assetid: 025F4A8E-9479-4668-8AFD-E20E7262DC24
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 521e794680df6449ebc49745319c4aeec74405d1
ms.sourcegitcommit: b11f305dbf7649c4b68550b666487c77ea30d98f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "7837111"
---
# <a name="xaml-and-whitespace"></a>XAML 与空格


了解 XAML 中使用的空格处理规则。

## <a name="whitespace-processing"></a>空格处理

与 XML，在 XAML 中的空格字符是空白、 换行和制表符。它们分别对应于 Unicode 值 0020、 000A 和 0009。 默认情况下，在 XAML 处理器遇到 XAML 文件中各元素之间的任何内部文本时，会执行以下空格规范化操作：

-   删除东亚字符之间的换行字符。
-   将所有空格字符（空白、换行、制表符）转换为空白。
-   删除所有连续的空格并替换为一个空格。
-   删除紧挨起始标记之后的空格。
-   删除紧挨结束标记之前的空格。
-   *东亚字符*定义为从 U+20000 到 U+2FFFD 和从 U+30000 到 U+3FFFD 的 Unicode 字符集。 这个子集有时也称为“CJK 象形文字”**。 有关详细信息，请参阅 http://www.unicode.org。

“默认”对应于 **xml:space** 属性的默认值所表示的状态。

### <a name="whitespace-in-inner-text-and-string-primitives"></a>内部文本中的空格和字符串原语

上面的规范化规则适用于 XAML 元素中的内部文本。 规范化后，一个 XAML 处理器将任何内部文本转换为合适的类型，如下所示：

-   如果属性的类型不是集合，但也不是一种直接的 **Object** 类型，XAML 处理器将尝试使用它的转换器转换为该类型。 此处失败的转换将导致 XAML 分析错误。
-   如果属性的类型是一个集合，并且内部文本是连续的（中间没有元素标记），内部文本会分析为单个 **String**。 如果集合类型不能接受 **String**，这也会导致 XAML 分析器错误。
-   如果属性的类型是 **Object**，那么内部文本会分析为单个 **String**。 如果中间没有元素标记，这将导致 XAML 分析器错误，因为 **Object** 类型标识单个对象（**String** 或其他对象）。
-   如果属性类型是一个集合，并且内部文本不是连续的，那么第一个子字符串转换为一个 **String** 并添加为一个集合项，中间元素添加为一个集合项，最后的结尾子字符串（如果有）作为第三个 **String** 项添加到集合中。

### <a name="whitespace-and-text-content-models"></a>空格和文本内容模型

在实际中，保留空格仅是所有可能的内容模型的一个子集。 该子集包含可接受某种形式的单独 **String** 类型的内容模型、一个专用的 **String** 集合，或者 **String** 和列表、集合或词典中的其他类型的组合。

甚至对于可接受字符串的内容模型，这些内容模型内的默认行为也不会重视任何保留的空格。

### <a name="preserving-whitespace"></a>保留空格

可以采用多种技术在源 XAML 中保留空格，使最终表示不会受 XAML 处理器空格规范化的影响。

`xml:space="preserve"`：在希望保留空格的元素级别上指定此属性。 请注意，这会保留所有空格，包括可能由代码编辑器或设计界面添加的，使标记元素以一种直观嵌套方式对齐的空格。 是否显示这些空格由包含元素的内容模型负责。 我们不建议在根级别指定 `xml:space="preserve"`，因为大部分对象模型都不会将空格视为一种重要的方式。 一种更好的做法是，仅在呈现字符串内的空格的元素级别上专门设置该属性，或者在空格很重要的集合中设置该属性。

实体和不间断空白：XAML 支持在一个文本对象模型中放置任何 Unicode 实体。 你可以使用专门的实体，例如不间断空白（在 UTF-8 编码中）。 你也可以使用支持不间断空白字符的富文本控件。 如果使用实体来模拟缩进等布局字符，请保持谨慎，因为不同于一般的布局工具（例如面板和边距的适当使用），基于大量因素，实体的运行时输出将不同。

