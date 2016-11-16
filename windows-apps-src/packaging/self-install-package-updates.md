---
author: mcleanbyron
ms.assetid: 414ACC73-2A72-465C-BD15-1B51CB2334F2
title: "为你的应用下载并安装程序包更新"
description: "了解如何在开发人员中心仪表板中将程序包标记为必需，以及如何在应用中编写代码以下载并安装程序包更新。"
translationtype: Human Translation
ms.sourcegitcommit: b96d4074a8960db314313c612955900c6a05dc48
ms.openlocfilehash: 4da8ffe72435501876a1e859d10a16cf19eb11fd

---
# 为你的应用下载并安装程序包更新

\[ 已针对 Windows10 上的 UWP 应用更新。 有关 Windows8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

从 Windows10 版本 1607 开始，你可以使用 [Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx) 命名空间中的 API，以编程方式检查当前应用中的程序包更新，下载并安装更新的程序包。 还可以查询已[在 Windows 开发人员中心仪表板上标记为必需](#mandatory-dashboard)的程序包，并在安装必需更新前禁用应用中的功能。

这些功能有助于通过最新版本的应用和相关服务，自动使你的用户群保持最新状态。

## API 概述

面向 Windows10 版本 1607 或更高版本的应用可以使用 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 类中的以下方法下载并安装包更新。

|  方法  |  说明  |
|----------|---------------|
| [GetAppAndOptionalStorePackageUpdatesAsync](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.getappandoptionalstorepackageupdatesasync.aspx) | 调用此方法来获取可用的包更新列表。<br/><br/>
            **重要提示**
            &nbsp;&nbsp;软件包通过认证过程时和 [GetAppAndOptionalStorePackageUpdatesAsync](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.getappandoptionalstorepackageupdatesasync.aspx) 方法识别包更新可用于应用时之间的延迟不超过一天。 |
| [RequestDownloadStorePackageUpdatesAsync](https://msdn.microsoft.com/library/windows/apps/mt706586.aspx) | 调用此方法来下载（但不安装）可用的包更新。 此操作系统显示询问用户下载更新的权限的对话框， |
| [RequestDownloadAndInstallStorePackageUpdatesAsync](https://msdn.microsoft.com/library/windows/apps/mt706585.aspx) | 调用此方法来下载并安装可用的包更新。 操作系统显示询问用户下载并安装更新的权限的对话框。 如果已通过调用 [RequestDownloadStorePackageUpdatesAsync](https://msdn.microsoft.com/library/windows/apps/mt706586.aspx) 下载包更新，此方法将跳过下载过程并仅安装更新。  |

<span/>

这些方法使用 [StorePackageUpdate](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storepackageupdate.aspx) 对象表示可用的更新包。 使用以下 [StorePackageUpdate](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storepackageupdate.aspx) 属性获取关于更新包的信息。

|  属性  |  说明  |
|----------|---------------|
| [Mandatory](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storepackageupdate.mandatory.aspx) | 使用此属性确定软件包是否已在开发人员中心仪表板中标记为必需。 |
| [Package](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storepackageupdate.package.aspx) | 使用此属性访问基础软件包相关数据。 |

<span/>

## 代码示例

以下代码示例演示了如何在你的应用中下载并安装程序包更新。 以下示例假设：
* 代码在 [Page](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.page.aspx) 的上下文中运行。
* 
            **Page** 包含名为 ```downloadProgressBar``` 的 [ProgressBar](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.progressbar.aspx)，可提供下载操作的状态。
* 代码文件有一个适用于 [Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx) 命名空间的 **using** 语句。
* 该应用是单用户应用，仅在启动该应用的用户上下文中运行。 对于[多用户应用](https://msdn.microsoft.com/windows/uwp/xbox-apps/multi-user-applications)，使用 [GetForUser](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.getforuser.aspx) 方法（而不是 [GetDefault](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.getdefault.aspx) 方法）获取 [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) 对象。

<span/>

### 下载并安装所有程序包更新

以下代码示例演示了如何下载并安装所有可用的程序包更新。  

```csharp
private StoreContext context = null;

public async Task DownloadAndInstallAllUpdatesAsync()
{
    if (context == null)
    {
        context = StoreContext.GetDefault();
    }

    // Get the updates that are available.
    IReadOnlyList<StorePackageUpdate> updates =
        await context.GetAppAndOptionalStorePackageUpdatesAsync();

    if (updates.Count > 0)
    {
        // Alert the user that updates are available and ask for their consent
        // to start the updates.
        MessageDialog dialog = new MessageDialog(
            "Download and install updates now? This may cause the application to exit.", "Download and Install?");
        dialog.Commands.Add(new UICommand("Yes"));
        dialog.Commands.Add(new UICommand("No"));
        IUICommand command = await dialog.ShowAsync();

        if (command.Label.Equals("Yes", StringComparison.CurrentCultureIgnoreCase))
        {
            // Download and install the updates.
            IAsyncOperationWithProgress<StorePackageUpdateResult, StorePackageUpdateStatus> downloadOperation =
                context.RequestDownloadAndInstallStorePackageUpdatesAsync(updates);

            // The Progress async method is called one time for each step in the download
            // and installation process for each package in this request.
            downloadOperation.Progress = async (asyncInfo, progress) =>
            {
                await this.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                () =>
                {
                    downloadProgressBar.Value = progress.PackageDownloadProgress;
                });
            };

            StorePackageUpdateResult result = await downloadOperation.AsTask();
        }
    }
}
```

### 处理必需程序包更新

以下代码示例基于以前的示例生成，演示了如何确定是否有任何更新程序包已[在 Windows 开发人员中心仪表板上标记为必需](#mandatory-dashboard)。 通常，如果无法成功下载或安装必需程序包更新，应顺利降级用户的应用体验。

```csharp
private StoreContext context = null;

// Downloads and installs package updates in separate steps.
public async Task DownloadAndInstallAllUpdatesAsync()
{
    if (context == null)
    {
        context = StoreContext.GetDefault();
    }  
    // Get the updates that are available.
    IReadOnlyList<StorePackageUpdate> updates =
        await context.GetAppAndOptionalStorePackageUpdatesAsync();

    if (updates.Count != 0)
    {
        // Download the packages.
        bool downloaded = await DownloadPackageUpdatesAsync(updates);

        if (downloaded)
        {
            // Install the packages.
            await InstallPackageUpdatesAsync(updates);
        }
    }
}

// Helper method for downloading package updates.
private async Task<bool> DownloadPackageUpdatesAsync(IEnumerable<StorePackageUpdate> updates)
{
    bool downloadedSuccessfully = false;

    IAsyncOperationWithProgress<StorePackageUpdateResult, StorePackageUpdateStatus> downloadOperation =
        this.context.RequestDownloadStorePackageUpdatesAsync(updates);

    // The Progress async method is called one time for each step in the download process for each
    // package in this request.
    downloadOperation.Progress = async (asyncInfo, progress) =>
    {
        await this.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
        () =>
        {
            downloadProgressBar.Value = progress.PackageDownloadProgress;
        });
    };

    StorePackageUpdateResult result = await downloadOperation.AsTask();

    switch (result.OverallState)
    {
        case StorePackageUpdateState.Completed:
            downloadedSuccessfully = true;
            break;
        default:
            // Get the failed updates.
            var failedUpdates = result.StorePackageUpdateStatuses.Where(
                status => status.PackageUpdateState != StorePackageUpdateState.Completed);

            // See if any failed updates were mandatory
            if (updates.Any(u => u.Mandatory && failedUpdates.Any(
                failed => failed.PackageFamilyName == u.Package.Id.FamilyName)))
            {
                // At least one of the updates is mandatory. Perform whatever actions you
                // want to take for your app: for example, notify the user and disable
                // features in your app.
                HandleMandatoryPackageError();
            }
            break;
    }

    return downloadedSuccessfully;
}

// Helper method for installing package updates.
private async Task InstallPackageUpdatesAsync(IEnumerable<StorePackageUpdate> updates)
{
    IAsyncOperationWithProgress<StorePackageUpdateResult, StorePackageUpdateStatus> installOperation =
        this.context.RequestDownloadAndInstallStorePackageUpdatesAsync(updates);

    // The package updates were already downloaded separately, so this method skips the download
    // operatation and only installs the updates; no download progress notifications are provided.
    StorePackageUpdateResult result = await installOperation.AsTask();

    switch (result.OverallState)
    {
        case StorePackageUpdateState.Completed:
            break;
        default:
            // Get the failed updates.
            var failedUpdates = result.StorePackageUpdateStatuses.Where(
                status => status.PackageUpdateState != StorePackageUpdateState.Completed);

            // See if any failed updates were mandatory
            if (updates.Any(u => u.Mandatory && failedUpdates.Any(failed => failed.PackageFamilyName == u.Package.Id.FamilyName)))
            {
                // At least one of the updates is mandatory, so tell the user.
                HandleMandatoryPackageError();
            }
            break;
    }
}

// Helper method for handling the scenario where a mandatory package update fails to
// download or install. Add code to this method to perform whatever actions you want
// to take, such as notifying the user and disabling features in your app.
private void HandleMandatoryPackageError()
{
}
```

<span id="mandatory-dashboard" />
## 在开发人员中心仪表板中使程序包提交为必需

当为面向 Windows10 版本 1607 或更高版本的应用创建程序包提交时，可以将该程序包标记为必需并标记变为必需的日期/时间。 当设置此属性，并且你的应用发现可使用本文前面部分中所述的 API 提供包更新时，你的应用可以确定该更新包是否为必需，并在安装更新前更改其行为（例如你的应用可以禁用功能）。

>
            **注意**
            &nbsp;&nbsp;Microsoft 不强制包更新处于必需状态，并且操作系统不提供向用户指示必须安装必需更新应用的 UI。 开发人员旨在使用必需设置通过其自己的代码强制执行必需的应用更新。  

若要将软件包提交标记为必需：

1. 登录到[开发人员中心仪表板](https://dev.windows.com/overview)并导航到你的应用的概述页面。
2. 单击包含要成为必需的程序包更新的提交名称。
3. 导航到提交的“程序包”页面。 在此页面底部附近，选择“使此更新为必需”，然后选择该程序包更新变为必需的日期和时间。 此选项适用于提交中的所有 UWP 程序包。

有关在开发人员中心仪表板中配置软件包的详细信息，请参阅[上传应用包](https://msdn.microsoft.com/windows/uwp/publish/upload-app-packages)。

  >
            **注意**
            &nbsp;&nbsp;如果你创建[软件包外部测试版](https://msdn.microsoft.com/windows/uwp/publish/package-flights)，可在外部测试版的“软件包”页面上使用类似 UI 将软件包标记为必需。 在此情况下，必需包更新仅适用于属于外部测试版组的客户。



<!--HONumber=Nov16_HO1-->


