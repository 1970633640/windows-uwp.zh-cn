---
author: mcleanbyron
description: "使用 Windows 应用商店提交 API 中的此方法获取应用提交的软件包推出信息。"
title: "使用 Windows 应用商店提交 API 获取应用提交的软件包推出信息"
ms.author: mcleans
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "windows 10, uwp, Windows 应用商店提交 API, 软件包推出, 应用提交"
ms.assetid: 9ada5ac3-a86e-4bb6-8ebc-915ba9649e3c
translationtype: Human Translation
ms.sourcegitcommit: 5645eee3dc2ef67b5263b08800b0f96eb8a0a7da
ms.openlocfilehash: ba9b48f2487016c4df7a14e0dc948dcf01952c99
ms.lasthandoff: 02/08/2017

---

# <a name="get-package-rollout-info-for-an-app-submission-using-the-windows-store-submission-api"></a>使用 Windows 应用商店提交 API 获取应用提交的软件包推出信息


使用 Windows 应用商店提交 API 中的此方法获取软件包外部测试版提交的[软件包推出](../publish/gradual-package-rollout.md)信息。 有关通过使用 Windows 应用商店提交 API 创建应用提交过程的详细信息，请参阅[管理应用提交](manage-app-submissions.md)。

## <a name="prerequisites"></a>先决条件

若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Windows 应用商店提交 API 的所有[先决条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。
* 使用你的开发人员中心帐户为应用创建提交。 可以使用开发人员中心仪表板执行此操作，也可以通过以下方式执行此操作：使用[创建应用提交](create-an-app-submission.md)方法。

>**注意**&nbsp;&nbsp;此方法只可以用于授予使用 Windows 应用商店提交 API 权限的 Windows 开发人员中心帐户。 并非所有帐户都已启用此权限。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求参数的使用示例和描述。

| 方法 | 请求 URI                                                      |
|--------|------------------------------------------------------------------|
| GET   | ```https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/packagerollout   ``` |

<span/>
 

### <a name="request-header"></a>请求头

| 标头        | 类型   | 说明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** &lt;*token*&gt;。 |

<span/>

### <a name="request-parameters"></a>请求参数

| 名称        | 类型   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| applicationId | 字符串 | 必需。 应用（包含要获取软件包推出信息的提交）的应用商店 ID。 有关应用商店 ID 的详细信息，请参阅[查看应用标识详细信息](https://msdn.microsoft.com/windows/uwp/publish/view-app-identity-details)。  |
| submissionId | 字符串 | 必需。 要获取软件包推出信息的提交的 ID。 可通过开发人员中心仪表板获取此 ID，它包含在[创建应用提交](create-an-app-submission.md)请求的响应数据中。  |

<span/>

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-example"></a>请求示例

以下示例演示了如何获取应用提交的软件包推出信息。

```
GET https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/submissions/1152921504621243649/packagerollout HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了对已启用逐步软件包推出的应用提交的此方法成功调用的 JSON 响应正文。 有关响应正文中这些值的更多详细信息，请参阅[软件包推出资源](manage-app-submissions.md#package-rollout-object)。

```json
{
    "isPackageRollout": true,
    "packageRolloutPercentage": 25,
    "packageRolloutStatus": "PackageRolloutInProgress",
    "fallbackSubmissionId": "1212922684621243058"
}
```

如果应用提交未启用逐步软件包推出，会返回以下响应正文。

```json
{
    "isPackageRollout": false,
    "packageRolloutPercentage": 0,
    "packageRolloutStatus": "PackageRolloutNotStarted",
    "fallbackSubmissionId": "0"
}
```

## <a name="error-codes"></a>错误代码

如果无法成功完成请求，该响应中会包含以下 HTTP 错误代码之一。

| 错误代码 |  描述   |
|--------|------------------|
| 404  | 找不到提交。 |
| 409  | 提交不属于指定的应用，或者应用使用的开发人员中心仪表板功能[当前不受 Windows 应用商店提交 API 支持](create-and-manage-submissions-using-windows-store-services.md#not_supported)。 |   

<span/>


## <a name="related-topics"></a>相关主题

* [逐步软件包推出](../publish/gradual-package-rollout.md)
* [使用 Windows 应用商店提交 API 管理应用提交](manage-app-submissions.md)
* [使用 Windows 应用商店服务创建和管理提交](create-and-manage-submissions-using-windows-store-services.md)

