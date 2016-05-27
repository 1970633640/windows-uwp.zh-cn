---
author: msatranjr
ms.assetid: 25B18BA5-E584-4537-9F19-BB2C8C52DFE1
title: 应用功能声明
description: 功能必须在你的通用 Windows 平台 (UWP) 应用的程序包清单中声明，以便可用于访问某些 API 或资源（如图片、音乐）或者设备（如相机或麦克风）。
---
# 应用功能声明

\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

功能必须在你的通用 Windows 平台 (UWP) 应用的[程序包清单](https://msdn.microsoft.com/library/windows/apps/BR211474)中声明，以便可用于访问某些 API 或资源（如图片、音乐）或者设备（如相机或麦克风）。

可以通过在应用的[程序包清单](https://msdn.microsoft.com/library/windows/apps/BR211474)中声明功能来请求对特定资源或 API 的访问权限。 可以使用 Microsoft Visual Studio 中的[清单设计器](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/br230259.aspx)来声明常用功能，也可以手动添加它们。 有关详细信息，请参阅[如何在程序包清单中指定功能](https://msdn.microsoft.com/library/windows/apps/BR211477)。 请务必了解，当客户从应用商店获取你的应用时，会向它们告知该应用声明的所有功能。 请避免声明你的应用不需要的功能。

某些功能为应用提供对*敏感资源*的访问权限。 由于这些资源可用于访问用户私人数据或花费用户金钱，因此它们被认为是敏感资源。 由“设置”应用管理的隐私设置允许用户动态控制对敏感资源的访问权限。 因此，你的应用不会假设敏感资源始终可用，这一点很重要。 有关访问敏感资源的详细信息，请参阅[隐私感知应用指南](https://msdn.microsoft.com/library/windows/apps/Hh768223)。 已注释用于为应用提供对*敏感资源*的访问权限的功能，即此类功能应用场景的旁边会有一个星号 (*)。

本文介绍了以下所述的四类功能。

-   适用于大多数常见应用场景的通用功能。

-   允许你的应用访问外围设备和内部设备的设备功能。

-   需要使用特殊的公司帐户才能提交到应用商店以供使用的特殊用途的功能。 有关公司帐户的详细信息，请参阅[帐户类型、位置和费用](https://msdn.microsoft.com/library/windows/apps/JJ863494)。

-   仅适用于 Microsoft 及其合作伙伴的受限功能。

## 常用功能

常用功能适用于最常见的应用场景。

| 功能应用场景 | 功能用法 |
|---------------------|------------------|
| **音乐**\* | **musicLibrary** 功能提供对用户音乐的编程访问权限，让应用无需用户交互即可枚举和访问库中的所有文件。 此功能通常用在使用整个音乐库的自动唱片点唱机应用中。<br /><br />[
            **文件选取器**](https://msdn.microsoft.com/library/windows/apps/BR207847)提供了一种强大的 UI 机制，让用户可以打开要通过某个应用处理的文件。 仅当应用需要进行编程访问，而使用**文件选取器**无法实现编程访问时，才声明 **musicLibrary** 功能。<br /><br /> 当在应用的程序包清单中声明 **musicLibrary** 功能时，该功能必须包含 **uap** 命名空间，如下所示。 <table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:Capability Name="musicLibrary"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **图片**\* | **picturesLibrary** 功能提供对用户图片的编程访问权限，让应用无需用户交互即可枚举和访问库中的所有文件。 在使用整个图片库的照片应用中，通常会使用此功能。<br /><br />[
            **文件选取器**](https://msdn.microsoft.com/library/windows/apps/BR207847)提供了一种强大的 UI 机制，让用户可以打开要通过某个应用处理的文件。 仅当应用需要进行编程访问，而使用**文件选取器**无法实现编程访问时，才声明 **picturesLibrary** 功能。<br /><br />当在应用的程序包清单中声明 **picturesLibrary** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="picturesLibrary"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **视频**\* | **videosLibrary** 功能提供对用户视频的编程访问权限，让应用无需用户交互即可枚举和访问库中的所有文件。 此功能通常用在使用整个视频库的电影播放应用中。<br /><br />[
            **文件选取器**](https://msdn.microsoft.com/library/windows/apps/BR207847)提供了一种强大的 UI 机制，让用户可以打开要通过某个应用处理的文件。 仅当应用需要进行编程访问，而使用**文件选取器**无法实现编程访问时，才声明 **videosLibrary** 功能。<br /><br />当在应用的程序包清单中声明 **videosLibrary** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="videosLibrary"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **可移动存储** | **removableStorage** 功能提供对可移动存储（如 U 盘和外部硬盘驱动器）中文件的编程访问权限，这些文件将按照程序包清单中声明的文件类型关联进行筛选。 例如，如果某个文档阅读器应用声明了 .doc 文件类型关联，则它可以打开可移动存储设备中的 .doc 文件，但无法打开其他类型的文件。 声明此功能时请务必小心，因为用户的可移动存储设备中可能包含多种信息，他们将期待你的应用提供有效的理由，以便对该可移动存储中属于已声明类型的所有文件进行编程访问。<br /><br />用户将期待你的应用处理你所声明的所有文件关联。 因此，请勿声明你的应用无法可靠处理的文件关联。 [
            **文件选取器**](https://msdn.microsoft.com/library/windows/apps/BR207847)提供了一种强大的 UI 机制，让用户可以打开要通过某个应用处理的文件。<br /><br />仅当应用需要进行编程访问，而使用[**文件选取器**](https://msdn.microsoft.com/library/windows/apps/BR207847)无法实现编程访问时，才声明 **removableStorage** 功能。<br /><br />当在应用的程序包清单中声明 **removableStorage** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="removableStorage"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **Internet 和公共网络**\* | 存在两种提供对 Internet 和公共网络的不同级别访问权限的功能。<br /><br />**internetClient** 功能指示应用可以接收从 Internet 传入的数据。 无法充当服务器。 无法访问本地网络。<br />**internetClientServer** 功能指示应用可以接收从 Internet 传入的数据。 可以充当服务器。 无法访问本地网络。<br /><br />具有 Web 服务组件的大多数应用都将使用 **internetClient**。 如果应用支持需要在其中侦听传入的网络连接的对等 (P2P) 方案，则应该使用 **internetClientServer**。 **internetClientServer** 功能包括 **internetClient** 功能所提供的访问权限，因此，在指定 **internetClientServer** 时无需指定 **internetClient**。
| **家庭和工作网络**\* | **privateNetworkClientServer** 功能提供通过防火墙对家庭和工作网络的入站和出站访问权限。 此功能通常用于通过局域网 (LAN) 通信的游戏和在各种本地设备上共享数据的应用。 如果你的应用指定了 **musicLibrary**、**picturesLibrary** 或 **videosLibrary**，则无需使用此功能即可访问家庭组中相应的库。 在 Windows 上，此功能不提供对 Internet 的访问权限。
| **约会** | **appointments** 功能提供对用户的约会存储的访问权限。 此功能允许读取对从同步的网络帐户获得的约会以及写入约会存储的其他应用的访问权限。 通过此功能，你的应用可以创建新的日历并向所创建的日历写入约会。<br /><br />当在应用的程序包清单中声明 **appointments** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="appointments"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **联系人**\* | **contacts** 功能提供了对各种联系人存储中的联系人聚合视图的访问权限。 此功能向已在各种网络和本地联系人存储中同步的联系人提供了对该应用的受限访问权限（应用网络许可规则）。<br /><br />当在应用的程序包清单中声明 **contacts** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="contacts"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **代码生成** | **codeGeneration** 功能允许应用访问以下功能，可向应用提供 JIT 功能。<br /><br />[**VirtualProtectFromApp**](https://msdn.microsoft.com/library/windows/desktop/Mt169846)<br />[**CreateFileMappingFromApp**](https://msdn.microsoft.com/library/windows/desktop/Hh994453)<br />[**OpenFileMappingFromApp**](https://msdn.microsoft.com/library/windows/desktop/Mt169844)<br />[**MapViewOfFileFromApp**](https://msdn.microsoft.com/library/windows/desktop/Hh994454)
| **AllJoyn** | **allJoyn** 功能允许网络上支持 AllJoyn 的应用和设备发现彼此并进行交互。<br /><br />在 [**Windows.Devices.AllJoyn**](https://msdn.microsoft.com/library/windows/apps/Dn894971) 命名空间中访问 API 的所有应用都必须使用此功能。
| **电话呼叫** | **phoneCall** 功能允许应用访问设备上的所有电话线并执行以下功能。<br /><br />通过电话线发出呼叫并显示系统拨号器，而不提示用户。<br />访问与线相关的元数据。<br />访问与线相关的触发器。<br />允许用户选择的垃圾邮件筛选器应用设置并检查阻止列表和呼叫来源信息。<br /><br />当在应用的程序包清单中声明 **phoneCall** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="phoneCall"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>**phoneCallHistoryPublic** 功能允许应用读取设备上的手机网络和某些 VOIP 呼叫历史记录信息。 此功能还允许应用编写 VOIP 呼叫历史记录项。 若要访问 [**PhoneCallHistoryStore**](https://msdn.microsoft.com/library/windows/apps/Dn705931) 类的所有成员，则需要此功能。
| **录制的通话文件夹**\* | **recordedCallsFolder** 设备功能允许应用访问记录的通话文件夹。<br /><br />当在应用的程序包清单中声明 **recordedCallsFolder** 功能时，该功能必须包含 **mobile** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;mobile:CapabilityName="recordedCallsFolder"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **用户帐户信息**\* | **userAccountInformation** 功能使应用能够访问用户的名称和头像。<br /><br />若要访问 Windows.System.User 命名空间中的某些 API，此功能是必需的。<br /><br />当在应用的程序包清单中声明 **userAccountInformation** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="userAccountInformation"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **VOIP 呼叫** | **voipCall** 功能允许应用访问 [**Windows.ApplicationModel.Calls**](https://msdn.microsoft.com/library/windows/apps/Dn297266) 命名空间中的 VOIP 呼叫 API。<br /><br />当在应用的程序包清单中声明 **voipCall** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="voipCall"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **3D 对象** | **objects3D** 功能允许应用编程访问 3D 对象文件。 此功能通常用在需要访问整个 3D 对象库的 3D 应用和游戏中。<br /><br />若要使用 [**Windows.Storage**](https://msdn.microsoft.com/library/windows/apps/BR227346) 命令空间中的 API 访问包含 3D 对象的文件夹，则需要此功能。<br /><br />当在应用的程序包清单中声明 **objects3D** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="objects3d"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **读取阻止的消息**\* | **blockedChatMessages** 功能允许应用读取已由“垃圾邮件筛选器”应用阻止的短信和彩信。<br /><br />若要使用 [**Windows.ApplicationModel.Chat**](https://msdn.microsoft.com/library/windows/apps/Dn642321) 命令空间中的 API 访问已阻止的消息，则需要此功能。<br /><br />当在应用的程序包清单中声明 **blockedChatMessages** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="chat"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **IoT 低级别总线硬件** | **lowLevelDevices** 功能允许在 IoT 设备上运行的应用访问低级别总线硬件，例如 GPIO、I2C、SPI、ADC 和 PWM。<br /><br />若要访问 [**Windows.Devices.Spi**](https://msdn.microsoft.com/library/windows/apps/Dn708178) 命名空间中的某些 API，则需要此功能。<br /><br />当在应用的程序包清单中声明 **lowLevelDevices** 功能时，该功能必须包含 **iot** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;iot:CapabilityName="lowLevelDevices"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>
| **IoT 系统管理** | **systemManagement** 功能允许应用具有基本的系统管理权限，例如关机或重启、区域设置和时区。<br /><br />若要访问 [**Windows.System**](https://msdn.microsoft.com/library/windows/apps/BR241814) 命名空间中的某些 API，则需要此功能。<br /><br />当在应用的程序包清单中声明 **systemManagement** 功能时，该功能必须包含 **iot** 命名空间，如下所示。<table><thead><tr><th>XML</th></tr></thead><tbody><tr><td><pre><code>&lt;Capabilities&gt;&lt;iot:CapabilityName="systemManagement"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table>


## 设备功能

设备功能允许你的应用访问外围设备和内部设备。 可在你的应用包清单中使用 **DeviceCapability** 元素指定设备功能。 此元素可能需要其他子元素，并且某些设备功能需要手动添加到该程序包清单。 有关详细信息，请参阅[如何在程序包清单中指定设备功能](https://msdn.microsoft.com/library/windows/apps/Dn263092)和 [**DeviceCapability Schema reference**](https://msdn.microsoft.com/library/windows/apps/BR211430)。

| 功能应用场景 | 功能用法 |
|---------------------|------------------|
| **位置**\* | **location** 功能提供对定位功能的访问权限，定位功能通常从专用硬件（如电脑中的 GPS 传感器）检索获得或从可用的网络信息中获得。 应用必须处理用户从“设置”****超级按钮禁用定位服务的情况。 |
| **麦克风** | **microphone** 功能提供对麦克风音频源的访问权限，让应用可以录制来自所连接麦克风的音频。 应用必须处理用户从“设置”****超级按钮禁用麦克风的情况。 |
| **邻近感应** | **proximity** 功能支持临近的多台设备彼此通信。 此功能通常用在一般的多玩家游戏和交换信息的应用中。 设备会尝试使用可提供最佳连接的通信技术，包括蓝牙、Wi-Fi 和 Internet。 此功能仅用于在设备之间发起通信。 |
| **摄像头** | **webcam** 功能提供对内置相机或外部摄像头的视频源的访问权限，这使应用可以捕获照片和视频。 在 Windows 上，应用必须处理用户从“设置”****超级按钮禁用相机的情况。<br/>**webcam** 功能仅授予对视频流的访问权限。 若要也授予对音频流的访问权限，必须添加 **microphone** 功能。 |
| **USB** | **usb** 设备功能允许访问[为 USB 设备更新应用清单程序包](http://go.microsoft.com/fwlink/p/?LinkId=302259)中的 API。 |
| **人体学接口设备 (HID)** | **humaninterfacedevice** 设备功能允许访问[如何为 HID 指定设备功能](https://msdn.microsoft.com/library/windows/apps/Dn263091)中的 API。 |
| **服务点 (POS)** | **pointOfService** 设备功能允许访问 [**Windows.Devices.PointOfService**](https://msdn.microsoft.com/library/windows/apps/Dn298071) 命名空间中的 API。 该命名空间允许你的应用访问服务点 (POS) 条码扫描仪和磁条阅读器。 该命名空间提供一个独立于供应商的接口，可用于从 Windows 应用商店应用访问由各种制造商提供的 POS 设备。 |
| **蓝牙** | **bluetooth** 设备功能允许应用通过通用属性 (GATT) 或经典基本速率 (RFCOMM) 协议与已经配对的蓝牙设备进行通信。<br/>若要使用 [**Windows.Devices.Bluetooth**](https://msdn.microsoft.com/library/windows/apps/Dn263413) 命名空间中的某些 API，则需要此功能。 |
| **WLAN 网络** | **wiFiControl** 设备功能允许应用扫描并连接到 WLAN 网络。<br/>若要使用 [**Windows.Devices.WiFi**](https://msdn.microsoft.com/library/windows/apps/Dn975224) 命名空间中的某些 API，则需要此功能。 |
| **无线电收发器状态** | **radios** 设备功能允许应用切换 WLAN 和蓝牙无线电收发器。<br/>若要使用 [**Windows.Devices.Radios**](https://msdn.microsoft.com/library/windows/apps/Dn996447) 命名空间中的 API，则需要此功能。  |
| **光盘** | **optical** 设备功能允许应用访问光盘驱动器（如 CD、DVD 和蓝光光盘）上的功能。<br/>若要使用 [**Windows.Devices.Custom**](https://msdn.microsoft.com/library/windows/apps/Dn263667) 命名空间中的某些 API，则需要此功能。 |
| **运动活动** | **activity** 设备功能允许应用检测设备的当前运动。<br/>若要使用 [**Windows.Devices.Sensors**](https://msdn.microsoft.com/library/windows/apps/BR206408) 命名空间中的某些 API，则需要此功能。 |

## 特殊和受限功能

**重要提示**  
特殊和受限功能专用于非常特定的场景。 这些功能的使用受严格限制，且受应用商店的其他上架政策和评审的约束。

在某些情况下，这些功能是必需的或适宜的，如在使用双因素身份验证开展银行业务时，用户提供带数字签名的智能卡确认其身份。 其他应用可能主要针对企业用户而设计，可能需要访问一些必需使用用户的域凭据才能访问的企业资源。

应用了特殊用途功能的应用需要使用公司帐户才能将这些功能提交到应用商店。 相反，受限功能不需要用于应用商店的特殊公司帐户，开发人员不可使用这些功能。 受限功能仅适用于 Microsoft 及其合作伙伴开发的应用。 有关公司帐户的详细信息，请参阅[帐户类型、位置和费用](https://msdn.microsoft.com/library/windows/apps/JJ863494)。

以不同于其他功能的方式在应用的程序包清单中声明所有受限功能时，这些功能必须包含 **rescap** 命名空间。 以下示例演示如何声明 **appCaptureSettings** 功能。

```xml
<Capabilities>
    <rescap:Capability Name="appCaptureSettings"/>
</Capabilities>
```

你还必须在 Package.appxmanifest 文件的顶部添加 **xmlns:rescap** 命名空间声明，如下所示。

```xml
<Package
    xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
    IgnorableNamespaces="uap mp wincap rescap">
```

| 功能应用场景 | 功能用法 |
|---------------------|------------------|
| **企业** | Windows 域凭据支持用户使用其凭据登录远程资源，其原理类似于用户已提供其用户名和密码。 **enterpriseAuthentication** 特殊功能通常用在连接到企业内部服务器的业务线应用中。<br /><br />对于一般的 Internet 通信，无需使用此功能。<br /><br />**enterpriseAuthentication** 特殊功能专用于支持常见业务线应用。 不要在无需访问公司资源的应用中声明此功能。 [
            **文件选取器**](https://msdn.microsoft.com/library/windows/apps/BR207847)提供了一种强大的 UI 机制，让用户可以打开网络共享中要通过某个应用处理的文件。 仅当应用需要进行编程访问，而使用**文件选取器**无法实现编程访问时，才声明 **enterpriseAuthentication** 特殊功能。<br /><br />当在应用的程序包清单中声明 **enterpriseAuthentication** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<br /><br /><div class="code"><span codelanguage="XML"></span><table><colgroup><col width="100%" /></colgroup><thead><tr class="header"><th align="left">XML</th></tr></thead><tbody><tr class="odd"><td align="left"><pre><code>&lt;Capabilities&gt;&lt;uap:CapabilityName="enterpriseAuthentication"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table></div>**enterpriseDataPolicy** 功能允许应用为设备定义和使用特定于企业的策略。 若要使用以下类的所有成员，此功能是必需的。<ul><li>[**FileProtectionManager**](https://msdn.microsoft.com/library/windows/apps/Dn705151)</li><li>[**DataProtectionManager**](https://msdn.microsoft.com/library/windows/apps/Dn706017)</li><li>[**ProtectionPolicyManager**](https://msdn.microsoft.com/library/windows/apps/Dn705170)</li></ul></td></tr>
| **共享用户证书** | **sharedUserCertificates** 特殊功能支持应用在“共享用户”存储中添加和访问基于软件和硬件的证书，例如存储在智能卡上的证书。 此功能通常用于需要智能卡来进行身份验证的财经或企业应用。<br /><br />当在应用的程序包清单中声明 **sharedUserCertificates** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<br /><br /><div class="code"><span codelanguage="XML"></span><table><colgroup><col width="100%" /></colgroup><thead><tr class="header"><th align="left">XML</th></tr></thead><tbody><tr class="odd"><td align="left"><pre><code>&lt;Capabilities&gt;&lt;uap:Capability Name="sharedUserCertificates"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table></div>
|**文档**\* | **documentsLibrary** 特殊功能提供对用户文档的编程访问权限，这些文档将按照程序包清单中声明的文件类型关联进行筛选，以支持脱机访问 OneDrive。 例如，如果某个 DOC 阅读器应用仅声明了一个 .doc 文件类型关联，则它可以打开文档中的 .doc 文件，却无法打开其他类型的文件。<br /><br />声明 **documentsLibrary** 特殊功能的应用无法访问家庭组计算机中的文档。 [文件选取器](https://msdn.microsoft.com/library/windows/apps/Hh465174)提供了一种强大的 UI 机制，让用户可以打开要通过某个应用处理的文件。 仅当无法使用文件选取器时才声明 **documentsLibrary** 特殊功能。<br /><br />若要使用 **documentsLibrary** 特殊功能，应用必须：<ul><li>使用有效的 OneDrive URL 或资源 ID 促进跨平台脱机访问特定 OneDrive 内容</li><li>在脱机时将打开的文件自动保存到用户的 OneDrive</li></ul>使用 **documentsLibrary** 特殊功能实现这两个目的的应用还可以选择使用该功能打开另一文档中的嵌入内容。 仅接受 **documentsLibrary** 特殊功能的以上用途。<ul><li>你的应用无法访问手机的内部存储中的文档库。 但是，如果另一个应用在可选 SD 卡上创建“文档”文件夹，你的应用可以看到该文件夹。</li></ul>当在应用的程序包清单中声明 **documentsLibrary** 功能时，该功能必须包含 **uap** 命名空间，如下所示。<div class="code"><span codelanguage="XML"></span><table><colgroup><col width="100%" /></colgroup><thead><tr class="header"><th align="left">XML</th></tr></thead><tbody><tr class="odd"><td align="left"><pre><code>&lt;Capabilities&gt;&lt;uap:Capability Name="documentsLibrary"/&gt;&lt;/Capabilities&gt;</code></pre></td></tr></tbody></table></div>
| **游戏 DVR 设置** | **appCaptureSettings** 受限功能允许应用控制游戏 DVR 的用户设置。<br /><br />若要使用 [**Windows.Media.Capture**](https://msdn.microsoft.com/library/windows/apps/BR226738) 命名空间中的某些 API，则需要此功能。
| **手机网络** | **cellularDeviceControl** 受限功能允许应用控制手机网络设备。<br /><br />**cellularDeviceIdentity** 功能允许应用访问手机网络标识数据。<br /><br />**cellularMessaging** 功能允许应用使用短信和 RCS。<br /><br />若要使用 [**Windows.Devices.Sms**](https://msdn.microsoft.com/library/windows/apps/BR206567) 命名空间中的某些 API，这些功能是必需的。<br /><br />从 Windows 10 开始，调用 [**AppIDList**](https://msdn.microsoft.com/library/windows/apps/Dn393996) 的应用）。
| **设备解锁** | **deviceUnlock** 受限功能允许应用解锁用于开发人员和企业旁加载方案的设备。
| **双重 SIM 卡磁贴** | **dualSimTiles** 受限功能允许应用在具有多张 SIM 卡的设备上创建额外的应用列表项。<br /><br />若要使用 [**Windows.UI.StartScreen**](https://msdn.microsoft.com/library/windows/apps/BR242235) 命名空间中的某些 API，则需要此功能。
| **企业共享存储** | **enterpriseDeviceLockdown** 受限功能允许应用使用设备锁定 API 和访问企业共享存储文件夹。
| **系统输入式注入** | **inputInjection** 受限功能允许应用以编程方式将各种形式的输入（如 HID、触摸、笔、键盘或鼠标）注入系统中。 此功能通常用于可控制系统的协作应用。<br /><br /><div class="alert">**注意** 对于电脑，只有位于同一应用容器中的进程才会收到来自应用的具有此功能的输入式注入。</div>
| **观察输入**\* | **inputObservation** 受限功能允许应用观察要由系统接收的各种形式的原始输入（如 HID、触摸、笔、键盘或鼠标），而不考虑其最终目标。
| **禁止显示输入** | **inputSuppression** 受限功能允许应用隐藏要由系统接收的各种形式的原始输入，例如 HID、触摸、笔、键盘或鼠标。
| **VPN 应用** | **networkingVpnProvider** 受限功能允许应用具有对 VPN 功能的完整访问权限，包括管理连接和提供 VPN 插件功能的能力。<br /><br />若要使用 [**Windows.Networking.Vpn**](https://msdn.microsoft.com/library/windows/apps/Dn434040) 命名空间中的某些 API，则需要此功能。
| **其他应用管理** | **packageManagement** 受限功能允许应用直接管理其他应用。<br /><br />**packageQuery** 设备功能允许应用收集有关其他应用的信息。<br /><br />若要访问 [**PackageManager**](https://msdn.microsoft.com/library/windows/apps/BR240960) 类中的某些方法和属性，这些功能是必需的。
| **屏幕投影** | **screenDuplication** 受限功能允许应用将屏幕投影到另一台设备上。<br /><br />若要使用 DirectX 命名空间中的 API，此功能是必需的。
| **用户主体名称** | **userPrincipalName** 受限功能允许应用修改和访问照片的缩略图缓存。<br /><br />若要调用 [**GetUserNameEx**](https://msdn.microsoft.com/library/windows/desktop/ms724435) 函数，则需要此功能。
| **电子钱包** | **walletSystem** 受限功能允许应用具有对存储的电子钱包卡的完整访问权限。<br /><br />若要使用 [**Windows.ApplicationModel.Wallet.System**](https://msdn.microsoft.com/library/windows/apps/Mt171610) 命名空间中的 API，则需要此功能。
| **位置历史记录** | **locationHistory** 受限功能允许应用访问设备的位置历史记录。<br /><br />若要使用 [**Windows.Devices.Geolocation**](https://msdn.microsoft.com/library/windows/apps/BR225603) 命名空间中的 API，则需要此功能。
| **应用关闭确认** | **confirmAppClose** 受限功能允许应用关闭本身及其自己的窗口，以及延迟应用的关闭。<br /><br />若要使用 [**Windows.UI.ViewManagement**](https://msdn.microsoft.com/library/windows/apps/BR242295) 命名空间中的 API，则需要此功能。
| **呼叫历史记录**\* | **phoneCallHistory** 受限功能允许应用读取呼叫历史记录和删除该历史记录中的条目。<br /><br />若要使用 [**Windows.ApplicationModel.Chat**](https://msdn.microsoft.com/library/windows/apps/Dn642321) 命名空间中的 API，则需要此功能。
| **系统级别约会访问** | **appointmentsSystem** 受限功能允许应用读取和修改用户日历上的所有约会。<br /><br />若要使用 [**Windows.ApplicationModel.Appointment**](https://msdn.microsoft.com/library/windows/apps/Dn263359) 命名空间中的 API，则需要此功能。
| **系统级别聊天消息访问**\* | **chatSystem** 受限功能允许应用读取和写入所有短信和彩信。<br />若要使用 [**Windows.ApplicationModel.Chat**](https://msdn.microsoft.com/library/windows/apps/Dn642321) 命名空间中的 API，则需要此功能。
| **系统级别联系人访问** | **contactsSystem** 受限功能允许应用读取已指定为受限或敏感的联系人信息，以及修改现有的联系人信息。<br /><br />若要使用 [**Windows.ApplicationModel.Chat**](https://msdn.microsoft.com/library/windows/apps/Dn642321) 命名空间中的 API，则需要此功能。
| **电子邮件访问*** | **email** 受限功能允许应用读取、整理和发送用户电子邮件。<br /><br />若要使用 [**Windows.ApplicationModel.Email**](https://msdn.microsoft.com/library/windows/apps/Dn631285) 命名空间中的 API，则需要此功能。
| **系统级别电子邮件访问**| **emailSystem** 受限功能允许应用读取、整理和发送受限或敏感的电子邮件。<br /><br />若要使用 [**Windows.ApplicationModel.Email**](https://msdn.microsoft.com/library/windows/apps/Dn631285) 命名空间中的 API，则需要此功能。
| **系统级别呼叫历史记录访问** | **phoneCallHistorySystem** 受限功能允许应用通过更改现有条目和编写新条目来完全修改呼叫历史记录。<br /><br />若要使用 [**Windows.ApplicationModel.Calls**](https://msdn.microsoft.com/library/windows/apps/Dn297266) 命名空间中的 API，则需要此功能。
| **发送文本消息**\* | **smsSend** 受限功能允许应用发送短信和彩信。<br /><br />若要使用 [**Windows.ApplicationModel.Chat**](https://msdn.microsoft.com/library/windows/apps/Dn642321) 命名空间中的 API，则需要此功能。
| **对所有用户数据的系统级别访问权限** | **userDataSystem** 受限功能允许应用访问用户数据系统数据存储。
| **应用商店预览功能** | **previewStore** 受限功能允许应用检索和购买应用内产品的 SKU。<br /><br />若要使用 [**Windows.ApplicationModel.Store.Preview**](https://msdn.microsoft.com/library/windows/apps/Mt185546) 命名空间中的某些 API，则需要此功能。
| **首次登录设置** | **firstSignInSettings** 受限功能允许应用访问用户首次登录到他们的设备时所设置的用户设置。
| **Windows 团队体验** | **teamEditionExperience** 受限功能允许应用访问用于控制 Windows 团队会话的多个体验式方面的内部 API。 Windows 团队会话可在诸如 Microsoft Surface Hub 等团队设备上运行。
| **远程解锁** | **remotePassportAuthentication** 受限功能允许应用访问可用于解锁远程电脑的凭据。
| **预览合成** | **previewUiComposition** 受限功能允许应用在其用户界面上预览 [**Windows.UI.Composition**](https://msdn.microsoft.com/library/windows/apps/Dn706878) 命名空间，以便它们可在完成前提供有关该 API 的反馈。 有关详细信息，请联系 wincomposition@microsoft.com。
| **安全评估锁定** | **secureAssessment** 受限功能允许应用将 Windows 锁定到单一应用模式以供安全评估。
| **连接管理器预配** | **networkConnectionManagerProvisioning** 受限功能允许应用定义通过 WWAN 与 WLAN 接口连接设备的策略。 使用此功能的应用由移动运营商创建，用来管理连接到其移动网络的设备。
| **流量套餐预配** | **networkDataPlanProvisioning** 受限功能允许应用收集有关设备上流量套餐的信息并读取网络使用情况。 使用此功能的应用由移动运营商创建，用来将其客户的实际数据使用量集成到操作系统数据使用量设置中。
| **软件授权** | **slapiQueryLicenseValue** 受限制功能允许应用查询软件授权策略。
| **扩展执行** | **extendedExecutionBackgroundAudio** 受限功能允许在应用不处于前台时播放音频。<br /><br />**extendedExecutionCritical** 受限功能允许应用开始一个关键扩展执行会话。<br /><br />**extendedExecutionUnconstrained** 受限功能允许应用开始一个不受限制的扩展执行会话。
| **移动设备管理** | **deviceManagementDmAccount** 受限功能允许应用预配和配置移动运营商开放移动联盟 - 设备管理 (MO OMA-DM) 帐户。<br /><br />**deviceManagementFoundation** 受限功能允许应用拥有对设备上的移动设备管理 (MDM) 配置服务提供程序 (CSP) 基础结构的基本访问权限。 请注意，其他功能是访问特定 CSP 时所必需的。<br /><br />**deviceManagementWapSecurityPolicies** 受限功能允许应用配置基于无线应用程序协议 (WAP) 的服务，例如彩信、服务指示/服务加载 (SI/SL)，以及开放移动联盟 - 客户端预配 (OMA-CP)。<br /><br />**deviceManagementEmailAccount** 受限功能允许移动运营商所创建的应用在设备上添加和管理其预配给用户的电子邮件帐户。
| **程序包策略控制** | **packagePolicySystem** 受限功能允许应用拥有对与安装在设备上的应用相关的系统策略的控制权。
| **游戏列表** | **gameList** 受限功能允许应用获取系统上安装的已知游戏列表。
| **Xbox 附件** | **xboxAccessoryManagement** 受限功能允许应用直接管理符合 Xbox 硬件规范的 Xbox 设备。
| **附件的语音识别** | **cortanaSpeechAccessory** 受限功能允许应用调用命令并将命令传递给 Cortana。
| **附件管理** | **accessoryManager** 受限功能允许应用注册为附件应用和选择特定应用通知，以便它们可转发到附件并显示给用户。
| **驱动程序访问** | **interopServices** 受限功能允许应用直接与驱动程序交互。
| **前台观察** | **inputForegroundObservation** 受限功能允许前台应用截获键盘输入并绕过所有非应用键盘输入处理。 无法通过此功能截获 SAS 组合。 若要访问 [**KeyboardDeliveryInterceptor**](https://msdn.microsoft.com/library/windows/apps/Mt608395) 类的成员，则需要此功能。
| **OEM 和 MO 合作伙伴应用** | **oemDeployment** 受限功能允许 Microsoft 合作伙伴创建的应用在设备上安装新应用并查询当前安装的应用。<br /><br />**oemPublicDirectory** 受限功能允许 Microsoft 合作伙伴创建的应用访问共享的应用文件夹。
| **用户数据帐户提供程序** | **userDataAccountsProvider** 受限功能允许应用完全管理邮件、日历和联系人帐户。
| **应用许可** | **appLicensing** 受限功能允许应用无需许可证即可运行。 如果你在清单中声明此功能，则无法将应用提交到应用商店。 任何访问要提交到应用商店的此功能的请求始终都会被拒绝。
| **位置系统**| **locationSystem** 受限功能允许应用执行某些有特权的位置配置，例如设置设备的默认位置。 如果你在清单中声明此功能，则无法将应用提交到应用商店。 任何访问要提交到应用商店的此功能的请求始终都会被拒绝。
| **用户数据帐户提供程序**| **userDataAccountsProvider** 受限功能允许应用完全管理邮件、日历和联系人帐户。



**注意**  
本文适用于编写 UWP 应用的 Windows 10 开发人员。 如果你要针对 Windows 8.x 或 Windows Phone 8.x 进行开发，请参阅[存档文档](http://go.microsoft.com/fwlink/p/?linkid=619132)。

## 相关主题

* [清单设计器](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/br230259.aspx)
* [隐私感知应用指南](https://msdn.microsoft.com/library/windows/apps/Hh768223)
* [如何在程序包清单中指定功能](https://msdn.microsoft.com/library/windows/apps/BR211477)
* [如何在包清单中指定设备功能](https://msdn.microsoft.com/library/windows/apps/Dn263092)
 


<!--HONumber=May16_HO2-->


