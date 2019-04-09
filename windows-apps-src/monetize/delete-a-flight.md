---
ms.assetid: AD80F9B3-CED0-40BD-A199-AB81CDAE466C
description: 在 Microsoft Store 提交 API 中使用此方法，若要删除到合作伙伴中心帐户注册的应用包航班。
title: 删除软件包外部测试版
ms.date: 04/17/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 提交 API, 删除外部测试版
ms.localizationpriority: medium
ms.openlocfilehash: a3455973d86b0c9e7c779cca429e36fa32266ed6
ms.sourcegitcommit: 6a7dd4da2fc31ced7d1cdc6f7cf79c2e55dc5833
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2019
ms.locfileid: "58335105"
---
# <a name="delete-a-package-flight"></a>删除软件包外部测试版

在 Microsoft Store 提交 API 中使用此方法，若要删除到合作伙伴中心帐户注册的应用包航班。


## <a name="prerequisites"></a>系统必备

若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Microsoft Store 提交 API 的所有[先决条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

| 方法 | 请求 URI                                                      |
|--------|------------------------------------------------------------------|
| DELETE    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/flights/{flightId}` |


### <a name="request-header"></a>请求头

| Header        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | string | 必需。 Azure AD 访问令牌的格式为 **Bearer** *token*&lt;&gt;。 |


### <a name="request-parameters"></a>请求参数

| 名称        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| applicationId | string | 必需。 应用（包含要删除的软件包外部测试版）的应用商店 ID。 App Store ID 将显示在合作伙伴中心。  |
| flightId | string | 必需。 要删除的软件包外部测试版的 ID。 [创建软件包外部测试版](create-a-flight.md)和[获取应用的软件包外部测试版](get-flights-for-an-app.md)请求的响应数据中包含此 ID。 在合作伙伴中心创建航班，此 ID 是也可用在合作伙伴中心中的航班页的 URL。  |


### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。


### <a name="request-example"></a>请求示例

以下示例演示了如何删除软件包外部测试版。

```json
DELETE https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/flights/43e448df-97c9-4a43-a0bc-2a445e736bcd HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

如果成功，此方法会返回空的响应正文。

## <a name="error-codes"></a>错误代码

如果无法成功完成请求，该响应中会包含以下 HTTP 错误代码之一。

| 错误代码 |  描述                                                                                                                                                                           |
|--------|------------------|
| 400  | 请求参数无效。 |
| 404  | 找不到指定的软件包外部测试版。  |
| 409  | 找到指定的包航班，但无法在其当前状态下，删除或应用程序使用的合作伙伴中心功能[目前不支持通过 Microsoft Store 提交 API](create-and-manage-submissions-using-windows-store-services.md#not_supported)。 |   


## <a name="related-topics"></a>相关主题

* [创建和管理使用 Microsoft Store 服务的提交](create-and-manage-submissions-using-windows-store-services.md)
* [创建包航班](create-a-flight.md)
* [获取包航班](get-a-flight.md)
