---
ms.assetid: E2A1200C-9583-40FA-AE4D-C9E6F6C32BCF
title: 向线程池提交工作项
description: 了解如何通过向线程池提交工作项，在单独的线程中完成工作。
---
# 向线程池提交工作项

\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

** 重要的 API **

-   [**RunAsync**](https://msdn.microsoft.com/library/windows/apps/BR230593)
-   [**IAsyncAction**](https://msdn.microsoft.com/library/windows/apps/BR206580)

了解如何通过向线程池提交工作项，在单独的线程中完成工作。 使用此快速入门可维护 UI 快速响应，同时仍然可以完成需要花费大量时间来完成的工作，并且可以使用它来并行完成多个任务。

## 创建和提交工作项

通过调用 [**RunAsync**](https://msdn.microsoft.com/library/windows/apps/BR230593) 创建工作项。 提供委派来完成工作（你可使用一个 lambda 或 delegate 函数）。 请注意，**RunAsync** 返回 [**IAsyncAction**](https://msdn.microsoft.com/library/windows/apps/BR206580) 对象；存储此对象以用于下一个步骤。

[
            **RunAsync**](https://msdn.microsoft.com/library/windows/apps/BR230593) 有 3 个版本，你可指定工作项的优先级，控制它是否与其他工作项同时运行。

**注意** 使用 [**CoreDispatcher.RunAsync**](https://msdn.microsoft.com/library/windows/apps/Hh750317) 访问 UI 线程并显示工作项的进度。

以下示例创建工作项并提供 lambda 以执行此工作：

> [!div class="tabbedCodeSnippets"]
``` cpp
// The nth prime number to find.
const unsigned int n = 9999;

// A shared pointer to the result.
// We use a shared pointer to keep the result alive until the 
// thread is done.
std::shared_ptr&lt;unsigned long&gt; nthPrime = make_shared&lt;unsigned long int&gt;(0);

// Simulates work by searching for the nth prime number. Uses a
// naive algorithm and counts 2 as the first prime number.
auto workItem = ref new WorkItemHandler(
    \[this, n, nthPrime](IAsyncAction^ workItem)
{
    unsigned int progress = 0; // For progress reporting.
    unsigned int primes = 0;   // Number of primes found so far.
    unsigned long int i = 2;   // Number iterator.

    if ((n &gt;= 0) &amp;&amp; (n &lt;= 2))
    {
        *nthPrime = n;
        return;
    }

    while (primes &lt; (n - 1))
    {
        if (workItem-&gt;Status == AsyncStatus::Canceled)
        {
            break;
        }

        // Go to the next number.
        i++;

        // Check for prime.
        bool prime = true;
        for (unsigned int j = 2; j &lt; i; ++j)
        {
            if ((i % j) == 0)
            {
                prime = false;
                break;
            }
        };

        if (prime)
        {
            // Found another prime number.
            primes++;

            // Report progress at every 10 percent.
            unsigned int temp = progress;
            progress = static_cast&lt;unsigned int&gt;(10.f*primes / n);

            if (progress != temp)
            {
                String^ updateString;
                updateString = "Progress to " + n + "th prime: "
                    + (10 * progress).ToString() + "%\n";

                // Update the UI thread with the CoreDispatcher.
                CoreApplication::MainView-&gt;CoreWindow-&gt;Dispatcher-&gt;RunAsync(
                    CoreDispatcherPriority::High,
                    ref new DispatchedHandler([this, updateString]()
                {
                    UpdateUI(updateString);
                }));
            }
        }
    }

    // Return the nth prime number.
    *nthPrime = i;
});

auto asyncAction = ThreadPool::RunAsync(workItem);

// A reference to the work item is cached so that we can trigger a 
// cancellation when the user presses the Cancel button.
m_workItem = asyncAction;
```
``` csharp
// The nth prime number to find.
const uint n = 9999;

// A shared pointer to the result.
// We use a shared pointer to keep the result alive until the 
// thread is done.
ulong nthPrime = 0;

// Simulates work by searching for the nth prime number. Uses a
// naive algorithm and counts 2 as the first prime number.
IAsyncAction asyncAction = Windows.System.Threading.ThreadPool.RunAsync(
    (workItem) =&gt;
{
    uint  progress = 0; // For progress reporting.
    uint  primes = 0;   // Number of primes found so far.
    ulong i = 2;        // Number iterator.

    if ((n &gt;= 0) &amp;&amp; (n &lt;= 2))
    {
        nthPrime = n;
        return;
    }

    while (primes &lt; (n - 1))
    {
        if (workItem.Status == AsyncStatus.Canceled)
        {
            break;
        }

        // Go to the next number.
        i++;

        // Check for prime.
        bool prime = true;
        for (uint j = 2; j &lt; i; ++j)
        {
            if ((i % j) == 0)
            {
                prime = false;
                break;
            }
        };

        if (prime)
        {
            // Found another prime number.
            primes++;

            // Report progress at every 10 percent.
            uint temp = progress;
            progress = (uint)(10.0*primes/n);

            if (progress != temp)
            {
                String updateString;
                updateString = "Progress to " + n + "th prime: "
                    + (10 * progress) + "%\n";

                // Update the UI thread with the CoreDispatcher.
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(
                    CoreDispatcherPriority.High,
                    new DispatchedHandler(() =&gt;
                {
                    UpdateUI(updateString);
                }));
            }
        }
    }

    // Return the nth prime number.
    nthPrime = i;
});

// A reference to the work item is cached so that we can trigger a
// cancellation when the user presses the Cancel button.
m_workItem = asyncAction;
```

在调用 [**RunAsync**](https://msdn.microsoft.com/library/windows/apps/BR230593) 后，线程池将对工作项进行排队，并在线程可用时运行工作项。 线程池工作项异步运行，并且它们可以任何顺序运行，以便确保你的工作项独立运行。

请注意，该工作项会检查 [**IAsyncInfo.Status**](https://msdn.microsoft.com/library/windows/apps/BR206593) 属性，如果该工作项被取消，则退出。

## 处理工作项完成

通过设置工作项的 [**IAsyncAction.Completed**](https://msdn.microsoft.com/en-us/library/windows/apps/windows.foundation.iasyncaction.completed.aspx) 属性来提供完成处理程序。 提供委派（可使用 lambda 或 delegate 函数）来处理工作项的完成。 例如，使用 [**CoreDispatcher.RunAsync**](https://msdn.microsoft.com/library/windows/apps/Hh750317) 访问 UI 线程并显示结果。

以下示例使用在步骤 1 中所提交工作项的结果更新 UI：

> [!div class="tabbedCodeSnippets"]
``` cpp
asyncAction-&gt;Completed = ref new AsyncActionCompletedHandler(
    \[this, n, nthPrime](IAsyncAction^ asyncInfo, AsyncStatus asyncStatus)
{
    if (asyncStatus == AsyncStatus::Canceled)
    {
        return;
    }
    
    String^ updateString;
    updateString = "\n" + "The " + n + "th prime number is " 
        + (*nthPrime).ToString() + ".\n";

    // Update the UI thread with the CoreDispatcher.
    CoreApplication::MainView-&gt;CoreWindow-&gt;Dispatcher-&gt;RunAsync(
        CoreDispatcherPriority::High,
        ref new DispatchedHandler([this, updateString]()
    {
        UpdateUI(updateString);
    }));
});
```
``` csharp
asyncAction.Completed = new AsyncActionCompletedHandler(
    (IAsyncAction asyncInfo, AsyncStatus asyncStatus) =&gt;
{
    if (asyncStatus == AsyncStatus.Canceled)
    {
        return;
    }

    String updateString;
    updateString = "\n" + "The " + n + "th prime number is " 
        + nthPrime + ".\n";

    // Update the UI thread with the CoreDispatcher.
    CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(
        CoreDispatcherPriority.High,
        new DispatchedHandler(()=&gt;
    {
        UpdateUI(updateString);
    }));
});
```

请注意，完成处理程序在分派 UI 更新之前会检查工作项是否被取消。

## 摘要和后续步骤

可通过在为 Windows 8.1 编写的[创建 ThreadPool 工作项示例](http://go.microsoft.com/fwlink/p/?LinkID=328569)中的此快速入门下载代码并在 win_unap Windows 10 应用中重新使用源代码来了解详细信息。

## 相关主题

* [向线程池提交工作项](submit-a-work-item-to-the-thread-pool.md)
* [使用线程池的最佳实践](best-practices-for-using-the-thread-pool.md)
* [使用计时器提交工作项](use-a-timer-to-submit-a-work-item.md)
 



<!--HONumber=Mar16_HO1-->


