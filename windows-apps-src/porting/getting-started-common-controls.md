---
ms.assetid: E2B73380-D673-48C6-9026-96976D745017
description: 常见控件入门
title: 常见控件入门
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: a64dbd6a9530f81c55b0d4b52e4c0fd55c4b9956
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372830"
---
# <a name="getting-started-common-controls"></a>入门：公共控件


## <a name="common-controls-list"></a>常见控件列表

在前面的部分中，你仅使用了两个控件：按钮和文本块。 有，当然，可供您的许多其他控件。 下面是一些可在你的应用和与其等效的 iOS 中使用的常用控件。 iOS 控件按字母顺序列出，后跟最为相似的通用 Windows 平台 (UWP) 控件。

UWP 控件相当智能的方面是，它们可以感知到在其上运行的设备类型，并相应地更改外观和功能。 例如，如果项目使用 [**DatePicker**](https://docs.microsoft.com/previous-versions/windows/apps/br211681(v=win.10)) 控件，能够优化自身以在桌面计算机上呈现不同于手机上的外观和行为，这就足够智能。 你无需执行任何操作，因为控件会在运行时对自身进行调整。

| iOS 控件（类/协议） | 等效的 UWP 控件 |
|------------------------------|--------------------------------------|
| 活动指示器 (**UIActivityIndicatorView**) | [**ProgressRing**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ProgressRing) <br/> 另请参阅[快速入门：添加进度控件](https://docs.microsoft.com/previous-versions/windows/apps/hh780651(v=win.10)) |
| 广告横幅视图 (**ADBannerView**) 和广告横幅视图委托 (**ADBannerViewDelegate**) | [AdControl](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol) <br/> 另请参阅[在应用中显示广告](../monetize/display-ads-in-your-app.md) |
| 按钮 (UIButton) | [Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button) <br/> 另请参阅[快速入门：添加按钮控件](https://docs.microsoft.com/previous-versions/windows/apps/jj153346(v=win.10)) |
| 日期选取器 (UIDatePicker) | [DatePicker](https://docs.microsoft.com/previous-versions/windows/apps/br211681(v=win.10)) |
| 图像视图 (UIDatePicker) | [Image](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Image) <br/> 另请参阅[图像和 ImageBrush](https://docs.microsoft.com/windows/uwp/controls-and-patterns/images-imagebrushes) |
| 标签 (UILabel) | [TextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) <br/> 另请参阅[快速入门：显示文本](https://docs.microsoft.com/previous-versions/windows/apps/hh700392(v=win.10)) |
| 地图视图 (MKMapView) 和地图视图委派 (MKMapViewDelegate) | 请参阅[必应地图适用于 UWP 应用](https://go.microsoft.com/fwlink/p/?LinkId=263496) |
| 导航控制器 (UINavigationController) 和导航控制器委托 (UINavigationControllerDelegate) | [帧](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame) <br/> 另请参阅[导航](https://docs.microsoft.com/windows/uwp/layout/navigation-basics) |
| 页面控件 (UIPageControl) | [页](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) <br/> 另请参阅[导航](https://docs.microsoft.com/windows/uwp/layout/navigation-basics) |
| 选取器视图 (UIPickerView) 和选取器视图委托 (UIPickerViewDelegate) | [ComboBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ComboBox) <br/> 另请参阅[添加组合框和列表框](https://docs.microsoft.com/previous-versions/windows/apps/hh780616(v=win.10)) |
| 进度条 (UIProgressView) | [ProgressBar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ProgressBar) <br/> 另请参阅[快速入门：添加进度控件](https://docs.microsoft.com/previous-versions/windows/apps/hh780651(v=win.10)) |
| 滚动视图 (UIScrollView) 和滚动视图委托 (UIScrollViewDelegate) | [ScrollViewer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer) <br/>  另请参阅[Extensible Application Markup Language (XAML) 滚动、平移以及缩放示例](https://go.microsoft.com/fwlink/p/?LinkId=238577) |
| 搜索栏 (UISearchBar) 和搜索栏委派 (UISearchBarDelegate) | 请参阅[向应用添加搜索](https://docs.microsoft.com/previous-versions/windows/apps/jj130767(v=win.10)) <br/>  另请参阅[快速入门：将搜索添加到应用程序](https://docs.microsoft.com/previous-versions/windows/apps/hh868180(v=win.10)) |
| 分段控件 (UISegmentedControl) | 无 |
| 滑块 (UISlider) | [滑块](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Slider) <br/>  另请参阅[如何添加滑块](https://docs.microsoft.com/previous-versions/windows/apps/hh868197(v=win.10)) |
| 拆分视图控制器 (UISplitViewController) 和拆分视图控制器委派 (UISplitViewControllerDelegate) | 无 |
| 开关 (UISwitch) | [ToggleSwitch](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToggleSwitch) <br/>  另请参阅[如何添加切换开关](https://docs.microsoft.com/previous-versions/windows/apps/hh868198(v=win.10)) |
| 选项卡栏控制器 (UITabBarController) 和选项卡栏控制器委派 (UITabBarControllerDelegate) | 无 |
| 表视图控制器 (UITableViewController)、表视图 (UITableView)、表视图委托 (UITableViewDelegate) 和表单元格 (UITableViewCell) | [ListView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListView) <br/>  另请参阅[快速入门：添加 ListView 和 GridView 控件](https://docs.microsoft.com/previous-versions/windows/apps/hh780650(v=win.10)) |
| 文本字段 (UITextField) 和文本字段委托 (UITextFieldDelegate) | [TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) <br/>  另请参阅[显示和编辑文本](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/text-controls) |
| 文本视图 (UITextView) 和文本视图委托 (UITextViewDelegate) | [TextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) <br/>  另请参阅[快速入门：显示文本](https://docs.microsoft.com/previous-versions/windows/apps/hh700392(v=win.10)) |
| 视图 (UIView) 和视图控制器 (UIViewController) | [页](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) <br/>  另请参阅[导航](https://docs.microsoft.com/windows/uwp/layout/navigation-basics) |
| Web 视图 (UIWebView) 和 Web 视图委托 (UIWebViewDelegate) | [WebView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.WebView) <br/>  另请参阅 [XAML WebView 控件示例](https://go.microsoft.com/fwlink/p/?LinkId=238582) |
| 窗口 (UIWindow) | [帧](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame) <br/>  另请参阅[导航](https://docs.microsoft.com/windows/uwp/layout/navigation-basics) |

有关其他更多控件，请参阅[控件列表](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/)。

**请注意**  使用 JavaScript 和 HTML 的 UWP 应用的控件的列表，请参阅[控件列表](https://docs.microsoft.com/previous-versions/windows/apps/hh465453(v=win.10))。

### <a name="next-step"></a>下一步

[入门：导航](getting-started-navigation.md)

## <a name="related-topics"></a>相关主题

* [生成 2014年中：XAML UI 和控件呢？](https://go.microsoft.com/fwlink/p/?LinkID=397897)
* [生成 2014年中：开发应用程序使用通用的 XAML UI 框架](https://go.microsoft.com/fwlink/p/?LinkID=397898)
* [生成 2014年中：使用 Visual Studio 构建 XAML 融合应用](https://go.microsoft.com/fwlink/p/?LinkID=397876)
