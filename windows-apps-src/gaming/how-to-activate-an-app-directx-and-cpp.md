---
author: mtoepke
title: "如何激活应用（DirectX 和 C++）"
description: "本主题介绍了如何为通用 Windows 平台 (UWP) DirectX 应用定义激活体验。"
ms.assetid: b07c7da1-8a5e-5b57-6f77-6439bf653a53
translationtype: Human Translation
ms.sourcegitcommit: 6530fa257ea3735453a97eb5d916524e750e62fc
ms.openlocfilehash: 0b13604d2b0349817881a5c1c56c311931c90759

---

# 如何激活应用（DirectX 和 C++）


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

本主题介绍了如何为通用 Windows 平台 (UWP) DirectX 应用定义激活体验。

## 注册应用激活事件处理程序


首先，注册以处理 [**CoreApplicationView::Activated**](https://msdn.microsoft.com/library/windows/apps/br225018) 事件，当启动你的应用并由操作系统对你的应用进行初始化时会引发该事件。

将此代码添加到你的查看提供程序（在此示例中称为 **MyViewProvider**）的 [**IFrameworkView::Initialize**](https://msdn.microsoft.com/library/windows/apps/hh700495) 方法的实现中：

```cpp
void App::Initialize(CoreApplicationView^ applicationView)
{
    // Register event handlers for the app lifecycle. This example includes Activated, so that we
    // can make the CoreWindow active and start rendering on the window.
    applicationView->Activated +=
        ref new TypedEventHandler<CoreApplicationView^, IActivatedEventArgs^>(this, &App::OnActivated);
  
  //...

}
```

## 为应用激活 CoreWindow 实例


当你的应用启动时，你必须为你的应用获取对 [**CoreWindow**](https://msdn.microsoft.com/library/windows/apps/br208225) 的引用。 **CoreWindow** 包含你的应用用于处理窗口事件的窗口事件消息调度程序。 通过调用 [**CoreWindow::GetForCurrentThread**](https://msdn.microsoft.com/library/windows/apps/hh701589) 在你的回调中为应用激活事件获取此引用。 获取此引用后，通过调用 [**CoreWindow::Activate**](https://msdn.microsoft.com/library/windows/apps/br208254) 激活主应用窗口。

```cpp
void App::OnActivated(CoreApplicationView^ applicationView, IActivatedEventArgs^ args)
{
    // Run() won't start until the CoreWindow is activated.
    CoreWindow::GetForCurrentThread()->Activate();
}
```

## 为主屏窗口启动处理事件消息


对于应用的 [**CoreWindow**](https://msdn.microsoft.com/library/windows/apps/br208225)，你的回调作为由 [**CoreDispatcher**](https://msdn.microsoft.com/library/windows/apps/br208211) 处理的事件消息发生。 如果你未从你的应用的主回路调用 [**CoreDispatcher::ProcessEvents**](https://msdn.microsoft.com/library/windows/apps/br208215)（在你的查看提供程序的 [**IFrameworkView::Run**](https://msdn.microsoft.com/library/windows/apps/hh700505) 方法中实现），将不会调用此回调。

``` syntax
// This method is called after the window becomes active.
void App::Run()
{
    while (!m_windowClosed)
    {
        if (m_windowVisible)
        {
            CoreWindow::GetForCurrentThread()->Dispatcher->ProcessEvents(CoreProcessEventsOption::ProcessAllIfPresent);

            m_main->Update();

            if (m_main->Render())
            {
                m_deviceResources->Present();
            }
        }
        else
        {
            CoreWindow::GetForCurrentThread()->Dispatcher->ProcessEvents(CoreProcessEventsOption::ProcessOneAndAllPending);
        }
    }
}
```

## 相关主题


* [如何暂停应用（DirectX 和 C++）](how-to-suspend-an-app-directx-and-cpp.md)
* [如何恢复应用（DirectX 和 C++）](how-to-resume-an-app-directx-and-cpp.md)

 

 







<!--HONumber=Aug16_HO3-->


