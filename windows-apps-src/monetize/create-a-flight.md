---
ms.assetid: 8C1E9E36-13AF-4386-9D0F-F9CB320F02F5
description: 在 Microsoft Store 提交 API 中使用此方法来创建到合作伙伴中心帐户注册的应用包航班。
title: 创建软件包外部测试版
ms.date: 04/16/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 提交 API, 创建外部测试版
ms.localizationpriority: medium
ms.openlocfilehash: 0c71dfc05bf2f283652087620848396b731871cd
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371966"
---
# <a name="create-a-package-flight"></a>创建软件包外部测试版

在 Microsoft Store 提交 API 中使用此方法来创建到合作伙伴中心帐户注册的应用包航班。

> [!NOTE]
> 此方法无需任何提交即可创建软件包外部测试版。 若要创建软件包外部测试版的提交，请参阅[管理软件包外部测试版提交](manage-flight-submissions.md)中的方法。

## <a name="prerequisites"></a>系统必备

若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Microsoft Store 提交 API 的所有[先决条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

| 方法 | 请求 URI                                                      |
|--------|------------------------------------------------------------------|
| 发布    | ```https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/flights``` |


### <a name="request-header"></a>请求头

| Header        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | string | 必需。 Azure AD 访问令牌的格式为 **Bearer** *token*&lt;&gt;。 |


### <a name="request-parameters"></a>请求参数

| 名称        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| applicationId | string | 必需。 要创建软件包外部测试版的应用的应用商店 ID。 有关应用商店 ID 的详细信息，请参阅[查看应用标识详细信息](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)。  |


### <a name="request-body"></a>请求正文

请求正文具有以下参数。

|  参数  |  在任务栏的搜索框中键入  |  描述  |  必需  |
|------|------|------|------|
|  friendlyName  |  string  |  软件包外部测试版的名称，如开发人员所指定。  |  否  |
|  groupIds  |  数组  |  包含与软件包外部测试版关联的外部测试版组 ID 的字符串数组。 有关外部测试版组的详细信息，请参阅[软件包外部测试版](https://docs.microsoft.com/windows/uwp/publish/package-flights)。  |  否  |
|  rankHigherThan  |  string  |  排名紧跟在当前软件包外部测试版之后的软件包外部测试版的友好名称。 如果未设置此参数，新软件包外部测试版在所有软件包外部测试版中排名最高。 有关排名的外部测试版组的详细信息，请参阅 [软件包外部测试版](https://docs.microsoft.com/windows/uwp/publish/package-flights)。    |  否  |


### <a name="request-example"></a>请求示例

以下示例演示了如何为具有应用商店 ID 9WZDNCRD911W 的应用创建新的软件包外部测试版。

```syntax
POST https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/flights HTTP/1.1
Authorization: Bearer eyJ0eXAiOiJKV1Q...
Content-Type: application/json
{
  "friendlyName": "myflight",
  "groupIds": [
    0
  ],
  "rankHigherThan": null
}

```

## <a name="response"></a>响应

以下示例演示了成功调用此方法的 JSON 响应正文。 有关响应正文中这些值的更多详细信息，请参阅以下部分。

```json
{
  "flightId": "43e448df-97c9-4a43-a0bc-2a445e736bcd",
  "friendlyName": "myflight",
  "groupIds": [
    "0"
  ],
  "rankHigherThan": "671c2857-725e-4faf-9e9e-ea1191ef879c"
}
```

### <a name="response-body"></a>响应正文

| 值      | 在任务栏的搜索框中键入   | 描述                                                                                                                                                                                                                                                                         |
|------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| flightId            | string  | 软件包外部测试版的 ID。 通过合作伙伴中心提供此值。  |
| friendlyName           | string  | 软件包外部测试版的名称，如请求中所指定。   |  
| groupIds           | 数组  | 包含与软件包外部测试版关联的外部测试版组 ID 的字符串数组，如请求中所指定。 有关外部测试版组的详细信息，请参阅[软件包外部测试版](https://docs.microsoft.com/windows/uwp/publish/package-flights)。   |
| rankHigherThan           | string  | 排名紧跟在当前软件包外部测试版之后的软件包外部测试版的友好名称，如请求中所指定。 有关排名的外部测试版组的详细信息，请参阅 [软件包外部测试版](https://docs.microsoft.com/windows/uwp/publish/package-flights)。  |


## <a name="error-codes"></a>错误代码

如果无法成功完成请求，该响应中会包含以下 HTTP 错误代码之一。

| 错误代码 |  描述   |
|--------|------------------|
| 400  | 请求无效。 |
| 409  | 无法创建包航班，由于其当前状态，或该应用使用的合作伙伴中心功能[目前不支持通过 Microsoft Store 提交 API](create-and-manage-submissions-using-windows-store-services.md#not_supported)。 |   


## <a name="related-topics"></a>相关主题

* [创建和管理使用 Microsoft Store 服务的提交](create-and-manage-submissions-using-windows-store-services.md)
* [获取包航班](get-a-flight.md)
* [删除包航班](delete-a-flight.md)
