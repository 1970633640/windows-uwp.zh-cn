---
description: Binding 标记扩展会在 XAML 加载时转换为 Binding 类的实例。
title: Binding 标记扩展'
ms.assetid: 3BAFE7B5-AF33-487F-9AD5-BEAFD65D04C3
---

# {Binding} 标记扩展

\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

**注意** 新的绑定机制可用于 Windows 10，该机制已针对性能和开发人员工作效率进行优化。 请参阅 [{x:Bind} 标记扩展](x-bind-markup-extension.md)。

**注意** 有关将应用中的数据绑定与 **{Binding}** 结合使用的常规信息（以及有关 **{x:Bind}** 和 **{Binding}** 之间的全方位比较），请参阅[深入了解数据绑定](https://msdn.microsoft.com/library/windows/apps/mt210946)。

**{Binding}** 标记扩展会在 XAML 加载时转换为 [**Binding**](https://msdn.microsoft.com/library/windows/apps/br209820) 类的实例。 此绑定对象将从数据源的某一属性中获取相关值。 绑定对象可以配置为观察数据源属性值的更改，并基于这些更改自行刷新。 该对象也可以配置为将其自己的值的更改推送回源属性。 作为数据绑定目标的属性必须是依赖属性。 有关详细信息，请参阅[依赖属性概述](dependency-properties-overview.md)。

**{Binding}** 具有与本地值相同的依赖属性优先级，而在强制性代码中设置本地值将删除在标记中设置的任何 **{Binding}**。

**用于演示 {Binding} 的应用示例**

-   下载 [Bookstore1](http://go.microsoft.com/fwlink/?linkid=532950) 应用。
-   下载 [Bookstore2](http://go.microsoft.com/fwlink/?linkid=532952) 应用。

## XAML 属性使用方法


``` syntax
<object property="{Binding}" .../>
-or-
<object property="{Binding propertyPath}" .../>
-or-
<object property="{Binding bindingProperties}" .../>
-or-
<object property="{Binding propertyPath, bindingProperties}" .../>
```

| 术语 | 说明 |
|------|-------------|
| *propertyPath* | 一个指定绑定的属性路径的字符串。 下面的[属性路径](#property-path)部分中提供了更多信息。 |
| *bindingProperties* | *propName*=*value*\[, *propName*=*value*\]*<br/>使用一个名称/值对语法指定的一个或多个绑定属性。 |
| *propName* | 要在 [**Binding**](https://msdn.microsoft.com/library/windows/apps/br209820) 对象上设置的属性的字符串名称。 例如，“Converter”。 | 
| *value* | 要将属性设置为的值。 参数的语法取决于下面的[可使用 {Binding} 设置的 Binding 类的属性](#properties-of-binding)部分的属性。 |

## 属性路径

*PropertyPath* 设置 [**Path**](https://msdn.microsoft.com/library/windows/apps/br209830) 的值，后者是你要绑定到的属性（源属性）。 你可以明确指出属性名称：`{Binding Path=...}`。 也可以将其省略：`{Binding ...}`。

[
            **Path**](https://msdn.microsoft.com/library/windows/apps/br209830) 类型为属性路径，其求值结果为自定义类型或框架类型的属性或子属性的字符串。 该类型可能是（但并不一定是）[**DependencyObject**](https://msdn.microsoft.com/library/windows/apps/br242356)。 属性路径中的步骤由点号 (.) 分隔，并且可包含多个分隔符以遍历连续的子属性。 无论使用何种编程语言，均可将点号分隔符用于实现要绑定到的对象。

例如，若要将 UI 绑定到员工对象的第一个名称属性，属性路径可能是“Employee.FirstName”。 如果将一个项目控件绑定到一个包含员工家属的属性，则属性路径可能是“Employee.Dependents”，并且项目控件的项目模板将负责显示“Dependents”中的项。

如果数据源是一个集合，则属性路径可以按照位置或索引来指定集合中的项目。 例如“Teams\[0\].Players”，其中文本“\[\]”中包含 “0”，用于指定集合中的第一个项目。

当使用绑定到现有 [**DependencyObject**](https://msdn.microsoft.com/library/windows/apps/br242356) 的 [**ElementName**](https://msdn.microsoft.com/library/windows/apps/br209828) 时，你可以使用附加属性作为属性路径的一部分。 若要消除附加属性的多义性，以使附加属性名称中的中间点不被视为属性路径中的一个步骤，可以将所有者限定的附加属性名称放在圆括号中；例如 `(AutomationProperties.Name)`。

属性路径中间对象作为 [**PropertyPath**](https://msdn.microsoft.com/library/windows/apps/br244259) 对象存储在运行时表示形式中，但大多数情况不需要与代码中的 **PropertyPath** 对象交互。 通常，可以使用 XAML 来指定所需的绑定信息。

有关属性路径的字符串语法、动画功能区域中的属性路径和构造 [**PropertyPath**](https://msdn.microsoft.com/library/windows/apps/br244259) 对象的详细信息，请参阅 [Property-path 语法](property-path-syntax.md)。

## 可使用 {Binding} 设置的 Binding 类的属性


**{Binding}** 通过 *bindingProperties* 占位符语法来解释，因为 [**Binding**](https://msdn.microsoft.com/library/windows/apps/br209820) 中存在多个可在标记扩展中进行设置的读/写属性。 这些属性可按任何顺序设置，并带有以逗号分隔的 *propName*=*value* 对。 由于其中一些属性需要不具有类型转换的类型，因此它们需要一些自己嵌套在 **{Binding}** 内的标记扩展。

| 属性 | 说明 |
|----------|-------------|
| [**Path**](https://msdn.microsoft.com/library/windows/apps/br209830) | 请参阅上面的[属性路径](#property-path)部分。 |
| [**转换器**](https://msdn.microsoft.com/library/windows/apps/br209826) | 指定绑定引擎所调用的转换器对象。 转换器可以在 XAML 中设置，但仅限于你引用你在对资源字典中的该对象的 [{StaticResource} 标记扩展](staticresource-markup-extension.md)引用中分配的对象实例。 |
| [**ConverterLanguage**](https://msdn.microsoft.com/library/windows/apps/hh701880) | 指定转换器要使用的区域性。 （如果要设置 [**Converter**](https://msdn.microsoft.com/library/windows/apps/br209826)。）区域性可设置为一个基于标准的标识符。 有关详细信息，请参阅 **ConverterLanguage** | 
| [**ConverterParameter**](https://msdn.microsoft.com/library/windows/apps/br209827) | 指定可在转换器逻辑中使用的转换器参数。 （如果要设置 [**Converter**](https://msdn.microsoft.com/library/windows/apps/br209826)。）大多数转换器使用可从要转换的传递值获取所有所需信息的简单逻辑，不需要 **ConverterParameter** 值。 **ConverterParameter** 参数适用于具有多个逻辑的中等高级转换器实现，这些逻辑可切断传入 **ConverterParameter** 的内容。 你可以编写一个转换器，使用除字符串之外的值，但这种情况并不常见，请参阅 **ConverterParameter** 中的备注以获取详细信息。 |
| [**ElementName**](https://msdn.microsoft.com/library/windows/apps/br209828) | 通过引用同一个 XAML 构造中的另一个元素（具有 **Name** 属性或 [x:Name 属性](x-name-attribute.md)）来指定数据源。 这种方法通常用于共享相关值，或者使用一个 UI 元素的子属性为另一个元素提供特定值，例如在 XAML 控件模板中。 |
| [**FallbackValue**](https://msdn.microsoft.com/library/windows/apps/dn279345) | 指定要在无法解析源或路径时显示的值。 | 
| [**模式**](https://msdn.microsoft.com/library/windows/apps/br209829) | 将绑定模式指定为以下字符串之一：“OneTime”、“OneWay”或“TwoWay”。 这些模式对应于 [**BindingMode**](https://msdn.microsoft.com/library/windows/apps/br209822) 枚举的常量名称。 默认值取决于绑定目标，但在大多数情况下，该值为“OneWay”。 请注意，该值不是 **{x:Bind}** 的默认值，而是“OneTime”。 | 
| [**RelativeSource**](https://msdn.microsoft.com/library/windows/apps/br209831) | 通过描述绑定来源的位置相对于绑定目标的位置来指定数据源。 这通过运行时对象图表的方式表示，例如指定对象的父级。 设置 [{RelativeSource} 标记扩展](relativesource-markup-extension.md)。 |
| [**源**](https://msdn.microsoft.com/library/windows/apps/br209832) | 指定对象数据源。 在 **Binding** 标记扩展内，[深入了解数据绑定](https://msdn.microsoft.com/library/windows/apps/mt210946)。 |
| [**TargetNullValue**](https://msdn.microsoft.com/library/windows/apps/dn279347) | 指定要在源值解析但并非显式 **null** 时显示的值。 |
| [**UpdateSourceTrigger**](https://msdn.microsoft.com/library/windows/apps/dn279350) | 指定绑定源更新的定时。 如果没有指定，则默认值为 **Default**。 |

**注意** 如果你要将标记从 **{x:Bind}** 转换为 **{Binding}**，请注意在 **Mode** 属性默认值方面的差异。

[
            **Converter**](https://msdn.microsoft.com/library/windows/apps/br209826)、[**ConverterLanguage**](https://msdn.microsoft.com/library/windows/apps/hh701880) 和 **ConverterLanguage** 都与如下方案相关：将绑定源中的值或类型转换为与绑定目标属性兼容的类型或值。 有关详细信息和相关示例，请参阅[深入了解数据绑定](https://msdn.microsoft.com/library/windows/apps/mt210946)的“数据转换”部分。

[
            **Source**](https://msdn.microsoft.com/library/windows/apps/br209832)、[**RelativeSource**](https://msdn.microsoft.com/library/windows/apps/br209831) 和 [**ElementName**](https://msdn.microsoft.com/library/windows/apps/br209828) 都可指定绑定源，因此它们相互排斥。

**提示** 如果你需要为某个值指定单个花括号（例如在 [**Path**](https://msdn.microsoft.com/library/windows/apps/br209830) 或 [**ConverterParameter**](https://msdn.microsoft.com/library/windows/apps/br209827) 中），请在其前面加上反斜杠：`\{`。 此外，将包含需要转义的括号的整个字符串放在第二组引号中，例如 `ConverterParameter='{Mix}'`。

## 示例

```XAML
<!-- binding a UI element to a view model -->    
<Page ... >
    <Page.DataContext>
        <local:BookstoreViewModel/>
    </Page.DataContext>

    <GridView ItemsSource="{Binding BookSkus}" SelectedItem="{Binding SelectedBookSku, Mode=TwoWay}" ... />
</Page>
```

```XAML
<!-- binding a UI element to another UI element -->
<Page ... >
    <Page.Resources>
        <local:S2Formatter x:Key="GradeConverter"/>
    </Page.Resources>

    <Slider x:Name="sliderValueConverter" ... />
    <TextBox Text="{Binding Path=Value, ElementName=sliderValueConverter,
        Mode=OneWay,
        Converter={StaticResource GradeConverter}}"/> 
</Page>
```

第二个示例设置了以下四个不同的 [**Binding**](https://msdn.microsoft.com/library/windows/apps/br209820) 属性：[**ElementName**](https://msdn.microsoft.com/library/windows/apps/br209828)、[**Path**](https://msdn.microsoft.com/library/windows/apps/br209830)、[**Mode**](https://msdn.microsoft.com/library/windows/apps/br209829) 和 [**Converter**](https://msdn.microsoft.com/library/windows/apps/br209826)。 本例中显示的 **Path** 明确命名为 **Binding** 属性。 **Path** 的求值结果是一个数据绑定源，该绑定源是同一个运行时对象树中的另一个对象（即，名为 `sliderValueConverter` 的 [**Slider**](https://msdn.microsoft.com/library/windows/apps/br209614)）。

请注意 [**Converter**](https://msdn.microsoft.com/library/windows/apps/br209826) 属性值如何使用另一个标记扩展 [{StaticResource} 标记扩展](staticresource-markup-extension.md)，以便在这里有两个嵌套标记扩展用法。 内部嵌套先求值，以便在获取资源之后，有一个可以由绑定使用的实际 [**IValueConverter**](https://msdn.microsoft.com/library/windows/apps/br209903)（一个由资源中的 `local:S2Formatter` 元素实例化的自定义类）。

## 工具支持

当在 XAML 标记编辑器中创作 **{Binding}** 时，Microsoft Visual Studio 中的 Microsoft IntelliSense 将显示数据上下文的相关属性。 只要你键入“{Binding”，适合 [**Path**](https://msdn.microsoft.com/library/windows/apps/br209830) 的数据上下文属性便会显示在下拉列表中。 IntelliSense 对 [**Binding**](https://msdn.microsoft.com/library/windows/apps/br209820) 的其他属性也能起到帮助作用。 为实现此操作，你必须在标记页中设置数据上下文或设计时数据上下文。 **“转到定义”**(F12) 也适用于 **{Binding}**。 或者，你也可以使用数据绑定对话框。

 



<!--HONumber=Mar16_HO1-->


