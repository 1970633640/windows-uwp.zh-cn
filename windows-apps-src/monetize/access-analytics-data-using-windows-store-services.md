---
author: mcleanbyron
ms.assetid: 4BF9EF21-E9F0-49DB-81E4-062D6E68C8B1
description: "使用 Windows 应用商店分析 API，针对已注册到你的或组织的 Windows 开发人员中心帐户的应用以编程方式检索分析数据。"
title: "使用 Windows 应用商店服务访问分析数据"
translationtype: Human Translation
ms.sourcegitcommit: 1a2e856cddf9998eeb8b0132c2fb79f5188c218b
ms.openlocfilehash: 596cc5054367acf0d3609a34b764bc7fcf33ea0b

---

# <a name="access-analytics-data-using-windows-store-services"></a>使用 Windows 应用商店服务访问分析数据

使用 *Windows 应用商店分析 API*，为注册到你的或组织的 Windows 开发人员中心帐户的应用以编程方式检索分析数据。 此 API 使你可以针对应用和加载项（也称为应用内产品或 IAP）购置、错误、应用评分和评价检索数据。 此 API 使用 Azure Active Directory (Azure AD) 验证来自应用或服务的调用。

以下步骤介绍端到端过程：

1.  确保已完成所有[先决条件](#prerequisites)。
2.  在 Windows 应用商店提交 API 中调用某个方法之前，请先[获取 Azure AD 访问令牌](#obtain-an-azure-ad-access-token)。 获取访问令牌后，可以在 60 分钟的令牌有效期内，使用该令牌调用 Windows 应用商店分析 API。 该令牌到期后，可以重新生成一个。
3.  [调用 Windows 应用商店分析 API](#call-the-windows-store-analytics-api)。

<span id="prerequisites" />
## <a name="step-1-complete-prerequisites-for-using-the-windows-store-analytics-api"></a>步骤 1：完成使用 Windows 应用商店分析 API 的先决条件

在开始编写调用 Windows 应用商店分析 API 的代码之前，确保已完成以下先决条件。

* 你（或你的组织）必须具有 Azure AD 目录，并且你必须具有该目录的[全局管理员](http://go.microsoft.com/fwlink/?LinkId=746654)权限。 如果你已使用 Office 365 或 Microsoft 的其他业务服务，表示你已经具有 Azure AD 目录。 否则，你可以免费[在开发人员中心中创建新的 Azure AD](https://msdn.microsoft.com/windows/uwp/publish/manage-account-users)。

* 你必须将 Azure AD 应用程序与你的开发人员中心帐户相关联、检索租户 ID 和应用程序的客户端 ID 并生成密钥。 Azure AD 应用程序是指你想要从中调用 Windows 应用商店分析 API 的应用或服务。 需要租户 ID、客户端 ID 和密钥，才可以获取将传递给 API 的 Azure AD 访问令牌。

  >**注意**&nbsp;&nbsp;只需执行一次此任务。 获取租户 ID、客户端 ID 和密钥后，当你需要创建新的 Azure AD 访问令牌时，可以随时重复使用它们。

若要将 Azure AD 应用程序与你的开发人员中心帐户相关联并检索所需值：

1.  在开发人员中心中，转到“帐户设置”、单击“管理用户”，然后将你的组织的开发人员中心帐户与你的组织的 Azure AD 目录相关联。 有关详细说明，请参阅[管理帐户用户](https://msdn.microsoft.com/windows/uwp/publish/manage-account-users)。

2.  在“管理用户”页面中，单击“添加 Azure AD 应用程序”、添加表示应用或服务并且将用于访问你的开发人员中心帐户的分析数据的 Azure AD 应用程序，然后为其分配“管理者”角色。 如果此应用程序已存在于你的 Azure AD 目录中，你可以在“添加 Azure AD 应用程序”页面上选择它，以将其添加到你的开发人员中心帐户。 如果没有此应用程序，你可以在“添加 Azure AD 应用程序”页面上创建新的 Azure AD 应用程序。 有关详细信息，请参阅[添加和管理 Azure AD 应用程序](https://msdn.microsoft.com/windows/uwp/publish/manage-account-users#add-and-manage-azure-ad-applications)。

3.  返回到“管理用户”页面、单击 Azure AD 应用程序的名称以转到应用程序设置，然后记下“租户 ID”和“客户端 ID”值。

4. 单击“添加新密钥”。 在接下来的屏幕上，记下“密钥”值。 在离开此页面后，你将无法再访问该信息。 有关详细信息，请参阅[添加和管理 Azure AD 应用程序](https://msdn.microsoft.com/windows/uwp/publish/manage-account-users#add-and-manage-azure-ad-applications)中有关管理密钥的信息。

<span id="obtain-an-azure-ad-access-token" />
## <a name="step-2-obtain-an-azure-ad-access-token"></a>步骤 2：获取 Azure AD 访问令牌

在 Windows 应用商店分析 API 中调用任何方法之前，首先必须获取将传递给该 API 中每个方法的 **Authorization** 标头的 Azure AD 访问令牌。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以对它进行刷新，以便可以在之后调用该 API 时继续使用。

若要获取访问令牌，请按照 [使用客户端凭据的服务到服务调用](https://azure.microsoft.com/documentation/articles/active-directory-protocols-oauth-service-to-service/) 中的说明将 HTTP POST 发送到 ```https://login.microsoftonline.com/<tenant_id>/oauth2/token``` 终结点。 示例请求如下所示。

```
POST https://login.microsoftonline.com/<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8

grant_type=client_credentials
&client_id=<your_client_id>
&client_secret=<your_client_secret>
&resource=https://manage.devcenter.microsoft.com
```

对于 POST URI 中的 *tenant\_id*、*client\_id* 和 *client\_secret* 参数，请为从上一部分的开发人员中心中检索到的应用程序指定租户 ID、客户端 ID 和密钥。 对于 *resource* 参数，必须指定 ```https://manage.devcenter.microsoft.com```。

在你的访问令牌到期后，可以按照[此处](https://azure.microsoft.com/documentation/articles/active-directory-protocols-oauth-code/#refreshing-the-access-tokens)的说明刷新令牌。

<span id="call-the-windows-store-analytics-api" />
## <a name="step-3-call-the-windows-store-analytics-api"></a>步骤 3：调用 Windows 应用商店分析 API

获取 Azure AD 访问令牌后，可以随时调用 Windows 应用商店分析 API。 有关每个方法的语法信息，请参阅以下文章。 必须将访问令牌传递到每个方法的 **Authorization** 标头。

* [获取应用购置](get-app-acquisitions.md)
* [获取加载项购置](get-in-app-acquisitions.md)
* [获取错误报告数据](get-error-reporting-data.md)
* [获取应用中的错误的详细信息](get-details-for-an-error-in-your-app.md)
* [获取应用中的错误的堆栈跟踪](get-the-stack-trace-for-an-error-in-your-app.md)
* [获取应用评分](get-app-ratings.md)
* [获取应用评价](get-app-reviews.md)
* [获取广告性能数据](get-ad-performance-data.md)
* [获取广告市场活动性能数据](get-ad-campaign-performance-data.md)

## <a name="code-example"></a>代码示例

以下代码示例演示了如何获取 Azure AD 访问令牌以及如何从 C# 控制台应用调用 Windows 应用商店分析 API。 若要使用此代码示例，请将 *tenantId*、*clientId*、*clientSecret* 和 *appID* 变量分配给你的方案的相应值。 此示例需要 Newtonsoft 中的 [Json.NET 程序包](http://www.newtonsoft.com/json)，以便反序列化 Windows 应用商店分析 API 返回的 JSON 数据。

> [!div class="tabbedCodeSnippets"]
[!code-cs[AnalyticsApi](./code/StoreServicesExamples_Analytics/cs/Program.cs#AnalyticsApiExample)]

## <a name="error-responses"></a>错误响应

Windows 应用商店分析 API 会在 JSON 对象中返回含有错误代码和消息的错误响应。 以下示例演示了由无效参数引起的错误响应。

```json
{
    "code":"BadRequest",
    "data":[],
    "details":[],
    "innererror":{
        "code":"InvalidQueryParameters",
        "data":[
            "top parameter cannot be more than 10000"
        ],
        "details":[],
        "message":"One or More Query Parameters has invalid values.",
        "source":"AnalyticsAPI"
    },
    "message":"The calling client sent a bad request to the service.",
    "source":"AnalyticsAPI"
}
```

## <a name="related-topics"></a>相关主题

* [获取应用购置](get-app-acquisitions.md)
* [获取加载项购置](get-in-app-acquisitions.md)
* [获取错误报告数据](get-error-reporting-data.md)
* [获取应用中的错误的详细信息](get-details-for-an-error-in-your-app.md)
* [获取应用中的错误的堆栈跟踪](get-the-stack-trace-for-an-error-in-your-app.md)
* [获取应用评分](get-app-ratings.md)
* [获取应用评价](get-app-reviews.md)
* [获取广告性能数据](get-ad-performance-data.md)
* [获取广告市场活动性能数据](get-ad-campaign-performance-data.md)
 



<!--HONumber=Dec16_HO4-->


