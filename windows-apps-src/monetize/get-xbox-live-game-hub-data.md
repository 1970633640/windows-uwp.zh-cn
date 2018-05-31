---
author: mcleanbyron
description: 在 Microsoft Store 分析 API 中使用此方法获取 Xbox Live 游戏中心数据。
title: 获取 Xbox Live 游戏中心数据
ms.author: mcleans
ms.date: 04/16/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp, Microsoft Store 服务, Microsoft Store 分析 API, Xbox Live 分析, 游戏中心
ms.localizationpriority: medium
ms.openlocfilehash: 0d34c95e615a10131b3e7f3ffe9ceb246b652727
ms.sourcegitcommit: 91511d2d1dc8ab74b566aaeab3ef2139e7ed4945
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2018
ms.locfileid: "1815782"
---
# <a name="get-xbox-live-game-hub-data"></a>获取 Xbox Live 游戏中心数据


在 Microsoft Store 分析 API 中使用此方法获取你的[支持 Xbox Live 的游戏](../xbox-live/index.md)的游戏中心数据。 还可以在 Windows 开发人员中心仪表板的 [Xbox 分析报告](../publish/xbox-analytics-report.md)中获取此信息。

> [!IMPORTANT]
> 目前，此方法只支持那些支持 Xbox Live 并由 [Microsoft 合作伙伴](../xbox-live/developer-program-overview.md#microsoft-partners)发布或通过 [ID@Xbox 计划](../xbox-live/developer-program-overview.md#id)提交的游戏。 它不会返回通过 [Xbox Live 创意者计划](../xbox-live/developer-program-overview.md#xbox-live-creators-program)提交的游戏的数据。

## <a name="prerequisites"></a>先决条件

若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Microsoft Store 分析 API 的所有[先决条件](access-analytics-data-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

## <a name="request"></a>请求


### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI       |
|--------|----------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/gameanalytics``` |


### <a name="request-header"></a>请求头

| 标头        | 类型   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** &lt;*token*&gt;。 |


### <a name="request-parameters"></a>请求参数

| 参数        | 类型   |  说明      |  必需  
|---------------|--------|---------------|------|
| applicationId | 字符串 | 你要检索 Xbox Live 游戏中心数据的游戏的 [Store ID](in-app-purchases-and-trials.md#store-ids)。  |  是  |
| metricType | 字符串 | 指定要检索的 Xbox Live 分析数据的类型的字符串。 对于此方法，指定值 **communitymanagergamehub**。  |  是  |
| startDate | 日期 | 要检索的游戏中心数据日期范围中的开始日期。 默认值为当前日期之前 30 天。 |  否  |
| endDate | 日期 | 要检索的游戏中心数据日期范围中的结束日期。 默认值为当前日期。 |  否  |
| top | int | 要在请求中返回的数据行数。 如果未指定，最大值和默认值为 10000。 当查询中存在多行数据时，响应正文中包含的下一个链接可用于请求下一页数据。 |  否  |
| skip | int | 要在查询中跳过的行数。 使用此参数可以浏览较大的数据集。 例如，top=10000 和 skip=0，将检索前 10000 行数据；top=10000 和 skip=10000，将检索之后的 10000 行数据，依此类推。 |  否  |


### <a name="request-example"></a>请求示例

以下示例演示了一个请求，该请求用于获取你的支持 Xbox Live 的游戏的游戏中心数据。 将 *applicationId* 值替换为你的游戏的 Store ID。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/gameanalytics?applicationId=9NBLGGGZ5QDR&metrictype=communitymanagergamehub&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应


| 值      | 类型   | 描述                  |
|------------|--------|-------------------------------------------------------|
| 值      | array  | 一个对象数组，其中包含指定时间范围内每个日期的游戏中心数据。 有关每个对象中的数据的详细信息，请参阅下表。                                                                                                                      |
| @nextLink  | 字符串 | 如果存在数据的其他页，此字符串中包含的 URI 可用于请求数据的下一页。 例如，当请求的 **top** 参数设置为 10000，但查询的数据超过 10000 行时，就会返回此值。 |
| TotalCount | int    | 查询的数据结果中的行总数。  |


*Value* 数组中的元素包含以下值。

| 值               | 类型   | 说明                           |
|---------------------|--------|-------------------------------------------|
| date                | 字符串 | 此项目中游戏中心数据的日期。 |
| applicationId       | 字符串 | 你要为其检索游戏中心数据的游戏的 Store ID。     |
| gameHubLikeCount     | 数字 |   在指定日期添加到游戏中心页面上的赞的数量。   |
| gameHubCommentCount          | 数字 |  在指定日期添加到你的应用的游戏中心页面上的评论的数量。  |
| gameHubShareCount           | 数字 | 客户在指定日期共享你的应用的游戏中心页面的次数。   |


### <a name="response-example"></a>响应示例

以下示例举例说明此请求的 JSON 响应正文。

```json
{
  "Value": [
    {
      "date": "2018-01-04",
      "applicationId": "9NBLGGGZ5QDR",
      "gameHubLikeCount": 10,
      "gameHubCommentCount": 1,
      "gameHubShareCount": 0
    },
    {
      "date": "2018-01-05",
      "applicationId": "9NBLGGGZ5QDR",
      "gameHubLikeCount": 12,
      "gameHubCommentCount": 1,
      "gameHubShareCount": 0
    }
  ],
  "@nextLink": null,
  "TotalCount": 26
}
```

## <a name="related-topics"></a>相关主题

* [使用 Microsoft Store 服务访问分析数据](access-analytics-data-using-windows-store-services.md)
* [获取 Xbox Live 分析数据](get-xbox-live-analytics.md)
* [获取 Xbox Live 成就数据](get-xbox-live-achievements-data.md)
* [获取 Xbox Live 运行状况数据](get-xbox-live-health-data.md)
* [获取 Xbox Live 中心数据](get-xbox-live-club-data.md)
* [获取 Xbox Live 多人游戏数据](get-xbox-live-multiplayer-data.md)
