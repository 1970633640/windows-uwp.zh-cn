---
author: jnHs
Description: View the names that you've reserved for your app, reserve additional names (for other languages or to change your app's name), and delete reserved names that you don't need anymore.
title: 管理应用名称
ms.assetid: D95A6227-746E-4729-AE55-648A7102401C
ms.author: wdg-dev-content
ms.date: 10/02/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp，应用名，更改应用名称、 更新应用名称、 游戏的名称、 产品名称
ms.localizationpriority: medium
ms.openlocfilehash: 878b105541691834dbbe35b5210f33045afdc47b
ms.sourcegitcommit: c4d3115348c8b54fcc92aae8e18fdabc3deb301d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2018
ms.locfileid: "5409181"
---
# <a name="manage-app-names"></a>管理应用名称

**管理应用名称**允许你查看你已为你的应用，保留的名称的所有保留其他名称 （用于其他语言或更改你的应用的名称），并删除不需要的名称。 通过展开左侧的导航菜单中的任何你的应用中的**应用管理**部分，你可以在[Windows 开发人员中心仪表板](https://partner.microsoft.com/dashboard)中找到此页面。

> [!IMPORTANT]
> 你可以保留其他名称的应用，并且你可以选择使用其中一个引擎在你的应用的已发布版本而不是你首次在仪表板中创建你的应用时所保留的一个。 但是，请注意，将会在保留你的产品名字用的一些你的 it 的[标识详细信息](view-app-identity-details.md)，如**程序包系列名称 (PFN)**。 这些值可能会给某些用户，且不能更改，因此请确保在首次保留的名称是适用于此用。


## <a name="reserve-additional-names-for-your-app"></a>为你的应用保留其他名称

可以保留多个应用名称以用于同一应用。 如果你以多种语言提供应用，而且要为不同的语言使用不同的名称，则该选项特别有用。 如下所述，还可以以更改应用的名称保留新名称。

以保留一个新的应用名称、 找到**管理应用名称**页的**保留更多名称**部分中的文本框。 输入想要保留的名称，然后单击“检查可用性”****。 如果该名称可用，请单击**保留产品名称**。 如果需要，可以通过重复上述步骤中，保留多个应用名称。

> [!NOTE]
> 有关保留应用名称的详细信息，以及为何某个名称可能不可用，请参阅[通过保留名称创建你的应用](create-your-app-by-reserving-a-name.md)。


## <a name="delete-app-names"></a>删除应用名称

如果你不再希望使用以前保留的名称，则可以通过在此处删除来释放它。 在执行此操作之前，请确保你确定要执行此操作，因为这意味着该名称将立即变为可供别人保留和使用的名称。

若要删除应用的保留名称之一，请找到你不再希望使用的名称，然后单击“删除”****。 在确认对话框中，再次单击“删除”**** 以确认。

请注意，你的应用必须具有至少一个保留的名称。 若要完全从仪表板中，删除应用 （和释放已为该应用保留的所有名称），单击从**应用概述**页面的**删除此应用**。 如果该应用有正在进行的提交，需要先删除该提交。 请注意，是否你已发布到应用商店应用，你无法删除它从你的仪表板 （但你可以使用你的**概述**页面上**显示/隐藏产品**功能来隐藏该）。 


## <a name="rename-an-app-that-has-already-been-published"></a>重命名已发布的应用

如果应用已经在应用商店中，并且希望重命名该应用，则可以为它保留一个新名称（按照上述步骤操作），然后为该应用创建新提交即可。 

你必须更新你的应用的程序包替换为新的旧名称并将更新的程序包上载到你的提交。
- 首先，更新 Package.StoreAssociation.xml 文件以使用新名称，手动或使用 Visual Studio (**项目 > 应用商店 > 将应用与应用商店...关联**)。有关详细信息，请参阅[使用 Visual Studio 的 UWP 应用包](../packaging/packaging-uwp-apps.md)。
- 还需要更新应用部件清单中的 [**Package/Properties/DisplayName**](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-displayname) 元素，以及更新包括应用名称的任何图形或文本。 
  > [!IMPORTANT]
  > 更改应用部件清单中的 **Package/Properties/DisplayName** 之前，请确保更新 Package.StoreAssociation.xml 文件，否则会出现错误。

若要更新应用商店一览，以便它使用新名称，请转到[应用商店一览页面](create-app-store-listings.md)为该语言，并从**产品名称**下拉列表中选择的名称。 请务必查看你的说明和任何提及的名称的清单的其他部分，并根据需要进行更新。

> [!NOTE]
> 如果你的应用具有多个语言包和/或应用商店一览，你将需要更新的程序包和/或应用商店一览每种语言名称需要进行更新。

你的应用已发布后的新名称，你可以删除你不再需要使用任何较旧名称。

> [!TIP]
> 使用第一个名称为它保留在仪表板中将显示每个应用。 如果你已遵循以上步骤以重命名的应用，并且你想要使用的新名称在仪表板中显示，你必须删除的原始名称 （通过**管理应用名称**页上，单击**删除**）。 

 

 




