---
title: "凭据保险箱"
description: "本文介绍了通用 Windows 平台 (UWP) 应用可如何使用凭据保险箱安全存储和检索用户凭据，并使用用户的 Microsoft 帐户在设备间漫游用户凭据。"
ms.assetid: 7BCC443D-9E8A-417C-B275-3105F5DED863
author: awkoren
translationtype: Human Translation
ms.sourcegitcommit: ba620bc89265cbe8756947e1531759103c3cafef
ms.openlocfilehash: 2d5e1fada82e0c39ad0dce31c779ac80005aff17

---

# 凭据保险箱


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


本文介绍了通用 Windows 平台 (UWP) 应用可如何使用凭据保险箱安全存储和检索用户凭据，并使用用户的 Microsoft 帐户在设备间漫游用户凭据。

例如，你有一个连接到服务以访问受保护资源（如媒体文件或社交网络）的应用。 你的服务需要每位用户的登录信息。 你已在应用中构建了 UI，此 UI 可获取每位用户的用户名和密码，然后使用这些信息使用户登录到服务中。 使用保险箱 API 可为用户存储用户名和密码，并在他们下次打开应用时轻松地检索它们并自动使用户登录（不论他们在什么设备上）。

对于域帐户来说，凭据保险箱的工作方式略有不同。 如果有凭据与 Microsoft 帐户一起存储，并且将该帐户与域帐户关联（如作时使用的帐户），凭据将漫游至该域帐户。 但是，任何在使用域帐户登录时添加的新凭据不会漫游。 这确保了该域的私有凭据不会暴露在域之外。

## 存储用户凭据


1.  使用来自 [**Windows.Security.Credentials**](https://msdn.microsoft.com/library/windows/apps/br227089) 命名空间的 [**PasswordVault**](https://msdn.microsoft.com/library/windows/apps/br227081) 对象获取对凭据保险箱的引用。
2.  创建包含你的应用的标识符、用户名和密码的 [**PasswordCredential**](https://msdn.microsoft.com/library/windows/apps/br227061) 对象，并将该对象传递至 [**PasswordVault.Add**](https://msdn.microsoft.com/library/windows/apps/hh701231) 方法以将凭据添加到保险箱。

```cs
var vault = new Windows.Security.Credentials.PasswordVault();
vault.Add(new Windows.Security.Credentials.PasswordCredential(
    "My App", username, password));
```

## 检索用户凭据


在你拥有对 [**PasswordVault**](https://msdn.microsoft.com/library/windows/apps/br227081) 对象的引用之后，你有多个选项从凭据保险箱检索用户凭据。

-   你可以使用 [**PasswordVault.RetrieveAll**](https://msdn.microsoft.com/library/windows/apps/br227088) 方法检索用户在保险箱中为你的应用提供的所有凭据。

-   如果你知道存储的凭据的用户名，你可以使用 [**PasswordVault.FindAllByUserName**](https://msdn.microsoft.com/library/windows/apps/br227084) 方法检索该用户名的所有凭据。

-   如果你知道存储的凭据的资源名，你可以使用 [**PasswordVault.FindAllByResource**](https://msdn.microsoft.com/library/windows/apps/br227083) 方法检索该资源名的所有凭据。

-   最后，如果你同时知道一个凭据的用户名和资源名，你可以使用 [**PasswordVault.Retrieve**](https://msdn.microsoft.com/library/windows/apps/br227087) 方法仅检索该凭据。

让我们来查看一个示例，在此示例中我们已在一个应用中全局存储了资源名，并且，如果找到了它们的凭据，我们将使用户自动登录。 如果我们找到了同一个用户的多个凭据，我们将要求用户选择一个默认凭据以在登录时使用。

```cs
private string resourceName = "My App";
private string defaultUserName;

private void Login()
{
    var loginCredential = GetCredentialFromLocker();

    if (loginCredential != null)
    {
        // There is a credential stored in the locker.
        // Populate the Password property of the credential
        // for automatic login.
        loginCredential.RetrievePassword();
    }
    else
    {
        // There is no credential stored in the locker.
        // Display UI to get user credentials.
        loginCredential = GetLoginCredentialUI();
    }

    // Log the user in.
    ServerLogin(loginCredential.UserName, loginCredential.Password);
}


private Windows.Security.Credentials.PasswordCredential GetCredentialFromLocker()
{
    Windows.Security.Credentials.PasswordCredential credential = null;

    var vault = new Windows.Security.Credentials.PasswordVault();
    var credentialList = vault.FindAllByResource(resourceName);
    if (credentialList.Count > 0)
    {
        if (credentialList.Count == 1)
        {
            credential = credentialList[0];
        }
        else
        {
            // When there are multiple usernames,
            // retrieve the default username. If one doesn't
            // exist, then display UI to have the user select
            // a default username.

            defaultUserName = GetDefaultUserNameUI();

            credential = vault.Retrieve(resourceName, defaultUserName);
        }
    }

    return credential;
}
```

## 删除用户凭据


在凭据保险箱中删除用户凭据是一个快捷的两步式过程。

1.  使用来自 [**Windows.Security.Credentials**](https://msdn.microsoft.com/library/windows/apps/br227089) 命名空间的 [**PasswordVault**](https://msdn.microsoft.com/library/windows/apps/br227081) 对象获取对凭据保险箱的引用。

2.  将希望删除的凭据传递至 [**PasswordVault.Remove**](https://msdn.microsoft.com/library/windows/apps/hh701242) 方法。

```cs
var vault = new Windows.Security.Credentials.PasswordVault();
vault.Remove(new Windows.Security.Credentials.PasswordCredential(
    "My App", username, password));
```

## 最佳做法


将凭据保险箱仅用于存储密码，而不要将其用于存储较大的数据 blob。

仅当满足以下条件时才将密码保存在凭据保险箱中：

-   用户已成功登录。
-   用户已选择保存密码。

永远不要使用应用数据或漫游设置在纯文本中存储凭据。


<!--HONumber=Aug16_HO3-->


