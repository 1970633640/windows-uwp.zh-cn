---
title: 诊断 Windows 运行时组件错误条件
description: 本文提供了有关用托管代码编写的 Windows 运行时组件的限制的其他信息。
ms.assetid: CD0D0E11-E68A-411D-B92E-E9DECFDC9599
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ab1ad2054288c38498eb1077a924531d3e22c0dd
ms.sourcegitcommit: d38e2f31c47434cd6dbbf8fe8d01c20b98fabf02
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70393704"
---
# <a name="diagnosing-windows-runtime-component-error-conditions"></a>诊断 Windows 运行时组件错误条件

本文提供了有关用托管代码编写的 Windows 运行时组件的限制的其他信息。 它扩展了[Winmdexp （Windows 运行时元数据导出工具）](https://docs.microsoft.com/dotnet/framework/tools/winmdexp-exe-windows-runtime-metadata-export-tool)中的错误消息中提供的信息，并对 Windows 运行时组件中提供的限制[ C#和视觉对象的信息进行了补充。基本](creating-windows-runtime-components-in-csharp-and-visual-basic.md)。

本文没有涵盖所有错误。 此处讨论的错误按照常规类别分组，并且每个类别包括关联的错误消息表。 请搜索消息文本（省略占位符的特定值）或搜索消息编号。 如果你在此处没有找到所需信息，请使用本文末尾的“反馈”按钮帮助我们改进这篇文档。 包括错误消息。 或者，你可以在 Microsoft Connect 网站上提交 Bug。

## <a name="error-message-for-implementing-async-interface-provides-incorrect-type"></a>实现异步接口的错误消息提供错误类型

托管 Windows 运行时组件无法实现表示异步操作或操作的通用 Windows 平台（UWP）接口（[IAsyncAction](https://docs.microsoft.com/windows/desktop/api/windows.foundation/nn-windows-foundation-iasyncaction)， [iasyncactionwithprogress<tprogress>&lt;TProgress&gt; ](https://docs.microsoft.com/previous-versions/br205784(v=vs.85))、 [Iasyncoperation<tresult>&lt;tresult&gt;](https://docs.microsoft.com/uwp/api/Windows.Foundation.IAsyncOperation_TResult_)或[IAsyncOperationWithProgress&gt;TResult、TProgress）。&lt;](https://docs.microsoft.com/uwp/api/Windows.Foundation.IAsyncOperationWithProgress_TResult_TProgress_) 而 .NET 提供了[system.runtime.interopservices.windowsruntime.asyncinfo](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime?redirectedfrom=MSDN)类用于在 Windows 运行时组件中生成异步操作。 Winmdexp.exe 在你错误地尝试实现异步接口时显示的错误消息使用之前的名称 AsyncInfoFactory 引用此类。 .NET 不再包括 System.runtime.interopservices.windowsruntime.asyncinfofactory 类。

| 错误编号 | 消息文本|       
|--------------|-------------|
| WME1084      | 类型 "{0}" 实现 Windows 运行时 async 接口 "{1}"。 Windows 运行时类型无法实现异步接口。 请使用 System.Runtime.InteropServices.WindowsRuntime.AsyncInfoFactory 类生成用于导出到 Windows 运行时的异步操作。 |

> **请注意** 引用 Windows 运行时使用旧术语的错误消息。 这现在称为通用 Windows 平台 (UWP)。 例如，Windows 运行时类型现在称为 UWP 类型。

## <a name="missing-references-to-mscorlibdll-or-systemruntimedll"></a>缺少对 mscorlib.dll 或 System.Runtime.dll 的引用

此问题仅在从命令行使用 Winmdexp.exe 时发生。 建议使用/reference 选项同时包含对 mscorlib.dll .NET Framework 和 ProgramFiles 的引用，这些程序集位于 "% （x86）% reference 程序集" 中，后者位于 "% （x86）%\\reference 程序集\\Microsoft\\Framework。\\NETCore\\4.5 "（"% ProgramFiles%\\... "在32位计算机上）。

| 错误编号 | 消息文本                                                                                                                                     |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1009      | 没有对 mscorlib.dll 的引用。 正确导出需要引用此元数据文件。                               |
| WME1090      | 无法确定核心引用程序集。 请确保使用 /reference 开关引用 mscorlib.dll 和 System.Runtime.dll。 |

## <a name="operator-overloading-is-not-allowed"></a>不允许运算符重载

在使用托管代码编写的 Windows 运行时组件中，无法在公共类型上公开重载的运算符。

> **请注意** ，在错误消息中，运算符由其元数据名称标识，如 op\_加法、op\_乘法、op\_ExclusiveOr、op\_隐性（隐式转换）等。

| 错误编号 | 消息文本                                                                                          |
|--------------|-------------------------------------------------------------------------------------------------------|
| WME1087      | "{0}" 是运算符重载。 托管的类型无法在 Windows 运行时中公开运算符重载。 |

## <a name="constructors-on-a-class-have-the-same-number-of-parameters"></a>类上的构造函数具有相同数量的参数

在 UWP 中，类只能拥有带有指定数量参数的一个构造函数；例如，不能是一个构造函数具有类型 **String** 的单个参数，而另一个构造函数具有类型 **int**（在 Visual Basic 中是 **Integer**）的单个参数。 唯一的解决方法是为每个构造函数使用不同数量的参数。

| 错误编号 | 消息文本                                                                                                                                            |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1099      | 类型 "{0}" 具有多个带有 "{1}" 参数的构造函数。 Windows 运行时类型无法具有多个带有相同数量的参数的构造函数。 |

## <a name="must-specify-a-default-for-overloads-that-have-the-same-number-of-parameters"></a>必须为具有相同数量的参数的重载指定默认值。

在 UWP 中，重载的方法仅在一个重载指定为默认重载时才能具有相同数量的参数。 请参阅[Windows 运行时带有C# and Visual Basic 的组件](creating-windows-runtime-components-in-csharp-and-visual-basic.md)中的 "重载方法"。

| 错误编号 | 消息文本                                                                                                                                                                      |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1059      | " {0}."{2}的多参数重载通过 windows.foundation.metadata.defaultoverloadattribute 进行修饰。{1}                                                            |
| WME1085      | 的-参数{1}重载。{2}必须有一个指定为默认重载的方法，方法是使用 windows.foundation.metadata.defaultoverloadattribute 进行修饰。 {0} |

## <a name="namespace-errors-and-invalid-names-for-the-output-file"></a>输出文件的命名空间错误和无效名称

在通用 Windows 平台中，Windows 元数据 (.winmd) 文件中的所有公共类型必须位于共享 .winmd 文件名的命名空间或文件名的子命名空间中。 例如，如果你的 Visual Studio 项目名称为 A.B（即，Windows 运行时组件为 A.B.winmd），它可以包含公共类 A.B.Class1 和 A.B.C.Class2，但无法包含 A.Class3 (WME0006) 或 D.Class4 (WME1044)。

> **请注意**  ，这些限制仅适用于公共类型，不适用于实现中使用的私有类型。

对于 A.Class3，你可以将 Class3 移动到其他命名空间或将 Windows 运行时组件的名称更改为 A.winmd。 虽然 WME0006 是一条警告，但应该将其视为错误。 在之前的示例中，调用 A.B.winmd 的代码将无法找到 A.Class3。

对于 D.Class4，没有任何文件名可以包含 D.Class4 和 A.B 命名空间中的类，因此不可选择更改 Windows 运行时组件的名称。 你可以将 D.Class4 移到其他命名空间，或将其置于其他 Windows 运行时组件中。

文件系统无法区分大小写，因此使用大小写区分的命名空间将不受允许 (WME1067)。

组件必须包含至少一种 **public sealed** 类型（在 Visual Basic 中是 **Public NotInheritable**）。 如果未包含，你将会收到 WME1042 或 WME1043，具体取决于组件是否包含私有类型。

Windows 运行时组件中的类型无法具有与命名空间相同的名称 (WME1068)。

> **警告如果你**直接调用 Winmdexp，而不使用/out 选项来指定 Windows 运行时组件的名称，Winmdexp 将尝试生成一个包括组件中所有命名空间的名称。   为命名空间重命名会更改组件的名称。

 

| 错误编号 | 消息文本                                                                                                                                                                                                                                                                                                                                             |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME0006      | "{0}" 不是此程序集的有效 winmd 文件名。 Windows 元数据文件中的所有类型必须存在于由文件名暗示的命名空间的子命名空间中。 未存在于此类子命名空间中的类型无法在运行时找到。 在此程序集中，能够充当文件名的最小常见命名空间是“{1}”。 |
| WME1042      | 输入模块必须包含至少一种位于命名空间内的公共类型。                                                                                                                                                                                                                                                                   |
| WME1043      | 输入模块必须包含至少一种位于命名空间内的公共类型。 仅在命名空间内找到的类型为专有类型。                                                                                                                                                                                                               |
| WME1044      | 公共类型具有不与其他命名空间{1}（"{0}"）共享公共前缀的命名空间（""）。 Windows 元数据文件中的所有类型必须存在于由文件名暗示的命名空间的子命名空间中。                                                                                                                              |
| WME1067      | 命名空间名称不能仅通过大小写{0}来区分：{1}""、""。                                                                                                                                                                                                                                                                                                |
| WME1068      | 类型 "{0}" 不能与命名空间 "{1}" 具有相同的名称。                                                                                                                                                                                                                                                                                                 |

## <a name="exporting-types-that-arent-valid-universal-windows-platform-types"></a>导出无效的通用 Windows 平台类型

组件的公共接口必须仅公开 UWP 类型。 但是，.NET 提供了许多常用类型的映射，这些类型在 .NET 和 UWP 中略有不同。 这使 .NET 开发人员能够使用熟悉的类型，而不是学习新的类型。 可以在组件的公共接口中使用这些映射的 .NET 类型。 请参阅[包含C#和 Visual Basic Windows 运行时组件](creating-windows-runtime-components-in-csharp-and-visual-basic.md)中的 "在 Windows 运行时组件中声明类型" 和 "将通用 Windows 平台类型传递给托管代码"; [Windows 运行时类型的 .net 映射](net-framework-mappings-of-windows-runtime-types.md)。

其中许多映射都是接口。 例如，[IList&lt;T&gt;](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?redirectedfrom=MSDN) 映射到 UWP 接口 [IVector&lt;T&gt;](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.IVector_T_)。 如果将 List&lt;string&gt;（在 Visual Basic 中是 `List(Of String)`）而非 IList&lt;string&gt; 用作参数类型，Winmdexp.exe 会提供包括所有由 List&lt;T&gt; 实现的映射接口的备用项列表。 如果使用嵌套的泛型类型，例如 List&lt;Dictionary&lt;int, string&gt;&gt;（在 Visual Basic 中是 List(Of Dictionary(Of Integer, String))），Winmdexp.exe 会提供有关每个级别的嵌套的选项。 这些列表会非常长。

通常情况下，最好选择最接近类型的接口。 例如，对于 Dictionary&lt;int, string&gt;，最好选择最接近的 IDictionary&lt;int, string&gt;。

> **重要 JavaScript 使用**托管类型实现的接口列表中首先出现的接口。   例如，如果你将 Dictionary&lt;int, string&gt; 返回到 JavaScript 代码，它会显示为 IDictionary&lt;int, string&gt;，无论你指定哪个接口作为返回类型都是如此。 这意味着，如果第一个接口不包括显示在后续接口上的成员，JavaScript 将看不到该成员。

> 注意  如果你的组件将由 JavaScript 使用，则应避免使用非泛型[IList](https://docs.microsoft.com/dotnet/api/system.collections.ilist?redirectedfrom=MSDN)和[IEnumerable](https://docs.microsoft.com/dotnet/api/system.collections.ienumerable?redirectedfrom=MSDN)接口。 这些接口分别映射到 [IBindableVector](https://docs.microsoft.com/uwp/api/windows.ui.xaml.interop.ibindablevector) 和 [IBindableIterator](https://docs.microsoft.com/uwp/api/windows.ui.xaml.interop.ibindableiterator)。 它们支持绑定 XAML 控件，并对 JavaScript 不可见。 JavaScript 提出运行时错误“函数‘X’签名无效且无法调用。”

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误号</th>
<th align="left">消息文本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WME1033</td>
<td align="left">方法 "{0}" 具有类型为{1}"{2}" 的参数 ""。 “{2}”不是有效的 Windows 运行时参数类型。</td>
</tr>
<tr class="even">
<td align="left">WME1038</td>
<td align="left">方法 "{0}" 的签名中具有类型为{1}"" 的参数。 尽管此类型并非有效的 Windows 运行时类型，但它可以实现作为有效的 Windows 运行时类型的接口。 请考虑更改方法签名以改为使用以下类型之一：“{2}”。</td>
</tr>
<tr class="odd">
<td align="left">WME1039</td>
<td align="left"><p>方法 "{0}" 的签名中具有类型为{1}"" 的参数。 尽管此泛型类型并非有效的 Windows 运行时类型，但类型或其泛型参数可以实现作为有效的 Windows 运行时类型的接口。 {2}</p>
> **** &lt;请注意  ，Winmdexp 将在方法签名中追加替代项的列表，如 "请考虑将方法签名中的类型"&gt; {2}类型："&lt;System.object&lt;t，IReadOnlyList&lt;t&gt;，，system.object&gt;t，... a i t，"。&gt;
</td>
</tr>
<tr class="even">
<td align="left">WME1040</td>
<td align="left">方法 "{0}" 的签名中具有类型为{1}"" 的参数。 使用 Windows.Foundation.IAsyncAction、Windows.Foundation.IAsyncOperation 或其他 Windows 运行时异步接口之一，而非使用托管的任务类型。 标准 .NET await 模式也适用于这些接口。 有关将托管的任务对象转换为 Windows 运行时异步接口的详细信息，请参阅 System.Runtime.InteropServices.WindowsRuntime.AsyncInfo。</td>
</tr>
</tbody>
</table>

 

## <a name="structures-that-contain-fields-of-disallowed-types"></a>包含禁止类型的字段的结构


在 UWP 中，结构仅可以包含字段，并仅结构可以包含字段。 这些字段必须是公共字段。 有效字段类型包括枚举、结构和基元类型。

| 错误编号 | 消息文本                                                                                                                                                                                                                                                            |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1060      | 结构 "{0}" 具有类型为{1}"{2}" 的字段 ""。 “{2}”不是有效的 Windows 运行时字段类型。 Windows 运行时结构中的每个字段仅可以是 UInt8、Int16、UInt16、Int32、UInt32、Int64、UInt64、单精度、双精度、布尔值、字符串、Enum，或其本身就是结构。 |

 

## <a name="restrictions-on-arrays-in-member-signatures"></a>对成员签名中数组的限制


在 UWP 中，成员签名中的数组必须是一维数组，并且下限为 0（零）。 不允许嵌套的数组类型，例如 `myArray[][]`（在 Visual Basic 中是 `myArray()()`）。

> **请注意** ，此限制不适用于在实现内部使用的数组。

 

| 错误编号 | 消息文本                                                                                                                                                     |
|--------------|--------------------|
| WME1034      | 方法 "{0}" 的签名中具有类型为{1}"" 的数组，其下限为非零。 Windows 运行时方法签名中数组的下限必须为零。 |
| WME1035      | 方法 "{0}" 在其签名中具有类型为 "{1}" 的多维数组。 Windows 运行时方法签名中的数组必须是一维数组。                  |
| WME1036      | 方法 "{0}" 的签名中具有类型为 "{1}" 的嵌套数组。 Windows 运行时方法签名中的数组无法嵌套。                                    |

 

## <a name="array-parameters-must-specify-whether-array-contents-are-readable-or-writable"></a>数组参数必须指定数组内容是可读还是可写。


在 UWP 中，参数必须是只读或只写。 参数无法标记 **ref**（在 Visual Basic 中是缺少 [OutAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.outattribute?redirectedfrom=MSDN) 属性的 **ByRef**）。 这适用于数组内容，因此数组参数必须指示数组内容是只读还是只写。 **out** 参数（在 Visual Basic 中是带有 OutAttribute 属性的 **ByRef** 参数）具有清晰的方向，但必须标记通过值（在 Visual Basic 中是 ByVal）传递的数组参数。 请参阅[将数组传递到 Windows 运行时组件](passing-arrays-to-a-windows-runtime-component.md)。

| 错误编号 | 消息文本         |
|--------------|----------------------|
| WME1101      | 方法 "{0}" 具有作为数组{1}的参数 ""，并且它同时{2}具有和{3}。 在 Windows 运行时中，数组参数内容必须是可读或可写。 请从“{1}”中删除其中一个属性。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| WME1102      | 方法 "{0}" 的输出参数 "{1}" 是一个数组，但它具有{2}。 在 Windows 运行时中，可写入输出数组的内容。 请从“{1}”中删除该属性。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| WME1103      | 方法 "{0}" 具有作为数组{1}的参数 ""，并且该参数具有 InteropServices 或 InAttribute 或 InteropServices。 system.runtime.interopservices.outattribute。 在 Windows 运行时中，数组参数必须具有 {2} 或 {3}。 请删除这些属性，或使用相应的 Windows 运行时属性替换它们（如有必要）。                                                                                                                                                                                                                                                                                                                                                                                          |
| WME1104      | 方法 "{0}" 的参数 "{1}" 不是数组， {2}并且{3}具有或。 Windows 运行时不支持使用 {2} 或 {3} 标记非数组参数。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| WME1105      | 方法 "{0}" 中的参数{1}"" 具有 InteropServices 或 InAttribute 或 InteropServices system.runtime.interopservices.outattribute。 Windows 运行时不支持使用 System.Runtime.InteropServices.InAttribute 或 System.Runtime.InteropServices.OutAttribute 标记参数。 请考虑删除 System.Runtime.InteropServices.InAttribute，并改为使用“out”修饰符替换 System.Runtime.InteropServices.OutAttribute。 方法 "{0}" 中的参数{1}"" 具有 InteropServices 或 InAttribute 或 InteropServices system.runtime.interopservices.outattribute。 Windows 运行时仅支持使用 System.Runtime.InteropServices.OutAttribute 标记 ByRef 参数，不支持这些属性的其他用法。 |
| WME1106      | 方法 "{0}" 具有作为数组{1}的参数 ""。 在 Windows 运行时中，数组参数的内容必须是可读或可写。 请将 {2} 或 {3} 应用到“{1}”。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |


## <a name="member-with-a-parameter-named-value"></a>具有名为“value”的参数的成员


在 UWP 中，将返回值视为输出参数，并且参数名称必须唯一。 默认情况下，Winmdexp.exe 将返回值命名为“value”。 如果方法具有名为“value”的参数，将收到错误 WME1092。 有两种方法可以更正此错误：

-   将参数命名为除“value”之外的名称（在属性访问器中，使用除“returnValue”之外的名称）。
-   使用 ReturnValueNameAttribute 属性更改返回值的名称，如下所示：

    > [!div class="tabbedCodeSnippets"]
    > ```cs
    > using System.Runtime.InteropServices;
    > using System.Runtime.InteropServices.WindowsRuntime;
    >
    > [return: ReturnValueName("average")]
    > public int GetAverage(out int lowValue, out int highValue)
    > ```
    > ```vb
    > Imports System.Runtime.InteropServices
    > Imports System.Runtime.InteropServices.WindowsRuntime
    >
    > Public Function GetAverage(<Out> ByRef lowValue As Integer, _
    > <Out> ByRef highValue As Integer) As <ReturnValueName("average")> String
    > ```

> **注意如果更改**返回值的名称，并且新名称与另一个参数的名称冲突，则会出现错误 WME1091。  

JavaScript 代码可以按照名称访问方法的输出参数，包括返回值。 有关示例，请参阅 [ReturnValueNameAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime.returnvaluenameattribute?redirectedfrom=MSDN) 属性。

| 错误编号 | 消息文本 |
|--------------|--------------|
| WME1091 | 方法 "\{0}" 具有名为 "\{1}" 的返回值，该返回值与参数名称相同。 Windows 运行时方法参数和返回值的名称必须唯一。 |
| WME1092 | 方法 "\{0}" 具有名为 "\{1}" 的参数，该参数与默认返回值名称相同。 请考虑将其他名称用于参数，或使用 System.Runtime.InteropServices.WindowsRuntime.ReturnValueNameAttribute 显式指定返回值的名称。 |

**请注意**  ，属性访问器的默认名称为 "returnValue"，对于所有其他方法，默认名称为 "value"。

## <a name="related-topics"></a>相关主题

* [用C#和 Visual Basic Windows 运行时组件](creating-windows-runtime-components-in-csharp-and-visual-basic.md)
* [Winmdexp （Windows 运行时元数据导出工具）](https://docs.microsoft.com/dotnet/framework/tools/winmdexp-exe-windows-runtime-metadata-export-tool)
