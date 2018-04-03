---
author: jnHs
Description: You can add users, groups, and Azure AD applications to your Dev Center account.
title: 向开发人员中心帐户添加用户、组和 Azure AD 应用程序
ms.author: wdg-dev-content
ms.date: 09/20/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp
ms.localizationpriority: high
ms.openlocfilehash: bf640dbfe642401b9a4f9c767b8c2145fed11d57
ms.sourcegitcommit: 11edca90aaf7856c762e68903483079d30ad3877
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="add-users-groups-and-azure-ad-applications-to-your-dev-center-account"></a>向开发人员中心帐户添加用户、组和 Azure AD 应用程序

你可以通过开发人员中心的[用户](manage-account-users.md)部分使用 Azure Active Directory 向你的开发人员中心帐户添加用户。 为每个用户分配一个角色（或自定义权限集），并且该角色定义他们的帐户访问权限。 你还可以添加[用户组](#groups)和 [Azure AD 应用程序](#azure-ad-applications)，以授予他们对你的开发人员中心帐户的访问权限。

将用户添加到帐户后，你可以[编辑帐户详细信息](#edit)、更改[角色和权限](set-custom-permissions-for-account-users.md)或[删除用户](#remove)。

> [!IMPORTANT]
> 若要向你的帐户添加用户，必须先[将你的开发人员中心帐户与你的组织的 Azure Active Directory 租户相关联](associate-azure-ad-with-dev-center.md)。 

在添加用户时，你将需要通过向其分配[角色或自定义权限集](set-custom-permissions-for-account-users.md)来指定他们对开发人员中心帐户的访问权限。请记住以下注意事项。 （这些适用于组和 Azure AD 应用程序以及各个用户。）

请注意，所有开发人员中心用户均须在[与开发人员中心帐户关联的 Azure AD 租户](associate-azure-ad-with-dev-center.md)中有一个活动帐户。 您可以在一个租户中一次性完成用户管理工作；但你必须使用你想要在其中添加或编辑用户的租户的管理员帐户登录。 在开发人员中心创建新用户后，也会在你登录的 Azure AD 租户中为该用户创建一个帐户，同样，对开发人员中心中的用户名称进行更改，你组织的 Azure AD 租户中也会出现相同更改。

> [!NOTE]
> 如果你的组织使用[目录集成](http://go.microsoft.com/fwlink/p/?LinkID=724033)在 Azure AD 中同步本地目录服务，你将无法在开发人员中心中创建新的用户、组或 Azure AD 应用程序。 你（或你的本地目录中的其他管理员）必须先在本地目录中直接创建它们，然后才能在开发人员中心中查看和添加它们。


<span id="users" />
## <a name="add-users-to-your-dev-center-account"></a>向你的开发人员中心帐户添加用户

若要向你的开发人员中心帐户添加用户，请转到**帐户设置**中的**用户**页，然后选择**添加用户**。 你必须使用你想要在其中工作的 Azure AD 租户的管理员帐户登录。 

### <a name="add-existing-users"></a>添加现有用户 

你可以选择你组织的租户内的现有用户，并授权他们访问你的开发人员中心帐户。 

<span id="from-directory" />
1.  从**用户**页面，选择**添加用户**。 
2.  从出现的列表中选择一个或多个用户。 你可以使用搜索框来搜索特定用户。
    > [!TIP]
    > 如果你选择将多个用户添加到你的开发人员中心帐户中，则必须为其分配相同角色或自定义权限集。 若要添加具有不同角色/权限的多个用户，请针对每个角色或自定义权限集重复以下步骤。

3.  当你完成选择用户时，请单击**添加选定项**。
4.  在**角色**部分中，为选定的用户指定[角色或自定义权限](set-custom-permissions-for-account-users.md)。
5.  单击**保存**。
如果你的帐户具有[全局管理员权限](http://go.microsoft.com/fwlink/p/?LinkId=746654)，你将看到其他一些用户添加方法。

### <a name="additional-methods-for-adding-users"></a>其他用户添加方法

如果你登录所用的管理员帐户对你使用的 Azure AD 租户还具有[全局管理员](http://go.microsoft.com/fwlink/?LinkId=746654)权限，那么在向开发人员中心帐户添加用户时你将有更多选项。 你需要选择其中一个选项：

-   **添加现有用户**：选择已你组织目录中的现有用户，并授权他们访问你的开发人员中心帐户，如上所述。
-   **创建新用户**：创建要添加到你的组织目录和开发人员中心帐户的全新用户帐户。
-   **邀请外部用户**：向当前不在你的组织目录中的用户发送电子邮件邀请。 他们将受邀访问你的开发人员中心帐户，并且会在你的 Azure AD 租户中为其创建新的[来宾用户](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)帐户。

<span id="new-user" />
### <a name="create-new-users"></a>创建新用户

> [!IMPORTANT]
> 你必须使用 Azure AD 租户中的全局管理员帐户登录才能创建新用户。

1.  从**用户**页面，单击**添加用户**，然后选择**创建新用户**。
2.  输入新用户的名字、姓氏和用户名。
3.  如果希望新用户在组织目录中拥有[全局管理员帐户](http://go.microsoft.com/fwlink/p/?LinkId=746654)，请选中标有**使此用户成为 Azure AD 中的全局管理员，并且全权管理所有目录资源**的框。 这可使该用户完整访问公司 Azure AD 中的所有管理功能。 他们能够在组织目录中添加和管理用户（但在开发人员中心中不行，除非授予帐户相应的[角色/权限](set-custom-permissions-for-account-users.md)）。 如果选中此框，需要为用户提供**密码恢复电子邮件**。
4.  如果你选中了**使此用户成为 Azure AD 中的全局管理员**框，请输入用户在需要恢复密码时可以使用的电子邮件。
5.  在**组成员身份**部分中，选择任何希望新用户加入的组。
6.  在**角色**部分中，为用户指定[角色或自定义权限](set-custom-permissions-for-account-users.md)。
7.  单击**保存**。
8.  在确认页上，你将看到新用户的登录信息，包括临时密码。 请确保记下此信息，并将其提供给新用户，因为在离开此页面后可能无法访问临时密码。


<span id="email" />
### <a name="invite-outside-users"></a>邀请外部用户

> [!IMPORTANT]
> 你必须使用 Azure AD 租户中的全局管理员帐户登录才能邀请外部用户。

1.  输入一个或多个电子邮件地址（最多十个），用逗号或分号隔开。
2.  在**角色**部分中，为用户指定[角色或自定义权限](set-custom-permissions-for-account-users.md)。
3.  单击**保存**。

你邀请的用户将获得加入你帐户的电子邮件邀请，并且会在你的 Azure AD 租户中为其创建新的[来宾用户](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)帐户。 每个用户需要接受邀请才能访问帐户。

如果需要重新发送邀请，请在**用户**页上查找用户，然后选择他们的电子邮件地址（或者显示**邀请挂起**的文本）。 然后在页面底部单击**重新发送邀请**。


### <a name="changing-a-users-directory-password"></a>更改用户的目录密码

如果在创建用户帐户时已经提供了**密码恢复电子邮件**，那么用户可以在有需要时自行更改密码。 你还可以按照以下步骤更新用户密码（如果你使用 Azure AD 租户中的全局管理员帐户登录以更改用户密码）。 请注意，此操作将更改用户在 Azure AD 租户中的密码以及他们用于访问开发人员中心的密码。 

1.  从**用户**页面，单击你希望编辑的用户帐户的名称。
2.  请单击页面底部的**重置密码**按钮。
3.  将显示一个确认页，用于显示用户的登录信息，包括临时密码。

    > [!IMPORTANT]
    >  务必打印或复制此信息，并将其提供给用户，因为你可能在离开此页面后无法访问临时密码。

<span id="groups" />
## <a name="add-groups-to-your-dev-center-account"></a>向你的开发人员中心帐户添加组

你可以将某个组从组织的目录添加到你的开发人员中心帐户。 当你执行此操作时，属于该组成员的每个用户都将能够访问它，并且具有与组的分配角色关联的权限。

### <a name="add-groups-from-your-organizations-directory"></a>从组织的目录添加组

1.  从**用户**页面，单击**添加组**。
2.  从出现的列表中选择一个或多个组。 你可以使用搜索框来搜索特定组。
    > [!TIP]
    > 如果你选择将多个组添加到你的开发人员中心帐户中，则必须为其分配相同角色或自定义权限集。 若要添加具有不同角色/权限的多个组，请针对每个角色或自定义权限集重复以下步骤。

3.  完成选择组后，请单击**添加选定项**。
4.  在**角色**部分中，为选定的组指定[角色或自定义权限](set-custom-permissions-for-account-users.md)。 组中的所有成员将都能够使用你应用于组的权限访问开发人员中心帐户，不必考虑与他们的个人帐户关联的角色/权限。
5.  单击**保存**。


### <a name="create-a-new-group-account-in-your-organizations-directory-and-add-it-to-your-dev-center-account"></a>在你的组织目录中创建新组帐户并将其添加到开发人员中心帐户中

如果你希望将开发人员中心访问权限授予全新的组，你可以在**用户**部分中创建新组。 请注意，将在组织的目录中创建新组，而不只是在你的开发人员中心帐户中创建。

1.  从**用户**页面，单击**添加组**。
2.  在下一页上，请单击**新组**。
3.  输入新组的显示名称。
4.  为组指定[角色或自定义权限](set-custom-permissions-for-account-users.md)。 组中的所有成员将都能够使用你应用于组的权限访问开发人员中心帐户，不必考虑与他们的个人帐户关联的角色/权限。
5.  从出现的列表中选择要分配给新组的用户。 你可以使用搜索框来搜索特定用户。
6.  完成选择用户后，请单击**添加选定项**将其添加到新组中。
7.  单击**保存**。


<span id="azure-ad-applications" />
## <a name="add-azure-ad-applications-to-your-dev-center-account"></a>向开发人员中心帐户添加 Azure AD 应用程序

你可以允许作为你组织 Azure AD 组成部分的应用程序或服务访问你的开发人员中心帐户。

### <a name="add-azure-ad-applications-from-your-organizations-directory"></a>从组织的目录中添加 Azure AD 应用程序

1.  从**用户**页面，选择**添加 Azure AD 应用程序**。
2.  从出现的列表中选择一个或多个 Azure AD 应用程序。 你可以使用搜索框来搜索特定的 Azure AD 应用程序。
    > [!TIP]
    > 如果你选择将多个 Azure AD 应用程序添加到你的开发人员中心帐户中，则必须为其分配相同角色或自定义权限集。 若要添加具有不同角色/权限的多个 Azure AD 应用程序，请针对每个角色或自定义权限集重复以下步骤。

3.  完成选择 Azure AD 应用程序后，请单击**添加选定项**。
4.  在**角色**部分中，为选定的 Azure AD 应用程序指定[角色或自定义权限](set-custom-permissions-for-account-users.md)。
5.  单击**保存**。


### <a name="create-a-new-azure-ad-application-account-in-your-organizations-directory-and-add-it-to-your-dev-center-account"></a>在你的组织目录中创建新 Azure AD 应用程序帐户并将其添加到开发人员中心帐户中

如果你希望将开发人员中心访问权限授予给全新的 Azure AD 应用程序帐户，你可以在**用户**部分中创建一个帐户。 请注意，这将在组织的目录中创建新的帐户，而不只是在你的开发人员中心帐户中创建。

> [!TIP]
> 如果你主要使用此 Azure AD 应用程序进行开发人员中心身份验证，并且不需要用户直接访问它，可以为**回复 URL** 和**应用 ID URI** 输入任何有效地址，只要这些值未由目录中的任何其他 Azure AD 应用程序使用。

1.  从**用户**页面，选择**添加 Azure AD 应用程序**。
2.  在下一页上，单击**新的 Azure AD 应用程序**。
3.  输入新的 Azure AD 应用程序的**回复 URL**。 这是用户可以登录并使用 Azure AD 应用程序的 URL（有时也称为“应用 URL”或“登录 URL”）。 **回复 URL** 的长度不得超过 256 个字符。
4.  输入新的 Azure AD 应用程序的**应用 ID URI**。 这是 Azure AD 应用程序在向 Azure AD 发送单一登录请求时所显示的逻辑标识符。 请注意，每个 Azure AD 应用程序的**应用 ID URI** 在目录中必须唯一，且长度不得超过 256 个字符。
5.  在**角色**部分中，为 Azure AD 应用程序指定[角色或自定义权限](set-custom-permissions-for-account-users.md)。
6.  单击**保存**。

添加或创建 Azure AD 应用程序后，可以返回到**用户**部分，然后选择应用程序名称查看应用程序的设置，包括租户 ID、客户端 ID、回复 URL 和应用 ID URI。

> [!NOTE]
> 如果要使用 [Microsoft Store 服务](../monetize/using-windows-store-services.md)提供的 REST API，将需要此页面上显示的租户 ID 和客户端 ID 值，以获取可用于对服务调用进行身份验证的 Azure AD 访问令牌。   

<span id="manage-keys" />
### <a name="manage-keys-for-an-azure-ad-application"></a>管理 Azure AD 应用程序的密钥

如果 Azure AD 应用程序在 Microsoft Azure AD 中读写数据，它将需要密钥。 可以通过在开发人员中心中编辑 Azure AD 应用程序的信息来为其创建密钥。 还可以删除不再需要的密钥。

1.  从**用户**页面，单击 Azure AD 应用程序的名称。
    > [!TIP]
    > 在你单击 Azure AD 应用程序的名称时，你将看到该 Azure AD 应用程序的所有有效密钥（其中包括密钥的创建日期以及其过期日期）。 若要删除不再需要的密钥，请单击“删除”****。

2.  若要添加新密钥，请单击**添加新密钥**。
3.  你将看到一个显示“客户端 ID”****和“密钥”****值的屏幕。
    > [!IMPORTANT]
    > 务必打印或复制此信息，因为你可能在离开此页面后无法再访问该信息。

4.  如果要创建更多密钥，请单击**添加其他密钥**。

<span id="edit" />
## <a name="edit-a-user-group-or-azure-ad-application"></a>编辑用户、组或 Azure AD 应用程序

将用户、组和/或 Azure AD 应用程序添加到你的开发人员中心帐户后，可以更改其帐户信息。 

> [!IMPORTANT]
> 对[角色或权限](set-custom-permissions-for-account-users.md)所做的更改将仅影响开发人员中心访问权限。 所有其他更改（例如更改用户的名称或组成员身份或 Azure AD 应用程序的回复 URL 和应用 ID URI）将反映在你的组织的 Azure AD 租户以及开发人员中心帐户中。 

1.  从**用户**页面，单击你希望编辑的用户、组或 Azure AD 应用程序帐户的名称。
2.  进行所需更改。 你可以编辑的项目如下所示：
    -   对于**用户**，你可以编辑用户的名字、姓氏或用户名。 你还可以在**组成员身份**部分中选择或取消选择组，以更新其组成员身份。
    -   对于**组**，你可以编辑组的名称。 （若要更新组成员身份，请编辑要添加或从组中删除的用户，并对**组成员身份**部分进行更改。）
    -   对于 **Azure AD 应用程序**，你可以输入**回复 URL** 或**应用 ID URI** 的新值。
    请记住，这些更改将在组织的目录以及你的开发人员中心帐户中进行。
3.  对于和开发人员中心访问权限有关的更改，请选择或取消选择要应用的角色，或选择**自定义权限**并进行所需更改。 这些更改仅影响开发人员中心访问权限，并且不会更改你的组织的 Azure AD 租户中的任何权限。
3.  单击**保存**。


## <a name="view-history-for-account-users"></a>查看帐户用户的历史记录

作为帐户所有者，你可以查看已添加到帐户中的任何其他用户的详细浏览历史记录。

在**用户**页面上，单击要查看其浏览历史记录的用户的**上次活动**下显示的链接。 你可以查看此用户在过去 30 天内访问过的所有网页的 URL。

<span id="remove" />
## <a name="remove-users-groups-and-azure-ad-applications"></a>删除用户、组和 Azure AD 应用程序

若要从开发人员中心帐户删除用户、组或 Azure AD 应用程序，请在**用户**页上单击按其名称显示的**删除**链接。 在确认你希望删除它后，该用户、组或 Azure AD 应用程序将无法再访问你的开发人员中心帐户（除非你以后再次添加它）。

> [!IMPORTANT] 
> 删除用户、组或 Azure AD 应用程序意味着它将无法再访问你的开发人员中心帐户。 它**不会**从你的组织的目录中删除用户、组或 Azure AD 应用程序。

 

