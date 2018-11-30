---
Description: Learn how to register your UWP app to receive push notifications that you send from Partner Center.
title: 针对定向推送通知配置应用
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10，uwp，Microsoft Store Services SDK，定向推送通知，合作伙伴中心
ms.assetid: 30c832b7-5fbe-4852-957f-7941df8eb85a
ms.localizationpriority: medium
ms.openlocfilehash: f60780186256e7f78a9596c979c79bfc704ae4c2
ms.sourcegitcommit: d2517e522cacc5240f7dffd5bc1eaa278e3f7768
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "8326343"
---
# <a name="configure-your-app-for-targeted-push-notifications"></a>针对定向推送通知配置应用

可以使用合作伙伴中心中的**推送通知**页面直接通过在其上安装通用 Windows 平台 (UWP) 应用的设备发送定向的推送通知吸引客户。 例如，可以使用定向推送通知鼓励客户采取行动（如为应用评分或试用新功能）。 可以发送多个不同类型的推送通知，包括 Toast 通知、磁贴通知和 XML 原始通知。 还可以跟踪由推送通知导致的应用启动的速度。 有关此功能的详细信息，请参阅[将推送通知发送到应用客户](../publish/send-push-notifications-to-your-apps-customers.md)。

可从合作伙伴中心向客户发送定向的推送通知之前，你必须使用 Microsoft Store Services SDK 中[StoreServicesEngagementManager](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager)类的方法来注册应用以接收通知。 你可以使用此类的其他方法以通知 （如果你想要跟踪的应用启动的通知导致的速度），你的应用已启动响应定向的推送通知的合作伙伴中心; 若要停止接收通知。

## <a name="configure-your-project"></a>配置项目

在编写任何代码之前，请遵循以下步骤在你的项目中添加对 Microsoft Store Services SDK 的引用：

1. 如果先前尚未这样做，请在开发计算机上[安装 Microsoft Store Services SDK](microsoft-store-services-sdk.md#install-the-sdk)。 
2. 在 Visual Studio 中打开你的项目。
3. 在“解决方案资源管理器”中，右键单击你的项目的**引用**节点，然后单击**添加引用**。
4. 在**引用管理器**中，展开**通用 Windows** 并单击**扩展**。
5. 在 SDK 列表中，单击 **Microsoft 协议框架**旁边的复选框，然后单击**确定**。

## <a name="register-for-push-notifications"></a>注册推送通知

若要注册应用以从合作伙伴中心接收定向的推送通知：

1. 在项目中，找到启动过程中运行的代码部分，可以在其中注册用于接收通知的应用。
2. 将以下语句添加到代码文件顶部。

    [!code-cs[DevCenterNotifications](./code/StoreSDKSamples/cs/DevCenterNotifications.cs#EngagementNamespace)]

3. 在之前确定的启动代码中，获取 [StoreServicesEngagementManager](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager) 对象，并调用其中一个 [RegisterNotificationChannelAsync](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.registernotificationchannelasync) 重载。 每次启动应用时，都应该调用此方法。

  * 如果你想要创建其自己的通道 URI 通知的合作伙伴中心，调用[registernotificationchannelasync （）](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.registernotificationchannelasync)重载。

      [!code-cs[DevCenterNotifications](./code/StoreSDKSamples/cs/DevCenterNotifications.cs#RegisterNotificationChannelAsync1)]
      > [!IMPORTANT]
      > 如果应用还会调用 [CreatePushNotificationChannelForApplicationAsync](https://docs.microsoft.com/uwp/api/windows.networking.pushnotifications.pushnotificationchannelmanager.createpushnotificationchannelforapplicationasync) 为 WNS 创建通知通道，请确保代码不会同时调用 [CreatePushNotificationChannelForApplicationAsync](https://docs.microsoft.com/uwp/api/windows.networking.pushnotifications.pushnotificationchannelmanager.createpushnotificationchannelforapplicationasync) 和 [RegisterNotificationChannelAsync()](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.registernotificationchannelasync) 重载。 如果需要调用这两个方法，请确保按序调用它们，即等待一个方法返回，然后再调用另一个方法。

  * 如果你想要指定的通道 URI，用于从合作伙伴中心的定向的推送通知，请调用[registernotificationchannelasync （storeservicesnotificationchannelparameters）](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.registernotificationchannelasync)重载。 例如，在应用已使用 Windows 推送通知服务 (WNS) 并且想要使用同一通道 URI 时，可能希望这样做。 必须先创建 [StoreServicesNotificationChannelParameters](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesnotificationchannelparameters) 对象，并将 [CustomNotificationChannelUri](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesnotificationchannelparameters.customnotificationchanneluri) 属性分配给你的通道 URI。

      [!code-cs[DevCenterNotifications](./code/StoreSDKSamples/cs/DevCenterNotifications.cs#RegisterNotificationChannelAsync2)]

> [!NOTE]
> 调用 **RegisterNotificationChannelAsync** 方法时，将会在本地应用数据存储器中为你的应用创建一个名为 MicrosoftStoreEngagementSDKId.txt 的文件（由 [ApplicationData.LocalFolder](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData.LocalFolder) 属性返回的文件夹）。 此文件包含供定向推送通知基础结构使用的 ID。 确保你的应用不会修改或删除此文件。 否则，用户可能会收到多个通知实例，或者通知可能不会以其他方式正常运行。

<span id="notification-customers" />

### <a name="how-targeted-push-notifications-are-routed-to-customers"></a>定向推送通知如何路由至客户

当你的应用调用 **RegisterNotificationChannelAsync** 时，此方法将会收集当前已登录到设备的客户的 Microsoft 帐户。 更高版本，当定向的推送通知发送至包含此客户的类别时，合作伙伴中心将通知发送到与此客户的 Microsoft 帐户相关联的设备。

请注意，如果客户已启动你的应用并在使用其 Microsoft 帐户登录到设备的状态下将设备交给其他人使用，请注意其他用户可能会看到面向最初客户的通知。 这可能会产生意外结果，尤其是对于那些提供客户可登录使用服务的应用。 若要在此情况下使其他用户无法看到定向通知，请在客户注销应用时调用 [UnregisterNotificationChannelAsync](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.unregisternotificationchannelasync) 方法。 有关详细信息，请参阅本文后面的[注销推送通知](#unregister)。

### <a name="how-your-app-responds-when-the-user-launches-your-app"></a>应用在用户启动应用时如何响应

注册应用以接收通知和你[发送推送通知向你的应用客户从合作伙伴中心](../publish/send-push-notifications-to-your-apps-customers.md)后，你的应用中的以下入口点之一时将会调用用户启动你的应用中响应你推送通知。 如果有一些代码想要在用户启动应用时运行，可以将该代码添加到应用中的这些入口点之一。

  * 如果推送通知中含有前台激活类型，请覆盖项目中 **App** 类的 [OnActivated](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onactivated) 方法，然后向该方法中添加你的代码。

  * 如果推送通知中含有后台激活类型，请将你的代码添加到[后台任务](../launch-resume/support-your-app-with-background-tasks.md)的 [Run](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.ibackgroundtask.run) 方法中。

例如，你可能想要通过以下方式对在你的应用中购买过任何付费加载项的用户进行奖励：给予这些用户免费的加载项。 在此情况下，可以将推送通知发送给面向这些用户的[客户群](../publish/create-customer-segments.md)。 然后，可以在上述所列的其中一个入口点中添加用于给予他们免费[应用内购买](in-app-purchases-and-trials.md)的代码。

## <a name="notify-partner-center-of-your-app-launch"></a>通知的应用启动的合作伙伴中心

如果你选择定向的推送通知合作伙伴中心中的**跟踪应用启动速率**选项，从你的应用通知应用的合作伙伴中心中的相应入口点调用[ParseArgumentsAndTrackAppLaunch](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.parseargumentsandtrackapplaunch)方法启动响应推送通知。

该方法还会返回应用的原始启动参数。 当你选择跟踪推送通知的应用启动速率时，将不透明跟踪 ID 添加到启动参数，以帮助跟踪应用启动在合作伙伴中心。 你必须将你的应用的启动参数传递给[ParseArgumentsAndTrackAppLaunch](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.parseargumentsandtrackapplaunch)方法中，并且此方法将跟踪 ID 发送到合作伙伴中心，从启动参数，删除跟踪 ID 并返回到原始启动参数你代码。

调用此方法的方式取决于推送通知的激活类型：

* 如果推送通知中含有前台激活类型，请从应用的 [OnActivated](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onactivated) 方法重写中调用此方法，然后传递在向此方法传递的 [ToastNotificationActivatedEventArgs](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ToastNotificationActivatedEventArgs) 对象中可用的参数。 以下代码示例假设你的代码文件中 **Microsoft.Services.Store.Engagement** 和 **Windows.ApplicationModel.Activation** 命名空间具有 **using** 语句。

  [!code-cs[DevCenterNotifications](./code/StoreSDKSamples/cs/App.xaml.cs#OnActivated)]

* 如果推送通知中含有后台激活类型，请从[后台任务](../launch-resume/support-your-app-with-background-tasks.md)的 [Run](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.ibackgroundtask.run) 方法中调用此方法，然后传递在向此方法传递的 [ToastNotificationActionTriggerDetail](https://docs.microsoft.com/uwp/api/Windows.UI.Notifications.ToastNotificationActionTriggerDetail) 对象中可用的参数。 以下代码示例假设你的代码文件中已有 **Microsoft.Services.Store.Engagement**、**Windows.ApplicationModel.Background** 和 **Windows.UI.Notifications** 命名空间的 **using** 语句。

  [!code-cs[DevCenterNotifications](./code/StoreSDKSamples/cs/DevCenterNotifications.cs#Run)]

<span id="unregister" />

## <a name="unregister-for-push-notifications"></a>注销推送通知

如果想要应用停止接收来自合作伙伴中心的定向的推送通知，请调用[UnregisterNotificationChannelAsync](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager.unregisternotificationchannelasync)方法。

[!code-cs[DevCenterNotifications](./code/StoreSDKSamples/cs/DevCenterNotifications.cs#UnregisterNotificationChannelAsync)]

请注意，此方法会使用于通知的通道失效，因此该应用不再从*任何*服务接收推送通知。 已关闭后，该通道无法用于任何服务，包括从合作伙伴中心的定向的推送通知和使用 WNS 的其他通知再次使用。 若要恢复向此应用发送推送通知，该应用必须请求新的通道。

## <a name="related-topics"></a>相关主题

* [向应用客户发送推送通知](../publish/send-push-notifications-to-your-apps-customers.md)
* [Windows 推送通知服务 (WNS) 概述](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview)
* [如何请求、创建和保存通知通道](https://docs.microsoft.com/previous-versions/windows/apps/hh868221(v=win.10))
* [Microsoft Store Services SDK](https://docs.microsoft.com/windows/uwp/monetize/microsoft-store-services-sdk)
