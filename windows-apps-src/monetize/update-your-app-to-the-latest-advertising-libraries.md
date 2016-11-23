---
author: mcleanbyron
description: "了解如何更新应用以使用最新的受支持 Microsoft 广告库，并确保应用继续收到横幅广告。"
title: "将应用更新到最新的 Microsoft Advertising 库"
translationtype: Human Translation
ms.sourcegitcommit: 9bd83a41ea4ec4ec7a75ef89e9c92f73d86cc731
ms.openlocfilehash: 710a5f4a3ae566550939fe783af7e97d20dd1b28


---

# 将应用更新到最新的 Microsoft Advertising 库

从 2017 年 1 月开始，我们将不再向使用较早的 Microsoft 广告 SDK 版本的应用提供横幅广告。 如果你有使用 **AdControl** 或 **AdMediatorControl** 显示横幅广告的现有应用（已经在应用商店中或仍然在开发中），则可能需要将应用更新为使用最新的广告 SDK，以便使应用在 2017 年 1 月继续接收横幅广告。 按照本文中的说明确定应用是否受此更改影响，并了解如何在必要时更新应用。

如果应用受此更改影响，并且你未将应用更新为使用最新的广告 SDK，则从 2017 年 1 月开始，你将看到以下行为：

* 将不再向应用中的任何 **AdControl** 或 **AdMediatorControl** 控件提供横幅广告，并且你将不再从这些控件中获取任何广告收益。

* 当应用中的 **AdControl** 或 **AdMediatorControl** 请求新广告时，将引发控件的 **ErrorOccurred** 事件，并且事件参数的 **ErrorCode** 属性将具有值 **NoAdAvailable**。

为了提供有关此更改的某些其他上下文，我们将删除对不支持最低功能集的较早广告 SDK 版本的支持，包括通过互动广告局 (IAB) 的[移动富媒体广告界面定义 (MRAID) 1.0 规范](http://www.iab.com/wp-content/uploads/2015/08/IAB_MRAID_VersionOne.pdf)提供 HTML5 富媒体的功能。 我们的许多广告厂商寻求这些功能，我们进行此更改是为了增加我们的应用生态系统对广告厂商的吸引力，并最终为你带来更多收益。

如果你遇到任何问题或需要帮助，请[联系支持人员](http://go.microsoft.com/fwlink/?LinkId=393643)。

>**注意**
            &nbsp;&nbsp;如果你之前已将应用更新为使用 [Microsoft Store Services SDK](http://aka.ms/store-services-sdk)（适用于 UWP 应用）或 [Microsoft Advertising SDK for Windows and Windows Phone 8.x](http://aka.ms/store-8-sdk)（适用于 Windows8.1 和 Windows Phone 8.x 应用），则应用已使用最新的可用广告 SDK，并且你无需对应用进行任何进一步的更改。

## 先决条件

* 使用 **AdControl** 或 **AdMediatorControl** 的应用的完整源代码和 Visual Studio 项目文件。

* 应用的 .appx 或 .xap 包。

  >**注意**
            &nbsp;&nbsp;如果你不再有应用的 .appx 或 .xap 包，但仍然有包含曾用于生成应用的 Visual Studio 和广告 SDK 版本的开发计算机，则可以在 Visual Studio 中重新生成 .appx 或 .xap 包。

<span id="part-1" />
## 第 1 部分：确定是否需要更新应用

按照以下部分中的说明确定是否需要更新应用。

### 应用使用 AdControl

如果应用使用 **AdControl** 显示横幅广告，请按照这些说明操作。

**适用于 Windows10 的 UWP 应用**

1. 创建应用的 .appx 包副本以便不干扰原始软件包包、重命名该副本使其具有 .zip 扩展名，然后提取文件内容。

2. 检查应用包的提取内容：

  * 如果看到 Microsoft.Advertising.dll 文件，则表示应用使用早期的 SDK，必须按照下面部分中的说明更新项目。 继续到[第 2 部分](update-your-app-to-the-latest-advertising-libraries.md#part-2)。

  * 如果未看到 Microsoft.Advertising.dll 文件，则表示 UWP 应用已经使用最新的可用广告 SDK，并且你无需对项目进行任何更改。

<span/>

**Windows8.1 或 Windows Phone 8.x 应用**

1. 创建应用的 .appx 或 .xap 包副本以便不干扰原始软件包包、重命名该副本使其具有 .zip 扩展名，然后提取文件内容。

2. 对于 XAML 或 JavaScript/HTML 应用，请检查应用包的提取内容：

  * 如果看到 Microsoft.Advertising.winmd 文件，但未看到 UniversalXamlAdControl.\*.dll 文件（适用于 XAML 应用）或 UniversalSharedLibrary.Windows.dll 文件（适用于 JavaScript/HTML 应用），则表示应用使用早期的 SDK，并且你必须按照以下部分中的说明更新项目。 继续到[第 2 部分](update-your-app-to-the-latest-advertising-libraries.md#part-2)。

  * 否则，按以下步骤继续。

2. 打开 Windows PowerShell、输入以下命令，然后将 ```-Path``` 参数分配到应用包的提取内容的完整路径。 此命令显示项目引用的所有广告库以及每个库的版本。

    ```
    get-childitem -Path "<path to your extracted package>" * -Recurse -include *advert*.dll,*admediator*.dll,*xamladcontrol*.dll,*universalsharedlibrary*.dll | where-object {$_.Name -notlike "*resources*" -and $_.Name -notlike "*design*" } | foreach-object { "{0}`t{1}" -f $_.FullName, [System.Diagnostics.FileVersionInfo]::GetVersionInfo($_).FileVersion }
    ```
2. 在下表中找到适用于应用目标平台的文件，并将该文件的版本与表中列出的版本进行比较。

  <table>
    <colgroup>
      <col width="33%" />
      <col width="33%" />
      <col width="33%" />
    </colgroup>
    <thead>
      <tr class="header">
        <th align="left">目标平台</th>
        <th align="left">文件</th>
        <th align="left">版本</th>
      </tr>
    </thead>
    <tbody>
      <tr class="odd">
        <td align="left"><p>Windows8.1 XAML</p></td>
        <td align="left"><p>UniversalXamlAdControl.Windows.dll</p></td>
        <td align="left"><p>8.5.1601.07018</p></td>
      </tr>
      <tr class="odd">
        <td align="left"><p>Windows Phone 8.1 XAML</p></td>
        <td align="left"><p>UniversalXamlAdControl.WindowsPhone.dll</p></td>
        <td align="left"><p>8.5.1601.07018</p></td>
      </tr>
      <tr class="odd">
        <td align="left"><p>Windows8.1 JavaScript/HTML<br/>Windows Phone 8.1 JavaScript/HTML</p></td>
        <td align="left"><p>UniversalSharedLibrary.Windows.dll</p></td>
        <td align="left"><p>8.5.1601.07018</p></td>
      </tr>
      <tr class="odd">
        <td align="left"><p>Windows Phone 8.1 Silverlight</p></td>
        <td align="left"><p>Microsoft.Advertising.\*.dll</p></td>
        <td align="left"><p>8.1.50112.0</p></td>
      </tr>
      <tr class="odd">
        <td align="left"><p>Windows Phone 8.0 Silverlight</p></td>
        <td align="left"><p>Microsoft.Advertising.\*.dll</p></td>
        <td align="left"><p>6.2.40501.0</p></td>
      </tr>
    </tbody>
  </table>

3. 如果文件的版本等于或高于上表中列出的版本，则无需对项目进行任何更改。

  如果文件具有更低的版本号，则必须按照下面部分中的说明更新项目。 继续到[第 2 部分](update-your-app-to-the-latest-advertising-libraries.md#part-2)。

<span/>

**Windows8.0 应用**

* 从 2017 年 1 月开始，不再向面向 Windows8.0 的应用提供横幅广告。 为了避免丢失的印象，我们建议你将项目转换为面向 Windows10 的 UWP 应用。 大多数 Windows8.0 应用流量现在在使用 Windows10 的设备上运行。

<span/>

**Windows Phone 7.x 应用**

* 从 2017 年 1 月开始，不再向面向 Windows Phone 7.x 的应用提供横幅广告。 为了避免丢失的印象，我们建议你将项目转换为面向 Windows Phone 8.1 应用或转换为面向 Windows10 的 UWP 应用。 大多数 Windows7.x 应用流量现在在使用 Windows Phone 8.1 或 Windows10 的设备上运行。

<span/>

### 应用使用 AdMediatorControl

如果应用使用 **AdMediatorControl** 显示横幅广告，请按照以下说明确定是否需要更新应用。

**适用于 Windows10 的 UWP 应用**

* UWP 应用不再支持 **AdMediatorControl**。 必须按照以下部分中的说明迁移到使用 **AdControl**。 继续到[第 2 部分](update-your-app-to-the-latest-advertising-libraries.md#part-2)。

<span/>

**Windows8.1 或 Windows Phone 8.1 应用**

1. 创建应用的 .appx 或 .xap 包副本以便不干扰原始软件包包、重命名该副本使其具有 .zip 扩展名，然后提取文件内容。

2. 打开 Windows PowerShell、输入以下命令，然后将 ```-Path``` 参数分配到应用包的提取内容的完整路径。 此命令显示项目引用的所有广告库以及每个库的版本。

    ```
    get-childitem -Path "<path to your extracted package>" * -Recurse -include *advert*.dll,*admediator*.dll,*xamladcontrol*.dll,*universalsharedlibrary*.dll | where-object {$_.Name -notlike "*resources*" -and $_.Name -notlike "*design*" } | foreach-object { "{0}`t{1}" -f $_.FullName, [System.Diagnostics.FileVersionInfo]::GetVersionInfo($_).FileVersion }
    ```

2. 如果输出中列出的 Microsoft.AdMediator.\*.dll 文件的版本是版本 2.0.1603.18005 或更高版本，则无需对项目进行任何更改。

  如果这些文件具有更低的版本号，则必须按照下面部分中的说明更新项目。 继续到[第 2 部分](update-your-app-to-the-latest-advertising-libraries.md#part-2)。

<span id="part-2" />
## 第 2 部分：安装最新的 SDK

如果应用使用早期的 SDK 版本，请按照以下说明确保你的开发计算机上具有最新的 SDK。

1. 确保开发计算机已安装 Visual Studio 2015（适用于 UWP、Windows8.1 或 Windows Phone 8.x 项目）或 Visual Studio 2013（适用于 Windows8.1 或 Windows Phone 8.x 项目）。

  >**注意**
            &nbsp;&nbsp;如果 Visual Studio 在开发计算机上处于打开状态，请在执行以下步骤前关闭它。

1.  从开发计算机中卸载 Microsoft Advertising SDK 和广告中介 SDK 的所有以前版本。

2.  打开“命令提示符”窗口并运行这些命令以清除可能与 Visual Studio 一起安装（但可能未显示在计算机上的已安装程序列表中）的任何 SDK 版本：

  ```
  MsiExec.exe /x{5C87A4DB-31C7-465E-9356-71B485B69EC8}
  MsiExec.exe /x{6AB13C21-C3EC-46E1-8009-6FD5EBEE515B}
  MsiExec.exe /x{6AC81125-8485-463D-9352-3F35A2508C11}
  ```

3.  为应用安装最新的 SDK：
  * 对于 Windows10 上的 UWP 应用，请安装 [Microsoft Store Services SDK](http://aka.ms/store-services-sdk)。
  * 对于面向较早操作系统版本的应用，请安装 [Microsoft Advertising SDK for Windows and Windows Phone 8.x](http://aka.ms/store-8-sdk)。

## 第 3 部分：更新项目

按照以下说明更新项目。

### 适用于 Windows10 的 UWP 项目

<span/>

如果应用使用 **AdMediatorControl**，请[将应用重构为使用 AdControl](migrate-from-admediatorcontrol-to-adcontrol.md)。 UWP 应用不再支持 **AdMediatorControl**。

如果应用使用 **AdControl**，请从项目中删除对 Microsoft 广告库的所有现有引用，并按照 [AdControl in XAML](adcontrol-in-xaml-and--net.md) 或 [AdControl in HTML](adcontrol-in-html-5-and-javascript.md) 说明添加所需的引用。 这将确保项目使用正确的库。 可保留现有 XAML 标记和代码。

<span/>

### Windows8.1 或 Windows Phone 8.1（XAML 或 JavaScript/HTML）项目

<span/>

1. 从项目中删除所有 Microsoft.Advertising.\* 和 Microsoft.AdMediator.\* 引用。 如果使用了通用项目模板，可能具有两个引用（分别用于 Windows 和 Windows Phone）。

2. 如果应用使用 **AdMediatorControl**，请按照[添加和使用广告中介控件](https://msdn.microsoft.com/library/windows/apps/xaml/dn864355.aspx)中的说明添加回库引用。 如果应用使用 **AdControl**，请按照 [XAML 中的 AdControl](adcontrol-in-xaml-and--net.md) 或 [HTML 中的 AdControl](adcontrol-in-html-5-and-javascript.md) 添加回库引用。

<span/>

注意以下事项：

* 如果应用之前已编译到**任何 CPU** 平台，则必须将项目重新编译到特定于体系结构的平台（x86、x64 或 ARM）。

* 如果你有一个 Windows Phone 8.x XAML 应用，并且在该应用之前使用的 SDK 版本中，在 **Microsoft.Advertising.Mobile.UI** 命名空间中定义了 **AdControl** 类，则必须更新代码以引用 **Microsoft.Advertising.WinRT.UI** 命名空间中的 **AdControl** 类（此类在更新的 SDK 版本中移动了命名空间）。

* 除了上述问题以外，你还可以保留现有 XAML 标记和代码。

<span/>

### Windows Phone 8.x Silverlight 项目

<span/>

1. 从项目中删除所有 Microsoft.Advertising.\* 和 Microsoft.AdMediator.\* 引用。

2. 如果应用使用 **AdMediatorControl**，请按照[添加和使用广告中介控件](https://msdn.microsoft.com/library/windows/apps/xaml/dn864355.aspx)中的说明添加回库引用。 如果应用使用 **AdControl**，请按照 [Windows Phone Silverlight 中的 AdControl](adcontrol-in-windows-phone-silverlight.md) 添加回库引用。

<span/>

注意以下事项：

* 可保留现有 XAML 标记和代码。

* 从“解决方案资源管理器”，检查项目中 **Microsoft.Advertising.Mobile.UI** 引用的属性。 它应为版本 6.2.40501.0（如果项目面向 Windows Phone 8.0）或 8.1.50112.0（如果应用面向 Windows Phone 8.1）。

* 对于 Windows Phone 8.x Silverlight 应用，不支持在仿真程序上测试生产单位。 我们建议在设备上测试。

## 第 4 部分：测试和重新发布应用

测试应用以确保它按预期显示横幅广告。

如果应用的以前版本已经在应用商店中提供，请在 Windows 开发人员中心仪表板中为已更新的应用[创建新提交](https://msdns.microsoft.com/windows/uwp/publish/app-submissions)以重新发布应用。





 



<!--HONumber=Nov16_HO1-->


