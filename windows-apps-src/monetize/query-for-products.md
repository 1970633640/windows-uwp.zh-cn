---
ms.assetid: D1F233EC-24B5-4F84-A92F-2030753E608E
description: 在 Microsoft Store 收集 API 中使用此方法，以获取客户在与你的 Azure AD 客户端 ID 相关联的应用中所拥有的所有产品。 你可以将查询范围设置为特定产品，或使用其他筛选器。
title: 查询产品
ms.date: 03/19/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 收集 API, 查看产品
ms.localizationpriority: medium
ms.openlocfilehash: 700cb111f74a4534f2f5e1de70eddfb88b456aa7
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57596802"
---
# <a name="query-for-products"></a>查询产品


在 Microsoft Store 收集 API 中使用此方法，以获取客户在与你的 Azure AD 客户端 ID 相关联的应用中所拥有的所有产品。 你可以将查询范围设置为特定产品，或使用其他筛选器。

此方法旨在由你的服务调用，用于响应来自你的应用的消息。 你的服务不应定期按计划轮询所有用户。

## <a name="prerequisites"></a>必备条件


若要使用此方法，你需要：

* 受众 URI 值为 `https://onestore.microsoft.com` 的 Azure AD 访问令牌。
* 一个 Microsoft Store ID 密钥，表示要获得其产品的用户的身份。

有关详细信息，请参阅[管理来自服务的产品授权](view-and-grant-products-from-a-service.md)。

## <a name="request"></a>请求

### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI                                                 |
|--------|-------------------------------------------------------------|
| POST   | ```https://collections.mp.microsoft.com/v6.0/collections/query``` |


### <a name="request-header"></a>请求头

| 标头         | 在任务栏的搜索框中键入   | 描述                                                                                           |
|----------------|--------|-------------------------------------------------------------------------------------------------------|
| 授权  | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** *token*&lt;&gt;。                           |
| 主机           | 字符串 | 必须设置为值 **collections.mp.microsoft.com**。                                            |
| 内容长度 | 数字 | 请求正文的长度。                                                                       |
| 内容类型   | 字符串 | 指定请求和响应类型。 当前，唯一受支持的值为 **application/json**。 |


### <a name="request-body"></a>请求正文

| 参数         | 在任务栏的搜索框中键入         | 描述         | 必需 |
|-------------------|--------------|---------------------|----------|
| 受益人     | UserIdentity | 表示要为产品查询的用户的 UserIdentity 对象。 有关详细信息，请参阅下表。    | 是      |
| ContinuationToken | 字符串       | 如果有多组产品，响应正文将在达到页面限制时返回延续令牌。 在后续调用中提供此处的延续令牌以检索剩余 产品。       | 否       |
| MaxPageSize       | 数字       | 要在一次响应中返回的最大产品数。 默认值和最大值为 100。                 | 否       |
| ModifiedAfter     | 日期/时间     | 如果已指定，该服务仅返回已在此日期后修改的产品。        | 否       |
| ParentProductID   | 字符串       | 如果已指定，该服务仅返回对应于指定应用的加载项。      | 否       |
| ProductSkuID     | list&lt;ProductSkuId&gt; | 如果已指定，该服务仅返回适用于所提供的产品/SKU 对的产品。 有关详细信息，请参阅下表。      | 否       |
| ProductType      | list&lt;string&gt;       | 指定要在查询结果中返回的产品类型。 受支持的产品类型为 **Application**、**Durable** 和 **UnmanagedConsumable**。     | 是       |
| ValidityType      | 字符串       | 当设置为 **All** 时，将返回用户的所有产品，包括已过期的项目。 当设置为 **Valid** 时，仅返回在此时有效的产品（即，它们的状态为活动，开始日期 &lt; 现在，结束日期 &gt; 现在）。 | 否       |


UserIdentity 对象包含以下参数。

| 参数            | 在任务栏的搜索框中键入   |  描述      | 必需 |
|----------------------|--------|----------------|----------|
| IdentityType         | 字符串 | 指定字符串值 **b2b**。    | 是      |
| identityValue        | 字符串 | [Microsoft Store ID 密钥](view-and-grant-products-from-a-service.md#step-4)，表示要查询其产品的用户的身份。  | 是      |
| localTicketReference | 字符串 | 已返回产品的请求标识符。 响应正文中返回的项目将具有匹配的 *localTicketReference*。 建议使用与 Microsoft Store ID 密钥中的 *userId* 声明相同的值。 | 是      |


ProductSkuId 对象包含以下参数。

| 参数 | 在任务栏的搜索框中键入   | 描述          | 必需 |
|-----------|--------|----------------------|----------|
| productId | 字符串 | Microsoft Store 目录中的[产品](in-app-purchases-and-trials.md#products-skus-and-availabilities)的 [Store ID](in-app-purchases-and-trials.md#store-ids)。 产品的示例应用商店 ID 为 9NBLGGH42CFD。 | 是      |
| SkuID     | 字符串 | Microsoft Store 目录中的产品 [SKU](in-app-purchases-and-trials.md#products-skus-and-availabilities) 的 [Store ID](in-app-purchases-and-trials.md#store-ids)。 SKU 的示例应用商店 ID 为 0010。       | 是      |


### <a name="request-example"></a>请求示例

```syntax
POST https://collections.mp.microsoft.com/v6.0/collections/query HTTP/1.1
Authorization: Bearer eyJ0eXAiOiJKV1Q…….
Host: collections.mp.microsoft.com
Content-Length: 2531
Content-Type: application/json

{
  "maxPageSize": 100,
  "beneficiaries": [
    {
      "localTicketReference": "1055521810674918",
      "identityValue": "eyJ0eXAiOiJ……",
      "identityType": "b2b"
    }
  ],
  "modifiedAfter": "\/Date(-62135568000000)\/",
  "productSkuIds": [
    {
      "productId": "9NBLGGH5WVP6",
      "skuId": "0010"
    }
  ],
  "productTypes": [
    "UnmanagedConsumable"
  ],
  "validityType": "All"
}
```

## <a name="response"></a>响应


### <a name="response-body"></a>响应正文

| 参数         | 在任务栏的搜索框中键入                     | 描述          | 必需 |
|-------------------|--------------------------|-----------------------|----------|
| ContinuationToken | 字符串                   | 如果有多组产品，此令牌将在达到页面限制时返回。 你可以在后续调用中指定此延续令牌以检索剩余 产品。 | 否       |
| 项目             | CollectionItemContractV6 | 指定用户的产品的数组。 有关详细信息，请参阅下表。        | 否       |


CollectionItemContractV6 对象包含以下参数。

| 参数            | 在任务栏的搜索框中键入               | 描述            | 必需 |
|----------------------|--------------------|-------------------------|----------|
| AcquiredDate         | 日期/时间           | 用户获取该项目的日期。                  | 是      |
| campaignId           | 字符串             | 在购买时为此项目提供的市场活动 ID。                  | 否       |
| devOfferId           | 字符串             | 应用内购买的优惠 ID。              | 否       |
| endDate              | 日期/时间           | 项目的结束日期。              | 是      |
| FulfillmentData      | 字符串             | 不适用         | 否       |
| InAppOfferToken      | 字符串             | 开发人员指定产品 ID 字符串分配给合作伙伴中心中的项。 ID 是一个示例产品*product123*。 | 否       |
| ItemID               | 字符串             | 用于从用户所拥有的其他项目标识此集合项 的 ID。 此 ID 对于每个产品都是唯一的。   | 是      |
| localTicketReference | 字符串             | 请求正文中上次提供的 *localTicketReference* 的 ID。                  | 是      |
| ModifiedDate         | 日期/时间           | 最后修改此项目的日期。              | 是      |
| orderId              | 字符串             | 获取此项目的顺序 ID（如果存在）。              | 否       |
| orderLineItemId      | 字符串             | 获取此项目的特定顺序的行项（如果存在） 。              | 否       |
| OwnershipType        | 字符串             | 字符串 *OwnedByBeneficiary*。   | 是      |
| productId            | 字符串             | Microsoft Store 目录中的[产品](in-app-purchases-and-trials.md#products-skus-and-availabilities)的 [Store ID](in-app-purchases-and-trials.md#store-ids)。 产品的示例应用商店 ID 为 9NBLGGH42CFD。          | 是      |
| productType          | 字符串             | 以下产品类型之一：**应用程序**，**持久**，和**UnmanagedConsumable**。        | 是      |
| PurchasedCountry     | 字符串             | 不适用   | 否       |
| 购买者            | IdentityContractV6 | 这表示项目的购买者的标识（如果存在）。 请参阅下面有关此对象的详细信息。        | 否       |
| quantity             | 数字             | 项目的数量。 当前，这将始终为 1。      | 否       |
| skuId                | 字符串             | Microsoft Store 目录中的产品 [SKU](in-app-purchases-and-trials.md#products-skus-and-availabilities) 的 [Store ID](in-app-purchases-and-trials.md#store-ids)。 SKU 的示例应用商店 ID 为 0010。     | 是      |
| SkuType              | 字符串             | SKU 的类型。 可能的值包括 **Trial**、**Full** 和 **Rental**。        | 是      |
| startDate            | 日期/时间           | 项目开始有效的日期。       | 是      |
| status               | 字符串             | 项目的状态。 可能的值包括 **Active**、**Expired**、**Revoked** 和 **Banned**。    | 是      |
| tags                 | 字符串             | 不适用    | 是      |
| transactionId        | GUID               | 因购买此项目而产生的事务 ID。 可 用于将项目报告为已完成。      | 是      |


IdentityContractV6 对象包含以下参数。

| 参数     | 在任务栏的搜索框中键入   | 描述                                                                        | 必需 |
|---------------|--------|------------------------------------------------------------------------------------|----------|
| IdentityType  | 字符串 | 包含值 *pub*。                                                      | 是      |
| identityValue | 字符串 | 指定的 Microsoft Store ID 密钥的 *publisherUserId* 字符串值。 | 是      |


### <a name="response-example"></a>响应示例

```syntax
HTTP/1.1 200 OK
Content-Length: 7241
Content-Type: application/json
MS-CorrelationId: 699681ce-662c-4841-920a-f2269b2b4e6c
MS-RequestId: a9988cf9-652b-4791-beba-b0e732121a12
MS-CV: xu2HW6SrSkyfHyFh.0.1
MS-ServerId: 020022359
Date: Tue, 22 Sep 2015 20:28:18 GMT

{
  "items" : [
    {
      "acquiredDate" : "2015-09-22T19:22:51.2068724+00:00",
      "devOfferId" : "f9587c53-540a-498b-a281-8a349491ed47",
      "endDate" : "9999-12-31T23:59:59.9999999+00:00",
      "fulfillmentData" : [],
      "inAppOfferToken" : "consumable2",
      "itemId" : "4b8fbb13127a41f299270ea668681c1d",
      "localTicketReference" : "1055521810674918",
      "modifiedDate" : "2015-09-22T19:22:51.2513155+00:00",
      "orderId" : "4ba5960d-4ec6-4a81-ac20-aafce02ddf31",
      "ownershipType" : "OwnedByBeneficiary",
      "productId" : "9NBLGGH5WVP6",
      "productType" : "UnmanagedConsumable",
      "purchaser" : {
        "identityType" : "pub",
        "identityValue" : "user123"
      },
      "skuId" : "0010",
      "skuType" : "Full",
      "startDate" : "2015-09-22T19:22:51.2068724+00:00",
      "status" : "Active",
      "tags" : [],
      "transactionId" : "4ba5960d-4ec6-4a81-ac20-aafce02ddf31"
    }
  ]
}
```

## <a name="related-topics"></a>相关主题

* [从服务管理产品的权利](view-and-grant-products-from-a-service.md)
* [为满足报告易耗型产品](report-consumable-products-as-fulfilled.md)
* [授予免费产品](grant-free-products.md)
* [续订 Microsoft Store ID 键](renew-a-windows-store-id-key.md)
