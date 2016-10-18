---
author: mcleanbyron
ms.assetid: B0AD0B8E-867E-4403-9CF6-43C81F3C30CA
description: "在 Windows 应用商店提交 API 中使用此方法，为注册到 Windows 开发人员中心帐户的应用检索软件包外部测试版信息。"
title: "使用 Windows 应用商店提交 API 为应用获取软件包外部测试版"
translationtype: Human Translation
ms.sourcegitcommit: 5f975d0a99539292e1ce91ca09dbd5fac11c4a49
ms.openlocfilehash: a49e4f2cf7110e12dd33a5baa37e328a39bae348

---

# 使用 Windows 应用商店提交 API 为应用获取软件包外部测试版




在 Windows 应用商店提交 API 中使用此方法，为注册到 Windows 开发人员中心帐户的应用列出软件包外部测试版。 有关软件包外部测试版的详细信息，请参阅[软件包外部测试版](https://msdn.microsoft.com/windows/uwp/publish/package-flights)。

## 先决条件

若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Windows 应用商店提交 API 的所有[先决条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

>**注意**&nbsp;&nbsp;此方法只可以用于授予使用 Windows 应用商店提交 API 权限的 Windows 开发人员中心帐户。 并非所有帐户都已启用此权限。

## 请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

| 方法 | 请求 URI                                                      |
|--------|------------------------------------------------------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/listflights``` |

<span/>
 
### 请求头

| 标头        | 类型   | 说明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** &lt;*token*&gt;。 |

<span/>

### 请求参数

| 名称        | 类型   | 说明  |  必需  |    
|---------------|--------|----------------------------------|
| applicationId | 字符串 | 必需。 要检索软件包外部测试版的应用的应用商店 ID。 有关应用商店 ID 的详细信息，请参阅[查看应用标识详细信息](https://msdn.microsoft.com/windows/uwp/publish/view-app-identity-details)。  |  是  |
|  top  |  int  |  要在请求中返回的项数（即，要返回的软件包外部测试版数）。 如果应用具有的软件包外部测试版超过在查询中指定的值，响应正文将包括可追加到方法 URI 的相对 URI 路径，用于请求下一页数据。  |  否  |
|  skip  |  int  |  返回剩余项之前，在查询中绕过的项数。 使用此参数分页浏览数据集。 例如，top=10 和 skip=0 可检索项目 1 到 10，top=10 和 skip=10 可检索项目 11 到 20，依此类推。  |  否  |

<span/>

### 请求正文

请勿为此方法提供请求正文。

### 请求示例

以下示例演示了如何为应用列出所有软件包外部测试版。

```
GET https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/listflights HTTP/1.1
Authorization: Bearer <your access token>
```

以下示例演示了如何为应用列出第一个软件包外部测试版。

```
GET https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/listflights?top=1 HTTP/1.1
Authorization: Bearer <your access token>
```

## 响应

以下示例演示了成功请求应用的第一个软件包外部测试版（共三个软件包外部测试版）返回的 JSON 响应正文。 有关响应正文中这些值的详细信息，请参阅以下部分。

```json
{
  "value": [
    {
      "flightId": "7bfc11d5-f710-47c5-8a98-e04bb5aad310",
      "friendlyName": "myflight",
      "lastPublishedFlightSubmission": {
        "id": "1152921504621086517",
        "resourceLocation": "flights/7bfc11d5-f710-47c5-8a98-e04bb5aad310/submissions/1152921504621086517"
      },
      "pendingFlightSubmission": {
        "id": "1152921504621215786",
        "resourceLocation": "flights/7bfc11d5-f710-47c5-8a98-e04bb5aad310/submissions/1152921504621215786"
      },
      "groupIds": [
        "1152921504606962205"
      ],
      "rankHigherThan": "Non-flighted submission"
    }
  ],
  "totalCount": 3
}
```

### 响应正文

| 值      | 类型   | 描述                                                                                                                                                                                                                                                                         |
|------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| @nextLink  | 字符串 | 如果存在数据的其他页，此字符串中包含可附加到基本 ```https://manage.devcenter.microsoft.com/v1.0/my/``` 请求 URI 的相对路径，用于请求下一页数据。 例如，如果初始请求正文的 *top* 参数设置为 2，但应用中有 4 个软件包外部测试版，响应正文将包含 ```applications/{applicationid}/listflights/?skip=2&top=2``` 的 @nextLink 值，指示你可以调用 ```https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationid}/listflights/?skip=2&top=2``` 请求接下来的 2 个软件包外部测试版。 |
| 值      | 数组  | 为指定的应用提供软件包外部测试版相关信息的对象数组。 有关每个对象中的数据的详细信息，请参阅[外部测试版资源](get-app-data.md#flight-object)。                                                                                                                           |
| totalCount | int    | 查询的数据结果中的行总数（即，指定应用的软件包外部测试版的总数）。                                                                                                                                                                                                                             |

<span/>

## 错误代码

如果无法成功完成请求，该响应中会包含以下 HTTP 错误代码之一。

| 错误代码 |  描述   |
|--------|------------------|
| 404  | 找不到任何软件包外部测试版。 |
| 409  | 应用使用的开发人员中心仪表板功能[当前不受 Windows 应用商店提交 API 支持](create-and-manage-submissions-using-windows-store-services.md#not_supported)。  |

<span/>

## 相关主题

* [使用 Windows 应用商店服务创建和管理提交](create-and-manage-submissions-using-windows-store-services.md)
* [获取所有应用](get-all-apps.md)
* [获取应用](get-an-app.md)
* [获取应用的加载项](get-add-ons-for-an-app.md)



<!--HONumber=Aug16_HO5-->


