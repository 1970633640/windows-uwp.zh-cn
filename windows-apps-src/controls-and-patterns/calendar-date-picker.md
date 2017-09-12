---
author: Jwmsft
Description: "日历日期选取器是一个下拉式控件，该控件已针对从日历视图中选取某个日期进行了优化，尤其是能够显示诸如星期几或丰富的日历信息等上下文信息。"
title: "日历日期选取器"
ms.assetid: 9e0213e0-046a-4906-ba86-0b49be51ca99
label: Calendar date picker
template: detail.hbs
ms.author: jimwalk
ms.date: 05/19/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, uwp
pm-contact: kisai
design-contact: ksulliv
dev-contact: joyate
doc-status: Published
ms.openlocfilehash: 88f60f60f272fb5501eb6c238cb0d9e5c01986a1
ms.sourcegitcommit: 10d6736a0827fe813c3c6e8d26d67b20ff110f6c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2017
---
# <a name="calendar-date-picker"></a>日历日期选取器

<link rel="stylesheet" href="https://az835927.vo.msecnd.net/sites/uwp/Resources/css/custom.css"> 

日历日期选取器是一个下拉式控件，该控件已针对从日历视图中选取某个日期进行了优化，尤其是能够显示诸如星期几或丰富的日历信息等上下文信息。 你可以修改日历以提供其他上下文或限制可用日期。

> **重要 API**：[CalendarDatePicker 类](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.aspx)、[Date 属性](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.date.aspx)、[DateChanged 事件](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.datechanged.aspx)


## <a name="is-this-the-right-control"></a>这是正确的控件吗？
使用**日历日期选取器**，让用户从上下文日历视图中选取某个日期。 将它用于选择约会或出发日期等事项。

若要让用户选取日历上下文不重要的已知日期，例如生日，请考虑使用[日期选取器](date-picker.md)。

有关选择正确控件的详细信息，请参阅[日期和时间控件](date-and-time.md)文章。

## <a name="examples"></a>示例

如果尚未设置日期，入口点将显示占位符文本；否则，它将显示选择的日期。 当用户选择该入口点时，日历视图将进行扩展以供用户选择日期。 日历视图将会覆盖其他 UI；它不会将其他 UI 推开。

![日历日期选取器示例](images/calendar-date-picker-2-views.png)

## <a name="create-a-date-picker"></a>创建日期选取器

```xaml
<CalendarDatePicker x:Name="arrivalCalendarDatePicker" Header="Arrival date"/>
```

```csharp
CalendarDatePicker arrivalCalendarDatePicker = new CalendarDatePicker();
arrivalCalendarDatePicker.Header = "Arrival date";
```

生成的日历日期选取器如下所示：

![日历日期选取器示例](images/calendar-date-picker-closed.png)

日历日期选取器具有用于选取日期的内部 [CalendarView](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendarview.aspx)。 CalendarView 属性的子集（例如 [IsTodayHighlighted](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.istodayhighlighted.aspx) 和 [FirstDayOfWeek](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.firstdayofweek.aspx)）存在于 CalendarDatePicker 上，并且会转发到内部 CalendarView 以供你修改。 

但是，你无法更改内部 CalendarView 的 [SelectionMode](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendarview.selectionmode.aspx) 以支持多项选择。 如果你需要让用户选取多个日期或需要日历始终可见，请考虑使用日历视图而非日历日期选取器。 有关如何修改日历屏幕的详细信息，请参阅[日历视图](calendar-view.md)文章。

### <a name="selecting-dates"></a>选择日期

使用 [Date](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.date.aspx) 属性获取或设置选定的日期。 默认情况下，Date 属性设置为 **null**。 当用户在日历视图中选择某个日期时，此属性即已更新。 用户可清除该日期，方法是在日历视图中单击选择的日期以取消选择。 

你可以在代码中像这样来设置日期。

```csharp
myCalendarDatePicker.Date = new DateTime(1977, 1, 5);
```

当在代码中设置 Date 时，值会受到 [MinDate](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.mindate.aspx) 和 [MaxDate](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.maxdate.aspx) 属性的限制。
- 如果 **Date** 小于 **MinDate**，则该值将设置为 **MinDate**。
- 如果 **Date** 大于 **MaxDate**，则该值将设置为 **MaxDate**。

可处理 [DateChanged](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.datechanged.aspx) 事件，以在 Date 值更改时收到通知。

> [!NOTE]
有关日期值的重要信息，请参阅日期和时间控件一文中的 [Datetime 和日历值](date-and-time.md#datetime-and-calendar-values)。

### <a name="setting-a-header-and-placeholder-text"></a>设置标题和占位符文本

你可以将 [Header](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.header.aspx)（或标签）和 [PlaceholderText](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.placeholdertext.aspx)（或水位线）添加到日历日期选取器，以向用户指示其用途。 若要自定义标题外观，可设置 [HeaderTemplate](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.calendardatepicker.headertemplate.aspx) 属性而非 Header。

默认占位符文本是“选择日期”。 你可以通过将 PlaceholderText 属性设置为空字符串来删除此文本，或提供自定义文本，如下所示。

```xaml
<CalendarDatePicker x:Name="arrivalCalendarDatePicker" Header="Arrival date" 
                    PlaceholderText="Choose your arrival date"/>
```

## <a name="get-the-sample-code"></a>获取示例代码
* [XAML UI 基本示例](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/XamlUIBasics)


## <a name="related-articles"></a>相关文章

- [日期和时间控件](date-and-time.md)
- [日历视图](calendar-view.md)
- [日期选取器](date-picker.md)
- [时间选取器](time-picker.md)
