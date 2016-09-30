---
author: DelfCo
Description: "通过适当设置日期、时间、数字和货币的格式，开发全球通用的应用。"
title: "使用全球通用的格式"
ms.assetid: 6ECE8BA4-9A7D-49A6-81EE-AB2BE7F0254F
label: Use global-ready formats
template: detail.hbs
translationtype: Human Translation
ms.sourcegitcommit: 59e02840c72d8bccda7e318197e4bf45ed667fa4
ms.openlocfilehash: 77b5e7bd412936dd5d8c4bc252771631d6b884cf

---

# <span id="dev_globalizing.use_global-ready_formats"></span>使用全球通用的格式





**重要的 API**

-   [**Windows.Globalization.Calendar**](https://msdn.microsoft.com/library/windows/apps/br206724)
-   [**Windows.Globalization.DateTimeFormatting**](https://msdn.microsoft.com/library/windows/apps/br206859)
-   [**Windows.Globalization.NumberFormatting**](https://msdn.microsoft.com/library/windows/apps/br226136)

通过适当设置日期、时间、数字和货币的格式，开发全球通用的应用。 你可以在以后对此进行调整，以适应全球市场中更多的文化、区域和语言。

## <span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


许多应用开发者在创建他们的应用时，自然只考虑了他们自己的语言和文化。 但当应用开始发展到其他市场时，使应用适应新语言和区域可能非常困难。 例如，日期、时间、数字、日历、货币、电话号码、度量单位和纸张大小的显示都会因文化或语言的不同而有所不同。

如果在开发应用时考虑一些事项，则能够简化适应新市场的过程。

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


[针对全球市场进行规划](https://msdn.microsoft.com/library/windows/apps/hh465405)
## <span id="Tasks"></span><span id="tasks"></span><span id="TASKS"></span>任务


1.  **设置相应的日期和时间格式。**

    有很多不同的显示日期和时间的方法。 不同区域和文化在以下方面的使用惯例不同：日期中的日和月顺序、时间中的小时和分钟的分隔，甚至用作分隔符的标点符号。 此外，可以采用各种长格式（“星期三，2012 年 3 月 28 日”）或短格式（“12/3/28”）显示日期，这些格式因文化而异。 当然，年份中的星期和月份的名称和缩写也因语言而异。

    如果你需要允许用户选择日期或选择时间，请使用标准的[日期和时间选取器](https://msdn.microsoft.com/library/windows/apps/hh465466)控件。 它们将会自动针对用户的首选语言和区域使用日期和时间格式。

    如果你需要自己显示日期或时间，则使用 [**Date/Time**](https://msdn.microsoft.com/library/windows/apps/br206859) 和 [**Number**](https://msdn.microsoft.com/library/windows/apps/br226136) 格式化程序来自动显示用户首选的日期、时间和数字格式。 以下代码将使用首选语言和区域设置给定 DateTime 的格式。 例如，如果当前日期为 2012 年 6 月 3 日，则格式化程序将生成“6/3/2012”（如果用户首选英语(美国)），但如果用户首选德语(德国)，则为“03.06.2012”：

    **C#**
    ```    CSharp
    // Use the Windows.Globalization.DateTimeFormatting.DateTimeFormatter class
    // to display dates and times using basic formatters.

    // Formatters for dates and times, using shortdate format.
    var sdatefmt = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("shortdate");
    var stimefmt = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("shorttime");

    // Obtain the date that will be formatted.
    var dateToFormat = DateTime.Now;

    // Perform the actual formatting.
    var sdate = sdatefmt.Format(dateToFormat);
    var stime = stimefmt.Format(dateToFormat);

    // Results for display.
    var results = "Short Date: " + sdate + "\n" +
                  "Short Time: " + stime;
    ```
    **JavaScript**
    ```    JavaScript
    // Use the Windows.Globalization.DateTimeFormatting.DateTimeFormatter class
    // to display dates and times using basic formatters.

    // Formatters for dates and times, using shortdate format.
    var sdatefmt = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("shortdate");
    var stimefmt = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("shorttime");

    // Obtain the date that will be formatted.
    var dateToFormat = new Date();

    // Perform the actual formatting.
    var sdate = sdatefmt.format(dateToFormat);
    var stime = stimefmt.format(dateToFormat);

    // Results for display.
    var results = "Short Date: " + sdate + "\n" +
                  "Short Time: " + stime;
    ```

2.  **设置相应的数字和货币格式。**

    不同的文化设置数字格式的方式也不相同。 格式差异可能包括显示多少小数位数、什么字符用作小数分隔符以及要使用什么货币符号。 使用 [**NumberFormatting**](https://msdn.microsoft.com/library/windows/apps/br226136) 来显示小数、分数、千分比和货币。 多数情况下，你只是根据用户的当前首选项来显示数字或货币。 但是你也可以使用格式化程序显示某个特殊的区域或格式的货币。

    以下代码提供了如何根据用户首选语言和区域或针对特定的给定货币系统显示货币的示例：

    **C#**
    ```    CSharp
    // This scenario uses the Windows.Globalization.NumberFormatting.CurrencyFormatter class
    // to format a number as a currency.

    // Determine the current user's default currency.
    var userCurrency = Windows.System.UserProfile.GlobalizationPreferences.Currencies[0];

    // Number to be formatted.
    var fractionalNumber = 12345.67;

    // Currency formatter using the current user's preference settings for number formatting.
    var userCurrencyFormat = new Windows.Globalization.NumberFormatting.CurrencyFormatter(userCurrency);
    var currencyDefault = userCurrencyFormat.Format(fractionalNumber);

    // Create a formatter initialized to a specific currency,
    // in this case US Dollar (specified as an ISO 4217 code) 
    // but with the default number formatting for the current user.
    var currencyFormatUSD = new Windows.Globalization.NumberFormatting.CurrencyFormatter("USD"); 
    var currencyUSD = currencyFormatUSD.Format(fractionalNumber);

    // Create a formatter initialized to a specific currency.
    // In this case it's the Euro with the default number formatting for France.
    var currencyFormatEuroFR = new Windows.Globalization.NumberFormatting.CurrencyFormatter("EUR", new[] { "fr-FR" }, "FR");
    var currencyEuroFR = currencyFormatEuroFR.Format(fractionalNumber);

    // Results for display.
    var results = "Fixed number (" + fractionalNumber + ")\n" +
                  "With user's default currency: " + currencyDefault + "\n" +
                  "Formatted US Dollar: " + currencyUSD + "\n" +
                  "Formatted Euro (fr-FR defaults): " + currencyEuroFR;
    ```
    **JavaScript**
    ```    JavaScript
    // This scenario uses the Windows.Globalization.NumberFormatting.CurrencyFormatter class
    // to format a number as a currency.

    // Determine the current user's default currency.
    var userCurrency = Windows.System.UserProfile.GlobalizationPreferences.currencies;

    // Number to be formatted.
    var fractionalNumber = 12345.67;

    // Currency formatter using the current user's preference settings for number formatting.
    var userCurrencyFormat = new Windows.Globalization.NumberFormatting.CurrencyFormatter(userCurrency);
    var currencyDefault = userCurrencyFormat.format(fractionalNumber);

    // Create a formatter initialized to a specific currency,
    // in this case US Dollar (specified as an ISO 4217 code) 
    // but with the default number formatting for the current user.
    var currencyFormatUSD = new Windows.Globalization.NumberFormatting.CurrencyFormatter("USD"); 
    var currencyUSD = currencyFormatUSD.format(fractionalNumber);

    // Create a formatter initialized to a specific currency.
    // In this case it's the Euro with the default number formatting for France.
    var currencyFormatEuroFR = new Windows.Globalization.NumberFormatting.CurrencyFormatter("EUR", ["fr-FR"], "FR");
    var currencyEuroFR = currencyFormatEuroFR.format(fractionalNumber);

    // Results for display.
    var results = "Fixed number (" + fractionalNumber + ")\n" +
                  "With user's default currency: " + currencyDefault + "\n" +
                  "Formatted US Dollar: " + currencyUSD + "\n" +
                  "Formatted Euro (fr-FR defaults): " + currencyEuroFR;
    ```

3.  **使用与文化相对应的日历。**

    日历因区域和语言而异。 并非每一个区域都使用公历作为默认日历。 某些区域的用户可能选择其他日历，例如日本历或伊斯兰历。 日历上的日期和时间还对不同的时区和夏令时敏感。

    使用标准的[日期和时间选取器](https://msdn.microsoft.com/library/windows/apps/hh465466)控件可允许用户选择日期，从而确保使用首选的日历格式。 对于可能需要对日历日期直接操作的更加复杂的方案，Windows.Globalization 提供了一个 [**Calendar**](https://msdn.microsoft.com/library/windows/apps/br206724) 类，该类为给定的文化、区域和日历类型提供相应的日历表示。

4.  **尊重用户的语言和文化首选项。**

    对于基于用户的语言、区域或文化首选项提供不同功能的方案，Windows 为你提供了一种访问这些首选项的方法：通过 [**Windows.System.UserProfile.GlobalizationPreferences**](https://msdn.microsoft.com/library/windows/apps/br241825)。 需要时，使用 **GlobalizationPreferences** 类获取用户当前地理区域、首选语言、首选货币等项目的值。

## <span id="related_topics"></span>相关主题


* [针对全球市场进行规划](https://msdn.microsoft.com/library/windows/apps/hh465405)
* [日期和时间控件指南](https://msdn.microsoft.com/library/windows/apps/hh465466)

**引用**
* [**Windows.Globalization.Calendar**](https://msdn.microsoft.com/library/windows/apps/br206724)
* [**Windows.Globalization.DateTimeFormatting**](https://msdn.microsoft.com/library/windows/apps/br206859)
* [**Windows.Globalization.NumberFormatting**](https://msdn.microsoft.com/library/windows/apps/br226136)
* [**Windows.System.UserProfile.GlobalizationPreferences**](https://msdn.microsoft.com/library/windows/apps/br241825)

**示例**
* [日历详细信息和数学示例](http://go.microsoft.com/fwlink/p/?linkid=231636)
* [设置日期和时间格式示例](http://go.microsoft.com/fwlink/p/?linkid=231618)
* [全球化首选项示例](http://go.microsoft.com/fwlink/p/?linkid=231608)
* [数字格式和分析示例](http://go.microsoft.com/fwlink/p/?linkid=231620)
 

 






<!--HONumber=Jun16_HO4-->


