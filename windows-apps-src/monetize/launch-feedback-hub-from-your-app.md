---
author: mcleanbyron
Description: "你可以通过从应用启动“反馈中心”来鼓励客户留下反馈。"
title: "从应用启动“反馈中心”"
ms.assetid: 070B9CA4-6D70-4116-9B18-FBF246716EF0
translationtype: Human Translation
ms.sourcegitcommit: de85956c7c1d2a0ba509d61ee8928b412f057f8a
ms.openlocfilehash: ccda01d9bfa4ffdff2bbce5d6c60c78e026270e5

---

# 从应用启动“反馈中心”

你可以通过将用于启动“反馈中心”的控件（如按钮）添加到通用 Windows 平台 (UWP) 应用来鼓励客户留下反馈。 “反馈中心”是预安装的应用，该应用提供了一个用于收集有关 Windows 和已安装应用的反馈的位置。 将收集通过“反馈中心”针对应用提交的所有客户反馈，并在 Windows 开发人员中心仪表板中的[反馈报告](../publish/feedback-report.md)中向你呈现，以便你可以在单个报告看到客户已提交的问题、建议和投票。

>**注意** **反馈**报告当前仅向已加入[开发人员中心预览体验计划](../publish/dev-center-insider-program.md)的开发者帐户提供。 

若要从应用启动“反馈中心”，请使用 [Microsoft 官方商城协议和盈利 SDK](http://aka.ms/store-em-sdk) 所提供的 API。 我们建议你使用此 API 从遵循我们的设计指南的应用中的 UI 元素启动“反馈中心”。

>**注意**“反馈中心”仅在运行 Windows 10 版本 10.0.14271 或更高版本的设备上可用。 我们建议你仅当“反馈中心”在用户设备上可用时才在应用中显示反馈控件。 本主题中的代码演示如何执行此操作。

## 如何从应用启动“反馈中心”

若要从应用启动“反馈中心”，请执行以下操作：

1. 安装 [Microsoft 官方商城协议和盈利 SDK](http://aka.ms/store-em-sdk)。 除了用于启动“反馈中心”的 API 外，此 SDK 还提供用于其他功能的 API，例如通过 A/B 测试运行实验和显示广告。 有关此 SDK 的详细信息，请参阅[通过官方商城协议和盈利 SDK 来获取应用收益并吸引客户](monetize-your-app-with-the-microsoft-store-engagement-and-monetization-sdk.md)。
2. 在 Visual Studio 中打开你的项目。
3. 在“解决方案资源管理器”中，右键单击你的项目的“引用”****节点，然后单击“添加引用”****。
4. 在“引用管理器”****中，展开“通用 Windows”****并单击“扩展”****。
5. 在 SDK 列表中，单击“Microsoft 官方商城协议 SDK”****旁边的复选框，并单击“确定”****。
6. 在项目中，添加要向用户显示的用于启动“反馈中心”的控件，如按钮。 我们建议你按如下方式配置该控件：
  * 将控件中显示的内容的字体设置为 **Segoe MDL2 Assets**。
  * 将控件中的文本设置为十六进制的 Unicode 字符代码 E939。 这是 **Segoe MDL2 Assets** 字体中推荐的反馈图标的字符代码。
  * 将控件的可见性设置为隐藏。

    > **注意**“反馈中心”仅在运行 Windows 10 版本 10.0.14271 或更高版本的设备上可用。 我们建议你默认隐藏反馈控件，并且仅当“反馈中心”在用户设备上可用时才在初始化代码中显示它。 下一步演示如何执行此操作。

  以下代码演示按上述方式配置的 [Button](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.button.aspx) 的 XAML 定义。
  ```xml
  <Button x:Name="feedbackButton" FontFamily="Segoe MDL2 Assets" Content="&#xE939;" HorizontalAlignment="Left" Margin="138,352,0,0" VerticalAlignment="Top" Visibility="Collapsed"  Click="feedbackButton_Click"/>
  ```
7. 在承载反馈控件的应用页面的初始化代码中，使用 [Feedback](https://msdn.microsoft.com/library/windows/apps/microsoft.services.store.engagement.feedback.aspx) 类的 [IsSupported](https://msdn.microsoft.com/library/windows/apps/microsoft.services.store.engagement.feedback.issupported.aspx) 属性来确定“反馈中心”是否在用户设备上可用。 如果此属性返回 **true**，则使该控件可见。 以下代码演示如何为 [Button](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.button.aspx) 执行此操作。
```CSharp
if (Microsoft.Services.Store.Engagement.Feedback.IsSupported)
{
        this.feedbackButton.Visibility = Visibility.Visible;
}
```
8. 在用户单击控件时运行的事件处理程序中，调用 [Feedback](https://msdn.microsoft.com/library/windows/apps/microsoft.services.store.engagement.feedback.aspx) 类的静态 [LaunchFeedbackAsync](https://msdn.microsoft.com/library/windows/apps/microsoft.services.store.engagement.feedback.launchfeedbackasync.aspx) 方法来启动“反馈中心”应用。 此方法有两个重载：一个不带有参数，另一个接受包含要与反馈相关联的元数据的键值对字典。 以下示例演示如何在 [Button](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.button.aspx) 的 [Click](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.primitives.buttonbase.click.aspx) 事件处理程序中启动“反馈应用”。
```CSharp
private async void feedbackButton_Click(object sender, RoutedEventArgs e)
{
        await Microsoft.Services.Store.Engagement.Feedback.LaunchFeedbackAsync();
}
```

## 反馈 UI 的设计建议

若要启动“反馈中心”，我们建议在应用中添加 UI 元素（如按钮），用于从 Segoe MDL2 Assets 字体和字符代码 E939 显示以下标准反馈图标。

![]Feedback icon](images/feedback_icon.PNG)

我们还建议你在应用中使用以下一个或多个链接到“反馈中心”的放置选项。
* **直接在应用栏中**。 根据你的实现，你可能希望仅使用图标或添加文本（如下所示）。

  ![]Feedback icon](images/feedback_appbar_placement.png)

* **在应用的“设置”中**。 这是提供对“反馈中心”的访问的更巧妙的方法。 在以下示例中，“反馈”链接显示为“应用”下的链接之一。

  ![]Feedback icon](images/feedback_settings_placement.png)

* **在事件驱动的浮出控件中**。 如果你要在启动到 Windows 反馈中心前向客户询问某个特定问题，这将非常有用。 例如，在你的应用使用某个功能后，你可能会就用户对该功能的满意度向客户提出特定问题。 如果用户选择回应，你的应用将启动“反馈中心”。


## 相关主题

* [反馈报告](../publish/feedback-report.md)



<!--HONumber=Jun16_HO4-->


