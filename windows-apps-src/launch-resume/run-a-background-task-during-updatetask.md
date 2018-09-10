---
author: TylerMSFT
title: 在 UWP 应用更新时运行后台任务
description: 了解如何创建在通用 Windows 平台 (UWP) 应用商店应用更新时运行的后台任务。
ms.author: twhitney
ms.date: 04/21/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp、 更新、 后台任务、 updatetask，后台任务
ms.localizationpriority: medium
ms.openlocfilehash: fcba2cb736f86cebc6d2664e2ec3b557d47c86d7
ms.sourcegitcommit: f5cf806a595969ecbb018c3f7eea86c7a34940f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2018
ms.locfileid: "3824021"
---
# <a name="run-a-background-task-when-your-uwp-app-is-updated"></a>在 UWP 应用更新时运行后台任务

了解如何编写后台任务在通用 Windows 平台 (UWP) 应用商店应用更新后运行。

用户向应用安装在设备上安装更新后，将由操作系统调用更新任务后台任务。 这允许你的应用执行初始化任务，例如初始化新的推送通知通道，更新数据库架构，依此类推之前在用户启动已更新的应用。

更新任务不同于启动后台任务使用[ServicingComplete](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemTriggerType)触发器，因为在这种情况下你的应用必须至少运行一次更新若要注册**将激活后台任务之前ServicingComplete**触发器。  更新任务未注册，因此，永远不会运行，但的升级后，应用将仍然拥有触发其更新任务。

## <a name="step-1-create-the-background-task-class"></a>步骤 1： 创建后台任务类

作为与其他类型的后台任务，你应实现更新任务后台任务作为 Windows 运行时组件。 若要创建此组件，请按照[创建和注册进程外后台任务](https://docs.microsoft.com/windows/uwp/launch-resume/create-and-register-a-background-task)的**创建后台任务类**部分。 包括以下步骤：

- 将一个 Windows 运行时组件项目添加到你的解决方案。
- 为组件，从你的应用中创建的引用。
- 在组件中创建公共、 密封类实现[**IBackgroundTask**](https://msdn.microsoft.com/library/windows/apps/br224794)。
- 实现[**Run**](https://msdn.microsoft.com/library/windows/apps/br224811)方法，即当更新任务运行时调用的所需的入口点。 如果你要从你的后台任务的异步调用，[创建和注册进程外后台任务](https://docs.microsoft.com/windows/uwp/launch-resume/create-and-register-a-background-task)将介绍了如何在你**运行**的方法使用延迟。

你无需注册此后台任务 （"注册要运行的后台任务"部分中**创建和注册进程外后台任务**主题） 用于更新任务。 这是因为你无需将任何代码添加到你的应用可以注册该任务，并且应用无需至少运行一次更新，以注册后台任务才能使用更新任务的主要原因。

下面的示例代码显示在 C# 中更新任务后台任务类的基本起始点。 后台任务类本身和后台任务项目中的所有其他类-需要是**公共**和**密封**。 后台任务类必须从**IBackgroundTask**和公共**run （）** 方法具有如下所示的签名：

```cs
using Windows.ApplicationModel.Background;

namespace BackgroundTasks
{
    public sealed class UpdateTask : IBackgroundTask
    {
        public void Run(IBackgroundTaskInstance taskInstance)
        {
            // your app migration/update code here
        }
    }
}
```

## <a name="step-2-declare-your-background-task-in-the-package-manifest"></a>步骤 2： 将你的后台任务在程序包清单中声明

在 Visual Studio 解决方案资源管理器，右键单击**Package.appxmanifest** ，然后单击**查看代码**以查看程序包清单。 添加以下`<Extensions>`XML 声明你的更新任务：

```XML
<Package ...>
    ...
  <Applications>  
    <Application ...>  
        ...
      <Extensions>  
        <Extension Category="windows.updateTask"  EntryPoint="BackgroundTasks.UpdateTask">  
        </Extension>  
      </Extensions>

    </Application>  
  </Applications>  
</Package>
```

在上述 XML 中，确保`EntryPoint`属性设置为更新任务类的 namespace.class 名称。 该名称是区分大小写。

## <a name="step-3-debugtest-your-update-task"></a>步骤 3： 调试/测试更新任务

确保你已部署你的应用到你的计算机，以便要更新的东西。

在你的后台任务的 run （） 方法中设置断点。

![设置断点](images/run-func-breakpoint.png)

接下来，在解决方案资源管理器，右键单击你的应用的项目 （不后台任务项目），然后单击**属性**。 在应用程序属性窗口中，在左侧，单击**调试**，然后选择**不启动，但调试代码在启动时**：

![设置调试设置](images/do-not-launch-but-debug.png)

接下来，若要确保触发 UpdateTask，增加程序包的版本号。 在解决方案资源管理器，双击你的应用的**Package.appxmanifest**文件，以打开程序包设计器，并更新**内部**版本号：

![更新的版本](images/bump-version.png)

现在，Visual Studio 2017 中按 F5 时，将更新你的应用，系统将激活后台 UpdateTask 组件。 调试程序将自动连接到后台进程。 将获取命中断点，然后可以单步执行更新代码逻辑。

后台任务完成后，你可以在同一调试会话内启动 Windows 开始菜单中的前台应用。 调试程序将再次自动连接到你的前台进程，这次和可以单步执行你的应用的逻辑。

> [!NOTE]
> Visual Studio 2015 用户： 上述步骤适用于 Visual Studio 2017。 如果你使用的 Visual Studio 2015，可以使用触发器和 UpdateTask，除 Visual Studio 将附加到它的测试相同的技术。 在 VS 2015 中的其他步骤是设置为入口点，设置 UpdateTask [ApplicationTrigger](https://docs.microsoft.com/windows/uwp/launch-resume/trigger-background-task-from-app)并触发直接从前台应用执行。

## <a name="see-also"></a>另请参阅

[创建和注册进程外后台任务](https://docs.microsoft.com/windows/uwp/launch-resume/create-and-register-a-background-task)
