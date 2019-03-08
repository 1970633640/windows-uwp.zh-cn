---
description: 在 Microsoft Store 分析 API 中使用此方法，以下载您的 Xbox One 游戏中的错误的 CAB 文件。
title: 下载 Xbox One 游戏内错误的 CAB 文件
ms.date: 11/06/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 分析 API, 下载 CAB
ms.localizationpriority: medium
ms.openlocfilehash: 736219533a254e6380c10600e97f707f15e37de6
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57604322"
---
# <a name="download-the-cab-file-for-an-error-in-your-xbox-one-game"></a>下载 Xbox One 游戏内错误的 CAB 文件

在 Microsoft Store 分析 API 中使用此方法，若要下载与已引入通过 Xbox 开发人员门户 (XDP) 在 Xbox One 游戏中的特定错误相关联，在 XDP 分析合作伙伴中心仪表板中提供的 CAB 文件。 此方法只能下载在过去 30 天内发生的错误的 CAB 文件。

可以使用此方法之前，必须先使用[获取游戏中你的 Xbox One 的错误的详细信息](get-details-for-an-error-in-your-xbox-one-game.md)方法来检索你想要下载的 CAB 文件的 ID。

## <a name="prerequisites"></a>必备条件


若要使用此方法，首先需要执行以下操作：

* 完成 Microsoft Store 分析 API 的所有[先决条件](access-analytics-data-using-windows-store-services.md#prerequisites)（如果尚未这样做）。
* [获取 Azure AD 访问令牌](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。
* 获取想要下载的 CAB 文件的 ID。 若要获取此 ID，请使用[获取游戏中你的 Xbox One 的错误的详细信息](get-details-for-an-error-in-your-xbox-one-game.md)方法来检索在应用中，特定错误的详细信息，并使用**cabId**该方法的响应正文中的值。

## <a name="request"></a>请求


### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/cabdownload``` |


### <a name="request-header"></a>请求头

| 标头        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** *token*&lt;&gt;。 |


### <a name="request-parameters"></a>请求参数

| 参数        | 在任务栏的搜索框中键入   |  描述      |  必需  |
|---------------|--------|---------------|------|
| applicationId | 字符串 | Xbox One 下载 CAB 文件的游戏的产品 ID。 若要获取你的游戏的产品 ID，请导航到 Xbox 开发人员门户 (XDP) 中你的游戏，并从 URL 中检索产品 ID。 或者，如果从 Windows 合作伙伴中心的分析报告下载运行状况数据，请在.tsv 文件中包括的产品 ID。 |  是  |
| cabId | 字符串 | 想要下载的 CAB 文件的唯一 ID。 若要获取此 ID，请使用[获取游戏中你的 Xbox One 的错误的详细信息](get-details-for-an-error-in-your-xbox-one-game.md)方法来检索在应用中，特定错误的详细信息，并使用**cabId**该方法的响应正文中的值。 |  是  |

 
### <a name="request-example"></a>请求示例

以下示例演示如何使用此方法下载 CAB 文件。 将 *applicationId* 和 *cabId* 值替换为你的应用的相应值。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/cabdownload?applicationId=BRRT4NJ9B3D1&cabId=1336373323853 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

此方法将会返回一个 302（重定向）响应代码，并且会将响应中的 **Location** 标头分配给 CAB 文件的共享访问签名 (SAS) URI。 调用程序将被重定向至此 URI 以自动下载 CAB 文件。

## <a name="related-topics"></a>相关主题

* [使用 Microsoft Store 服务的访问分析数据](access-analytics-data-using-windows-store-services.md)
* [获取错误报告数据为你的 Xbox One 游戏](get-error-reporting-data-for-your-xbox-one-game.md)
* [获取游戏中你的 Xbox One 的错误的详细信息](get-details-for-an-error-in-your-xbox-one-game.md)
* [获取游戏中你的 Xbox One 的错误的堆栈跟踪](get-the-stack-trace-for-an-error-in-your-xbox-one-game.md)
