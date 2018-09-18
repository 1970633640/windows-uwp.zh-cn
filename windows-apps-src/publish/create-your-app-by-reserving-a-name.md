---
author: jnHs
Description: The first step in creating a new app in your Windows Dev Center dashboard is reserving an app name. See how to reserve app names and find suggestions for choosing a great name for your app.
title: 通过保留名称创建应用
keywords: Windows 10, uwp, 预留名称, 应用名称, 应用名, 名称, 产品名称, 命名, 保留名称, 标题, 名, 题目
ms.assetid: 6DC58A9A-DF47-4652-8D13-0AC9289F5950
ms.author: wdg-dev-content
ms.date: 8/07/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 83f2ab8a27810635b569d44961ff532ce3240e28
ms.sourcegitcommit: f5321b525034e2b3af202709e9b942ad5557e193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2018
ms.locfileid: "4017861"
---
# <a name="create-your-app-by-reserving-a-name"></a>通过保留名称创建应用

在[Windows 开发人员中心仪表板](https://partner.microsoft.com/dashboard)中创建新的应用的第一步保留应用名称。 每个保留名称（有时被称为应用的*标题*）在整个 Microsoft Store 中必须是唯一的。

即使你尚未开始构建应用，也可以为你的应用保留名称。 我们建议你尽早这样做，这样其他任何人都无法使用该名称。 请注意，你将需要在三个月内提交应用，以便为你保留该名称。

在[上载应用程序包](upload-app-packages.md)时，[**Package/Properties/DisplayName**](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-displayname) 值必须与为应用所保留的名称相匹配。 如果使用 Microsoft Visual Studio 创建应用程序包，则将为你填充此特性。

> [!IMPORTANT]
> 你可以保留其他名称的应用，并且你可以选择使用其中一个引擎在你的应用的已发布版本而不是保留当你首次在仪表板中创建你的应用的一个。 但是，请注意，将会在此处输入的名字用的一些你的应用[标识详细信息](view-app-identity-details.md)，如**程序包系列名称 (PFN)**。 这些值可能会给某些用户，且不能更改，因此请确保你保留该名称是适用于此用。


## <a name="create-your-app-by-reserving-a-new-name"></a>通过保留新名称创建应用

保留名称是在仪表板中创建应用的第一步。 

1.  在**概述**页面上，单击**创建新应用**。
2.  在文本框中，输入要使用的名称，然后选择**检查可用性**。 如果该名称可用，你将看到绿色复选标记。 （如果你输入的名称已经由另一个开发人员保留或使用，你将看到一条指示该名称不可用的消息。）
3.  单击**保留产品名称**。

现在已为你保留该名称，只要你准备就绪，就可以开始进行[提交](app-submissions.md)。 

> [!NOTE]
> 可能会发现自己无法保留某个名称，即使在 Microsoft Store 中并没有看到任何以该名称命名的应用也是如此。 这通常是因为其他开发人员已为其应用保留该名称，但尚未提交该应用。 如果你拥有某个名称的商标权或其他法律权利，但却无法保留该名称，或发现 Microsoft Store 中的其他应用在使用该名称，请[联系 Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=233777)。

在保留某个名称后，你有三个月的时间来提交应用。 如果在三个月内未提交该应用，保留的名称将过期，其他开发人员将可以使用该名称命名应用。 如果你尝试采用已任其过期的名称提交应用，则可能会遇到错误。

> [!NOTE]
> 如果有一个在早期版本的 Windows Phone 仪表板中创建的 Windows Phone 应用，并且从未为其保留名称，则你必须进行此操作以上载它的 .appx 程序包，或[查看应用标识详细信息](view-app-identity-details.md)（特定于 .appx 程序包）。 保留唯一名称还可以阻止其他任何用户私自保留该名称。 但是，如果未保留名称，也仍可以为你的 Windows Phone 8.x 客户管理和提交该应用。


## <a name="choosing-your-apps-name"></a>选择应用名称

为你的应用选择适当的名称非常重要。 你应该选取一个能够引起客户兴趣的名称，从而吸引他们进一步了解你的应用。 下面是有关选择良好应用名称的几点提示。

-   **保持简短。** 在很多情况下，用来显示应用名称的空间非常有限，因此我们建议尽可能使用最短的名称。 虽然你的应用的名称最多可包含 256 个字符，但客户可能无法始终看到非常长的名称的末尾。
    > [!NOTE]
    > 在各种位置显示的实际字符数目可能有所不同，具体取决于分配的长度和你的应用名称所使用的字符类型。 例如，在 Windows 使用的 Segoe UI 字体中，10 个“W”字符占用的空间大约相当于 30 个“I”字符。 因为此变化，请确保在提交你的应用之前测试你的应用，并验证它的名字在其磁贴（如果你选择覆盖应用名称）、搜索结果和应用本身内的显示方式。 另外，请考虑应用要采用的每种语言。 请记住，东亚字符往往比拉丁字符宽，因此将显示的字符会比拉丁字符少。
-   **保持独创性。** 确保使用与众不同的应用名称，这样不易与现有应用产生混淆。
-   **请勿使用其他人注册商标的名称。** 确保你有权使用你保留的名称。 如果其他人将该名称注册为商标，他们有权投诉侵权，你将无法继续使用该名称。 如果在你的应用发布后发生这种情况，我们会将其从应用商店中删除。 你将需要更改你的应用名称以及出现在应用及其内容中该名称的所有实例，然后才能再次[提交你的应用](app-submissions.md)进行认证。
-   **避免在名称末尾添加区别性信息。** 如果将用于区分多个应用的信息添加到名称末尾，则客户可能会忽略此信息，尤其是在名称很长的情况下；这样所有应用看上去似乎都采用了相同名称。 如果这不可避免，请使用不同的徽标和应用图像，这样会更容易区分应用。
-   **不要在名称中添加表情符号。** 你不能保留包含表情符号或其他不受支持的字符的名称。


## <a name="manage-additional-app-names"></a>管理其他应用名称

可以在 Windows 开发人员中心仪表板中在每个应用的**应用管理**部分的**管理应用名称**页面上添加和管理其他名称。

在某些情况下，可能希望保留用于同一应用的多个名称，例如要提供应用的多个语言版本并希望每个语言版本均使用不同的名称。 如果你要完全更改应用的名称，你将需要保留额外的名称。

在此页面上，你还可以删除你已保留但不想再使用的任何名称。

有关详细信息，请参阅[管理应用名称](manage-app-names.md)。

 

 




