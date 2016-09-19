---
author: TylerMSFT
title: "将应用服务转换为在与其提供程序相同的进程中运行"
description: "将在单独的后台进程中运行的应用服务代码转换为在与应用服务提供程序相同的进程中运行的代码。"
translationtype: Human Translation
ms.sourcegitcommit: 9e959a8ae6bf9496b658ddfae3abccf4716957a3
ms.openlocfilehash: 0990e9938bb9bf1794cf58c5541a64f22853b093

---

# 将应用服务转换为在与其提供程序相同的进程中运行

[AppServiceConnection](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.appservice.appserviceconnection.aspx) 使其他应用程序可以在后台唤醒你的应用，并建立与它的直接通信。

引入单进程应用服务后，两个正在运行的前台应用程序可通过应用服务连接建立直接通信。 应用服务现在在无需将服务代码分离到独立项目的同时，还可以在与前台应用程序相同的进程中运行，这简化了应用之间的通信。

将多进程模型的应用服务转换为单进程模型需要两项更改。 第一项是清单更改。

> ```xml
>  <uap:Extension Category="windows.appService">
>          <uap:AppService Name="SingleProcessAppService" />
>  </uap:Extension>
> ```

删除 `EntryPoint` 属性。 在调用应用服务后，[OnBackgroundActivated()](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.application.onbackgroundactivated.aspx) 回调将用作回调方法。

第二项更改是将服务逻辑从其单独的后台任务项目移动至可从 **OnBackgroundActivated()** 调用的方法。

此时，应用程序可直接运行应用服务。  例如：

> ``` cs
> private AppServiceConnection appServiceconnection;
> private BackgroundTaskDeferral appServiceDeferral;
> protected override async void OnBackgroundActivated(BackgroundActivatedEventArgs args)
> {
>     base.OnBackgroundActivated(args);
>     IBackgroundTaskInstance taskInstance = args.TaskInstance;
>     AppServiceTriggerDetails appService = taskInstance.TriggerDetails as AppServiceTriggerDetails;
>     appServiceDeferral = taskInstance.GetDeferral();
>     taskInstance.Canceled += OnAppServicesCanceled;
>     appServiceConnection = appService.AppServiceConnection;
>     appServiceConnection.RequestReceived += OnAppServiceRequestReceived;
>     appServiceConnection.ServiceClosed += AppServiceConnection_ServiceClosed;
> }
>
> private async void OnAppServiceRequestReceived(AppServiceConnection sender, AppServiceRequestReceivedEventArgs args)
> {
>     AppServiceDeferral messageDeferral = args.GetDeferral();
>     ValueSet message = args.Request.Message;
>     string text = message["Request"] as string;
>              
>     if ("Value" == text)
>     {
>         ValueSet returnMessage = new ValueSet();
>         returnMessage.Add("Response", "True");
>         await args.Request.SendResponseAsync(returnMessage);
>     }
>     messageDeferral.Complete();
> }
>
> private void OnAppServicesCanceled(IBackgroundTaskInstance sender, BackgroundTaskCancellationReason reason)
> {
>     appServiceDeferral.Complete();
> }
>
> private void AppServiceConnection_ServiceClosed(AppServiceConnection sender, AppServiceClosedEventArgs args)
> {
>     appServiceDeferral.Complete();
> }
> ```

在上述代码中，`OnBackgroundActivated` 方法处理应用服务激活。 通过 [AppServiceConnection](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.appservice.appserviceconnection.aspx) 进行通信所需的所有事件均已注册，并且任务延迟对象已存储，以便在应用程序之间的通信完成时可标记为“完成”。

在应用收到请求并读取所提供的 [ValueSet](https://msdn.microsoft.com/library/windows/apps/windows.foundation.collections.valueset.aspx) 时，查看是否存在 `Key` 和 `Value` 字符串。 如果存在，则应用服务会将一对 `Response` 和 `True` 字符串值返回到 **AppServiceConnection** 另一侧的应用上。

请在[创建和使用应用服务](https://msdn.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service?f=255&MSPPError=-2147217396)中了解关于连接和与其他应用通信的详细信息。



<!--HONumber=Aug16_HO3-->


