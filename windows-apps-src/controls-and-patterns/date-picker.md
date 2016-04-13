---
Description: 日期选取器向你提供了一种标准化方式，可使用户通过触摸、鼠标或键盘输入选取本地化格式的日期值。 
title: 日期选取器
ms.assetid: d4a01425-4dee-4de3-9a05-3e85c3fc03cb
isNew: true
label: Date picker
template: detail.hbs
---

# 日期选取器

日期选取器向你提供了一种标准化方式，可使用户通过触摸、鼠标或键盘输入选取本地化格式的日期值。 

<span class="sidebar_heading" style="font-weight: bold;">重要的 API</span>

-   [**DatePicker 类**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.datepicker.aspx)
-   [**Date 属性**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.datepicker.date.aspx)

## 这是正确的控件吗？
使用日期选取器以使用户选取日历上下文不重要的已知日期，例如生日。

有关选择正确日期控件的详细信息，请参阅[日期和时间控件](date-and-time.md)文章。

## 示例

入口点显示选定的日期，当用户选择该入口点时，会从中间垂直展开一个选取器图面以供用户进行选择。 日期选取器会覆盖其他 UI；它不会将其他 UI 推开。

![日期选取器展开示例](images/controls_datepicker_expand.png)

## 创建日期选取器

本示例演示如何创建附带标头的简单日期选取器。

```xaml
<DatePicker x:Name=birthDatePicker Header="Date of birth"/>
```

```csharp
DatePicker birthDatePicker = new DatePicker();
birthDatePicker.Header = "Date of birth";
```

生成的日期选取器如下所示：

![日期选取器示例](images/date-picker-closed.png)

> **注意** 对于日期值的重要信息，请参阅“日期和时间控件”文章中的 [DateTime 和 Calendar 值](date-and-time.md#datetime-and-calendar-values)。



## 相关文章

- [日期和时间控件](date-and-time.md)
- [日历日期选取器](calendar-date-picker.md)
- [日历视图](calendar-view.md)
- [时间选取器](time-picker.md)


<!--HONumber=Mar16_HO4-->


