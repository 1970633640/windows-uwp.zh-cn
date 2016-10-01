---
author: mcleanbyron
ms.assetid: 9621641A-7462-425D-84CC-101877A738DA
description: "了解如何在 UWP 应用中从 AdMediatorControl 迁移到 AdControl。"
title: "针对 UWP 应用从 AdMediatorControl 迁移到 AdControl"
translationtype: Human Translation
ms.sourcegitcommit: 07baa54990ec31dc0cb9c289f9f0222754da9d7c
ms.openlocfilehash: 3abef943530cc756de117edccc5ab16e5f178604

---

# 针对 UWP 应用从 AdMediatorControl 迁移到 AdControl

Microsoft 支持的通用 Windows 平台 (UWP) 应用中以前的广告 SDK 版本，通过使用 **AdMediatorControl** 类来显示横幅广告，从而允许开发人员通过显示来自我们的合作伙伴网络（AOL 和 AppNexus）以及 AdDuplex 的横幅广告来优化其广告收益。 [Microsoft Store Services SDK](http://aka.ms/store-em-sdk) 不再支持 **AdMediatorControl** 类。 如果现有应用使用的是之前 SDK 中的 **AdMediatorControl** 类，并且你希望将其迁移到使用 [Microsoft Store Services SDK](http://aka.ms/store-em-sdk) 的 UWP 应用，请按照本文中的说明将代码更新为使用 **AdControl** 类而非 **AdMediatorControl** 类。 你可以选择使用加权或评级方法，将应用配置为使用 AdDuplex 进行广告中介配置。

>**注意**&nbsp;&nbsp;本文中的代码示例仅供演示。 你可能需要对代码示例进行调整，以便在你的应用中运行。

## 先决条件

* 当前正在使用 AdMediatorControl 并且已在 Windows 应用商店中发布的 UWP 应用。
* 装有 Visual Studio 2015 和 [Microsoft Store Services SDK](http://aka.ms/store-em-sdk) 的开发计算机。
* 如果你想要使用 AdDuplex 进行广告中介配置，还必须在开发计算机上安装了 [AdDuplex Windows 10 SDK](https://visualstudiogallery.msdn.microsoft.com/6930860a-e64b-4b46-9d72-62d7fddda077)。

  >**注意**&nbsp;&nbsp;作为从上述链接运行 AdDuplex SDK 安装程序的替代方法，你可以在 Visual Studio 2015 中为你的 UWP 应用项目安装 AdDuplex 库。 在 Visual Studio 2015 中打开 UWP 应用项目后，单击“项目”**** > “管理 NuGet 程序包”****、搜索名为“AdDuplexWin10”****的 NuGet 程序包，然后安装该程序包。

## 步骤 1：检索你的应用程序 ID 和广告单元 ID

迁移代码以使用 **AdControl** 类时，必须知道自己的应用程序 ID 和广告单元 ID。 获取最新 ID 的最佳方法是从中介配置文件中检索它们。

1. 登录到 Windows 开发人员中心仪表板，然后单击当前正在使用 **AdMediatorControl** 的应用。
2. 单击“盈利”****，然后单击“利用广告来盈利”****。
3. 在“Windows 广告中介”****部分中，单击“下载中介配置”****链接，并在文本编辑器（如记事本）中打开 AdMediator.config 文件。
4. 在该文件中，找到具有子元素 ```<Name>MicrosoftAdvertising</Name>``` 的 ```<AdAdapterInfo>``` 元素。 该部分包含用于 Microsoft 付费广告的配置。
5. 在此 ```<AdAdapterInfo>``` 元素中，找到 ```<Property>``` 元素，其中包含值为 **WApplicationId** 和 **WAdUnitId** 的 ```<Key>``` 元素。 在以下示例中，```<Value>``` 元素值即为示例。

  ```xml
  <Metadata>
      <Property>
          <Key>WApplicationId</Key>
          <Value>364d4938-c0f5-4c3d-8aae-090206211dc9</Value>
      </Property>
      <Property>
          <Key>WAdUnitId</Key>
          <Value>301568</Value>
      </Property>
  </Metadata>
  ```
6. 在这些 ```<Value>``` 元素中复制这两个值以供稍后使用。 这些值包含 Microsoft 付费广告的非移动广告单元的应用程序 ID 和广告单元 ID。
5. 在相同的 ```<AdAdapterInfo>``` 元素中，找到 ```<Property>``` 元素，其中包含值为 **MApplicationId** 和 **MAdUnitId** 的 ```<Key>``` 元素。 在以下示例中，```<Value>``` 元素值即为示例。

  ```xml
  <Metadata>
      <Property>
          <Key>MApplicationId</Key>
          <Value>e2cf8388-7018-4a11-8ab0de90f2a7a401</Value>
      </Property>
      <Property>
          <Key>MAdUnitId</Key>
          <Value>301056</Value>
      </Property>
  </Metadata>
  ```
6. 在 ```<Value>``` 元素中复制这两个值以供稍后使用。 这些值包含 Microsoft 付费广告的移动广告单元的应用程序 ID 和广告单元 ID。
7. 如果你使用的是[自家广告](../publish/about-house-ads.md)，请找到具有子元素 ```<Name>MicrosoftAdvertisingHouse</Name>``` 的 ```<AdAdapterInfo>``` 元素。 在此元素中，找到值为 **MAdUnitId** 和 **WAdUnitId** 的 ```<Key>``` 元素，并保存相应的 ```<Value>``` 元素值以供稍后使用。 它们分别是 Microsoft 自家广告的移动和非移动广告单元 ID。
8. 如果你使用 AdDuplex，请找到具有子元素 ```<Name>AdDuplex</Name>``` 的 ```<AdAdapterInfo>``` 元素。 在此元素中，找到值为 **AppKey** 和 **AdUnitId** 的 ```<Key>``` 元素，并保存相应的 ```<Value>``` 元素值以供稍后使用。 这分别是 AdDuplex 应用密钥和广告单元 ID。

## 步骤 2：更新你的应用代码

既然你已拥有应用程序 ID 和广告单元 ID，你可以随时更新应用中的代码，以便使用 **AdControl** 而不是 **AdMediatorControl**。

### 仅 Microsoft 付费广告

如果你仅将 Microsoft 付费广告用于广告中介配置，请按照以下步骤操作。

  >**注意**&nbsp;&nbsp;这些步骤假设要在其上显示广告的应用页面包含名为“myAdGrid”****的空网格，例如 ```<Grid x:Name="myAdGrid"/>```。 在这些步骤中，将完全在代码（而非 XAML）中创建和配置广告控件。

1. 在 Visual Studio 中，打开你的 UWP 应用项目。
2.  在“解决方案资源管理器”****窗口中，右键单击“引用”****，然后选择“添加引用...”****。
在“引用管理器”****中，展开“通用 Windows”****、单击“扩展”****，然后选中“适用于 XAML 的 Microsoft Advertising SDK”****（版本 10.0）旁边的复选框。
3. 在“引用管理器”****中，单击“确定”。
4. 从 XAML 中删除 **AdMediatorControl** 声明，并删除任何使用此 **AdMediatorControl** 对象的代码，包括任何相关的事件处理程序。
5. 针对要在其上显示广告的应用 **Page** 打开代码文件。
6. 将以下语句添加到代码文件顶部（如果它不存在）。

  ```csharp
  using Microsoft.Advertising.WinRT.UI;
  using Windows.System.Profile;
  ```
7. 将以下常量声明添加到你的 **Page** 类。

  ```csharp
  private const int AD_WIDTH = <tbd>;
  private const int AD_HEIGHT = <tbd>;
  private const string WAPPLICATIONID = "<tbd>";
  private const string WADUNITID = "<tbd>";
  private const string MAPPLICATIONID = "<tbd>";
  private const string MADUNITID = "<tbd>";
  ```
7. 对于其中每个常量声明，请替换 ```<tbd>``` 值：
  * **AD_WIDTH** 和 **AD_HEIGHT**：为其指定[横幅广告的受支持广告大小]( https://msdn.microsoft.com/windows/uwp/monetize/supported-ad-sizes-for-banner-ads)之一。
  * **WAPPLICATIONID** 和 **WADUNITID**：为其指定之前从中介配置文件中检索的 Microsoft 付费广告的 **WApplicationId** 和 **WAdUnitId** 值（这些值用于付费广告的非移动广告单元）。
  * **MAPPLICATIONID** 和 **MADUNITID**：为其指定之前从中介配置文件中检索的 Microsoft 付费广告的 **MApplicationId** 和 **MAdUnitId** 值（这些值用于付费广告的移动广告单元）。

8. 将以下变量声明添加到你的 **Page** 类。

  ```csharp
  // Declare an AdControl.
  private AdControl myAdControl = null;

  // Application ID and ad unit ID values for Microsoft advertising. By default,
  // assign these to non-mobile ad unit info.
  private string myAppId = WAPPLICATIONID;
  private string myAdUnitId = WADUNITID;
  ```
5. 在对 **InitializeComponent()** 方法的调用后，将以下代码添加到你的 **Page** 类构造函数。

  ```csharp
  myAdGrid.Width = AD_WIDTH;
  myAdGrid.Height = AD_HEIGHT;

  // For mobile device families, use the mobile ad unit info.
  if ("Windows.Mobile" == AnalyticsInfo.VersionInfo.DeviceFamily)
  {
      myAppId = MAPPLICATIONID;
      myAdUnitId = MADUNITID;
  }

  // Initialize the AdControl.
  myAdControl = new AdControl();
  myAdControl.ApplicationId = myAppId;
  myAdControl.AdUnitId = myAdUnitId;
  myAdControl.Width = AD_WIDTH;
  myAdControl.Height = AD_HEIGHT;
  myAdControl.IsAutoRefreshEnabled = true;

  myAdGrid.Children.Add(myAdControl);
  ```  

### Microsoft 付费广告、自家广告和 AdDuplex

如果你使用 Microsoft 自家广告或 AdDuplex 以及 Microsoft 付费广告，并且想要继续使用 AdDuplex 进行广告中介配置，请按照本部分中的步骤操作。 代码示例支持 AdDuplex 和 Microsoft 自家广告。 如果你使用 AdDuplex 而非 Microsoft 自家广告（反之亦然），请删除不适用于你的方案的代码。

  >**注意**&nbsp;&nbsp;这些步骤假设要在其上显示广告的应用页面包含名为“myAdGrid”****的空网格，例如 ```<Grid x:Name="myAdGrid"/>```。 在这些步骤中，将完全在代码（而非 XAML）中创建和配置广告控件。

1. 在 Visual Studio 中，打开你的 UWP 应用项目。
2.  在“解决方案资源管理器”****窗口中，右键单击“引用”****，然后选择“添加引用...”****。
在“引用管理器”****中，展开“通用 Windows”****、单击“扩展”****，然后选中“适用于 XAML 的 Microsoft Advertising SDK”****（版本 10.0）旁边的复选框。
3. 在“引用管理器”****中，单击“确定”。
4. 从 XAML 中删除 **AdMediatorControl** 声明，并删除任何使用此 **AdMediatorControl** 对象的代码，包括任何相关的事件处理程序。
5. 针对要在其上显示广告的应用 **Page** 打开代码文件。
6. 将以下语句添加到代码文件顶部（如果它们不存在）。

  ```csharp
  using Windows.System.UserProfile;
  using Microsoft.Advertising.WinRT.UI;
  using Windows.System.Profile;
  ```
7. 将以下常量声明添加到你的 **Page** 类。

  ```csharp
  private const int AD_WIDTH = <tbd>;
  private const int AD_HEIGHT = <tbd>;
  private const int HOUSE_AD_WEIGHT = <tbd>;
  private const int AD_REFRESH_SECONDS = 35;
  private const int MAX_ERRORS_PER_REFRESH = 3;
  private const string WAPPLICATIONID = "<tbd>";
  private const string WADUNITID_PAID = "<tbd>";
  private const string WADUNITID_HOUSE = "<tbd>";
  private const string MAPPLICATIONID = "<tbd>";
  private const string MADUNITID_PAID = "<tbd>";
  private const string MADUNITID_HOUSE = "<tbd>";
  private const string ADDUPLEX_APPKEY = "<tbd>";
  private const string ADDUPLEX_ADUNIT = "<tbd>";
  ```
4. 对于每个已指定给 ```<tbd>``` 的常量声明，请针对你的方案将 ```<tbd>``` 替换为实值。
  * **AD_WIDTH** 和 **AD_HEIGHT**：为其指定[横幅广告的受支持广告大小]( https://msdn.microsoft.com/windows/uwp/monetize/supported-ad-sizes-for-banner-ads)之一。
  * **HOUSE_AD_WEIGHT**：为其指定一个 0 到 100 之间的整数，用于指定相较于 Microsoft 付费广告而言要应用于 Microsoft 自家广告的权重值（其中 0 是指永不显示自家广告，而 100 是指始终显示自家广告）。
  * **WAPPLICATIONID** 和 **WADUNITID_PAID**：为其指定之前从中介配置文件中检索的 Microsoft 付费广告的 **WApplicationId** 和 **WAdUnitId** 值（这些值用于付费广告的非移动广告单元）。
  * **WADUNITID_HOUSE**：为其指定之前从中介配置文件中检索的自家广告的 **WAdUnitId**（该值用于自家广告的非移动广告单元）。
  * **MAPPLICATIONID** 和 **MADUNITID_PAID**：为其指定之前从中介配置文件中检索的 Microsoft 付费广告的 **MApplicationId** 和 **MAdUnitId** 值（这些值用于付费广告的移动广告单元）。
  * **MADUNITID_HOUSE**：为其指定之前从中介配置文件中检索的自家广告的 **MAdUnitId**（该值用于自家广告的移动广告单元）。
  * **ADDUPLEX_APPKEY** 和 **ADDUPLEX_ADUNIT**：为其指定之前从中介配置文件中检索的 AdDuplex 应用密钥和广告单元 ID 值。
5. 将以下变量声明添加到你的 **Page** 类。
  ```csharp
  // Dispatch timer to fire at each ad refresh interval.
  private DispatcherTimer myAdRefreshTimer = new DispatcherTimer();

  // Global variables used for mediation decisions.
  private Random randomGenerator = new Random();
  private int errorCountCurrentRefresh = 0;  // Prevents infinite redirects.
  private int adDuplexWeight = 0;            // Will be set by GetAdDuplexWeight().

  // Microsoft and AdDuplex controls for banner ads.
  private AdControl myMicrosoftBanner = null;
  private AdDuplex.AdControl myAdDuplexBanner = null;

  // Application ID and ad unit ID values for Microsoft advertising. By default,
  // assign these to non-mobile ad unit info.
  private string myMicrosoftAppId = WAPPLICATIONID;
  private string myMicrosoftPaidUnitId = WADUNITID_PAID;
  private string myMicrosoftHouseUnitId = WADUNITID_HOUSE;
  ```
5. 在对 **InitializeComponent()** 方法的调用后，将以下代码添加到你的 **Page** 类构造函数。
  ```csharp
  myAdGrid.Width = AD_WIDTH;
  myAdGrid.Height = AD_HEIGHT;
  adDuplexWeight = GetAdDuplexWeight();
  RefreshBanner();

  // Start the timer to refresh the banner at the desired interval.
  myAdRefreshTimer.Interval = new TimeSpan(0, 0, AD_REFRESH_SECONDS);
  myAdRefreshTimer.Tick += myAdRefreshTimer_Tick;
  myAdRefreshTimer.Start();

  // For mobile device families, use the mobile ad unit info.
  if ("Windows.Mobile" == AnalyticsInfo.VersionInfo.DeviceFamily)
  {
      myMicrosoftAppId = MAPPLICATIONID;
      myMicrosoftPaidUnitId = MADUNITID_PAID;
      myMicrosoftHouseUnitId = MADUNITID_HOUSE;
  }
  ```
6. 最后，将以下方法添加到你的 **Page** 类。 这些方法将实例化 Microsoft **AdControl** 和 AdDuplex **AdControl** 对象，并将随机数字生成器与给定的权重值结合使用，以便每隔一定的计时器间隔对这些控件中的横幅广告进行刷新。
  ```csharp
  private int GetAdDuplexWeight()
  {
      // TODO: Change this logic to fit your needs.
      // This example uses Microsoft ads first in Canada and Mexico, then
      // AdDuplex as fallback. In France, AdDuplex is first. In other regions,
      // this example uses a weighted average approach, with 50% to AdDuplex.

      int returnValue = 0;
      switch (GlobalizationPreferences.HomeGeographicRegion)
      {
          case "CA":
          case "MX":
              returnValue = 0;
              break;
          case "FR":
              returnValue = 100;
              break;
          default:
              returnValue = 50;
              break;
      }
      return returnValue;
  }

  private void ActivateMicrosoftBanner()
  {
      // Return if you hit the error limit for this refresh interval.
      if (errorCountCurrentRefresh >= MAX_ERRORS_PER_REFRESH)
      {
          myAdGrid.Visibility = Visibility.Collapsed;
          return;
      }

      // Use random number generator and house ads weight to determine whether
      // to use paid ads or house ads. Paid is the default. You could alternatively
      // write a method similar to GetAdDuplexWeight and override by region.
      string myAdUnit = myMicrosoftPaidUnitId;
      int houseWeight = HOUSE_AD_WEIGHT;
      int randomInt = randomGenerator.Next(0, 100);
      if (randomInt < houseWeight)
      {
          myAdUnit = myMicrosoftHouseUnitId;
      }

      // Hide the AdDuplex control if it is showing.
      if (null != myAdDuplexBanner)
      {
          myAdDuplexBanner.Visibility = Visibility.Collapsed;
      }

      // Initialize or display the Microsoft control.
      if (null == myMicrosoftBanner)
      {
          myMicrosoftBanner = new AdControl();
          myMicrosoftBanner.ApplicationId = myMicrosoftAppId;
          myMicrosoftBanner.AdUnitId = myAdUnit;
          myMicrosoftBanner.Width = AD_WIDTH;
          myMicrosoftBanner.Height = AD_HEIGHT;
          myMicrosoftBanner.IsAutoRefreshEnabled = false;

          myMicrosoftBanner.AdRefreshed += myMicrosoftBanner_AdRefreshed;
          myMicrosoftBanner.ErrorOccurred += myMicrosoftBanner_ErrorOccurred;

          myAdGrid.Children.Add(myMicrosoftBanner);
      }
      else
      {
          myMicrosoftBanner.AdUnitId = myAdUnit;
          myMicrosoftBanner.Visibility = Visibility.Visible;
          myMicrosoftBanner.Refresh();
      }
  }

  private void ActivateAdDuplexBanner()
  {
      // Return if you hit the error limit for this refresh interval.
      if (errorCountCurrentRefresh >= MAX_ERRORS_PER_REFRESH)
      {
          myAdGrid.Visibility = Visibility.Collapsed;
          return;
      }

      // Hide the Microsoft control if it is showing.
      if (null != myMicrosoftBanner)
      {
          myMicrosoftBanner.Visibility = Visibility.Collapsed;
      }

      // Initialize or display the AdDuplex control.
      if (null == myAdDuplexBanner)
      {
          myAdDuplexBanner = new AdDuplex.AdControl();
          myAdDuplexBanner.AppKey = ADDUPLEX_APPKEY;
          myAdDuplexBanner.AdUnitId = ADDUPLEX_ADUNIT;
          myAdDuplexBanner.Width = AD_WIDTH;
          myAdDuplexBanner.Height = AD_HEIGHT;
          myAdDuplexBanner.RefreshInterval = AD_REFRESH_SECONDS;

          myAdDuplexBanner.AdLoaded += myAdDuplexBanner_AdLoaded;
          myAdDuplexBanner.AdCovered += myAdDuplexBanner_AdCovered;
          myAdDuplexBanner.AdLoadingError += myAdDuplexBanner_AdLoadingError;
          myAdDuplexBanner.NoAd += myAdDuplexBanner_NoAd;

          myAdGrid.Children.Add(myAdDuplexBanner);
      }
      myAdDuplexBanner.Visibility = Visibility.Visible;
  }

  private void myAdRefreshTimer_Tick(object sender, object e)
  {
      RefreshBanner();
  }

  private void RefreshBanner()
  {
      // Reset the error counter for this refresh interval and
      // make sure the ad grid is visible.
      errorCountCurrentRefresh = 0;
      myAdGrid.Visibility = Visibility.Visible;

      // Display ad from AdDuplex.
      if (100 == adDuplexWeight)
      {
          ActivateAdDuplexBanner();
      }
      // Display Microsoft ad.
      else if (0 == adDuplexWeight)
      {
          ActivateMicrosoftBanner();
      }
      // Use weighted approach.
      else
      {
          int randomInt = randomGenerator.Next(0, 100);
          if (randomInt < adDuplexWeight) ActivateAdDuplexBanner();
          else ActivateMicrosoftBanner();
      }
  }

  private void myMicrosoftBanner_AdRefreshed(object sender, RoutedEventArgs e)
  {
      // Add your code here as necessary.
  }

  private void myMicrosoftBanner_ErrorOccurred(object sender, AdErrorEventArgs e)
  {
      errorCountCurrentRefresh++;
      ActivateAdDuplexBanner();
  }

  private void myAdDuplexBanner_AdLoaded(object sender, AdDuplex.Banners.Models.BannerAdLoadedEventArgs e)
  {
      // Add your code here as necessary.
  }

  private void myAdDuplexBanner_NoAd(object sender, AdDuplex.Common.Models.NoAdEventArgs e)
  {
      errorCountCurrentRefresh++;
      ActivateMicrosoftBanner();
  }

  private void myAdDuplexBanner_AdLoadingError(object sender, AdDuplex.Common.Models.AdLoadingErrorEventArgs e)
  {
      errorCountCurrentRefresh++;
      ActivateMicrosoftBanner();
  }

  private void myAdDuplexBanner_AdCovered(object sender,   AdDuplex.Banners.Core.AdCoveredEventArgs e)
  {
      errorCountCurrentRefresh++;
      ActivateMicrosoftBanner();
  }
  ```



<!--HONumber=Sep16_HO1-->


