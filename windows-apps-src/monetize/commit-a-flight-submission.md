---
author: Xansky
ms.assetid: F94AF8F6-0742-4A3F-938E-177472F96C00
description: 在 Microsoft Store 提交 API 中使用此方法，来确认新的或更新的软件包外部测试版提交到合作伙伴中心。
title: 确认软件包外部测试版提交
ms.author: mhopkins
ms.date: 04/17/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 提交 API, 确认外部测试版提交
ms.localizationpriority: medium
ms.openlocfilehash: 58293a73589c7d2780360df24bcc24f38335f1e5
ms.sourcegitcommit: e814a13978f33654d8e995584f4b047cb53e0aef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "6034183"
---
# <a name="commit-a-package-flight-submission"></a>确认软件包外部测试版提交

在 Microsoft Store 提交 API 中使用此方法，来确认新的或更新的软件包外部测试版提交到合作伙伴中心。 确认操作警报合作伙伴中心，提交数据已上传 （包括任何相关的软件包）。 作为响应，合作伙伴中心提交以供引入和发布的提交数据所做的更改。 确认操作成功后，在合作伙伴中心中显示对提交更改。

有关确认操作如何适应使用 Microsoft Store 提交 API 创建软件包外部测试版提交的过程的详细信息，请参阅[管理软件包外部测试版提交](manage-flight-submissions.md)。

## <a name="prerequisites"></a>先决条件

若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Microsoft Store 提交 API 的所有[先决条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。
* [创建软件包外部测试版提交](create-a-flight-submission.md)，然后通过对提交数据所做的任何必要更改[更新提交](update-a-flight-submission.md)。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

| 方法 | 请求 URI                                                      |
|--------|------------------------------------------------------------------|
| POST    | ```https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/flights/{flightId}/submissions/{submissionId}/commit``` |


### <a name="request-header"></a>请求标头

| 标头        | 类型   | 说明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** &lt;*token*&gt;。 |


### <a name="request-parameters"></a>请求参数

| 名称        | 类型   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| applicationId | 字符串 | 必需。 应用（包含要确认的软件包外部测试版提交）的应用商店 ID。 在合作伙伴中心是可用的应用商店 ID。  |
| flightId | 字符串 | 必需。 软件包外部测试版（包含要确认的提交）的 ID。 此 ID 包含在[创建软件包外部测试版](create-a-flight.md)和[获取应用的软件包外部测试版](get-flights-for-an-app.md)请求的响应数据中。 在合作伙伴中心中创建外部测试版，此 ID 也包含在合作伙伴中心中的外部测试版页面的 URL 中可用。  |
| submissionId | 字符串 | 必需。 要确认的提交的 ID。 此 ID 包含在[创建软件包外部测试版提交](create-a-flight-submission.md)请求的响应数据中。 对于已在合作伙伴中心中创建的提交，此 ID 也包含在合作伙伴中心中的提交页面的 URL 中可用。  |


### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-example"></a>请求示例

以下示例演示如何确认软件包外部测试版提交。

```
POST https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/flights/43e448df-97c9-4a43-a0bc-2a445e736bcd/submissions/1152921504621243649/commit HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了成功调用此方法的 JSON 响应正文。 有关响应正文中这些值的更多详细信息，请参阅以下部分。

```json
{
  "status": "CommitStarted"
}
```

### <a name="response-body"></a>响应正文

| 值      | 类型   | 描述                                                                                                                                                                                                                                                                         |
|------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 状态           | 字符串  | 提交的状态。 这可以是以下值之一： <ul><li>None</li><li>Canceled</li><li>PendingCommit</li><li>CommitStarted</li><li>CommitFailed</li><li>PendingPublication</li><li>Publishing</li><li>Published</li><li>PublishFailed</li><li>PreProcessing</li><li>PreProcessingFailed</li><li>Certification</li><li>CertificationFailed</li><li>Release</li><li>ReleaseFailed</li></ul>  |


## <a name="error-codes"></a>错误代码

如果无法成功完成请求，该响应中会包含以下 HTTP 错误代码之一。

| 错误代码 |  描述   |
|--------|------------------|
| 400  | 请求参数无效。 |
| 404  | 找不到指定提交。 |
| 409  | 指定的提交已找到，但它可能无法确认; 在其当前状态，或者应用使用[当前不受 Microsoft Store 提交 API](create-and-manage-submissions-using-windows-store-services.md#not_supported)的合作伙伴中心功能。 |


## <a name="related-topics"></a>相关主题

* [使用 Microsoft Store 服务创建和管理提交](create-and-manage-submissions-using-windows-store-services.md)
* [管理软件包外部测试版提交](manage-flight-submissions.md)
* [获取软件包外部测试版提交](get-a-flight-submission.md)
* [创建软件包外部测试版提交](create-a-flight-submission.md)
* [更新软件包外部测试版提交](update-a-flight-submission.md)
* [删除软件包外部测试版提交](delete-a-flight-submission.md)
* [获取软件包外部测试版提交的状态](get-status-for-a-flight-submission.md)
