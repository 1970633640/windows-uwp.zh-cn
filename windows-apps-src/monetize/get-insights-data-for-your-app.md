---
author: mcleanbyron
description: 使用 Microsoft 存储分析 API 中的此方法来获取您的应用程序的见解数据。
title: 获取见解数据
ms.author: mcleans
ms.date: 07/31/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10 uwp、 存储服务、 Microsoft 存储分析 API，见解
ms.localizationpriority: medium
ms.openlocfilehash: 53fbd91437e5dc702f8672c6cbadeea32a8a96bf
ms.sourcegitcommit: f2f4820dd2026f1b47a2b1bf2bc89d7220a79c1a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "2792063"
---
# <a name="get-insights-data"></a>获取见解数据

使用此方法在 Microsoft 存储分析 API 获取见解数据与收购、 运行状况和应用程序的使用情况指标期间给定的日期范围和其他可选的筛选器。 此信息也是 Windows 开发人员中心仪表板中的[洞察力报告](../publish/insights-report.md)中提供的。

## <a name="prerequisites"></a>必备条件


若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Microsoft Store 分析 API 的所有[先决条件](access-analytics-data-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

## <a name="request"></a>请求


### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI       |
|--------|----------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/insights``` |


### <a name="request-header"></a>请求头

| 标头        | 类型   | 说明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** &lt;*token*&gt;。 |


### <a name="request-parameters"></a>请求参数

| 参数        | 类型   |  说明      |  必需  
|---------------|--------|---------------|------|
| applicationId | 字符串 | 要为其检索见解数据的应用程序[存储 ID](in-app-purchases-and-trials.md#store-ids) 。 如果不指定此参数，响应正文将包含所有应用程序注册到您的帐户的见解数据。  |  否  |
| startDate | date | 开始日期的见解数据的日期范围内检索。 默认值为当前日期之前 30 天。 |  否  |
| endDate | date | 结束日期的见解数据的日期范围中进行检索。 默认值为当前日期。 |  否  |
| filter | 字符串  | 在响应中筛选行的一条或多条语句。 每条语句包含的响应正文中的字段名称和值使用 **eq** 或 **ne** 运算符进行关联，并且语句可以使用 **and** 或 **or** 进行组合。 *filter* 参数中的字符串值必须使用单引号括起来。 例如，*筛选器 = dataType eq 获取*。 <p/><p/>您可以指定以下筛选器字段：<p/><ul><li><strong>获取</strong></li><li><strong>运行状况</strong></li><li><strong>使用情况</strong></li></ul> | 否   |

### <a name="request-example"></a>请求示例

下面的示例演示用于获取见解数据的请求。 将 *applicationId* 值替换为你的应用的 Store ID。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/insights?applicationId=9NBLGGGZ5QDR&startDate=6/1/2018&endDate=6/15/2018&filter=dataType eq 'acquisition' or dataType eq 'health' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

### <a name="response-body"></a>响应正文

| 值      | 类型   | 说明                  |
|------------|--------|-------------------------------------------------------|
| 值      | array  | 包含见解数据的应用程序的对象的数组。 有关每个对象中的数据的详细信息，请参阅下面的[洞察值](#insight-values)部分。                                                                                                                      |
| TotalCount | int    | 查询的数据结果中的行总数。                 |


### <a name="insight-values"></a>洞察值

*Value* 数组中的元素包含以下值。

| 值               | 类型   | 描述                           |
|---------------------|--------|-------------------------------------------|
| applicationId       | 字符串 | 要为其检索见解数据应用程序的存储 ID。     |
| insightDate                | 字符串 | 我们在其标识特定指标的更改的日期。 此日期表示在其中我们检测到显著增大周末或减少与之前的周相比指标。 |
| 数据类型     | 字符串 | 指定此洞察介绍的一般分析区域的以下字符串之一：<p/><ul><li><strong>获取</strong></li><li><strong>运行状况</strong></li><li><strong>使用情况</strong></li></ul>   |
| insightDetail          | array | 一个或多个[InsightDetail 值](#insightdetail-values)表示当前洞察的详细信息。    |


### <a name="insightdetail-values"></a>InsightDetail 值

| 值               | 类型   | 说明                           |
|---------------------|--------|-------------------------------------------|
| FactName           | 字符串 | 下列值，该值指示当前洞察或当前维度介绍，指标之一基于的**数据类型**的值。<ul><li>对于**运行状况**，此值始终为**点击次数**。</li><li>**获取**，此值始终为**AcquisitionQuantity**。</li><li>**使用情况**，此值可以是以下字符串之一：<ul><li><strong>DailyActiveUsers</strong></li><li><strong>EngagementDurationMinutes</strong></li><li><strong>DailyActiveDevices</strong></li><li><strong>DailyNewUsers</strong></li><li><strong>DailySessionCount</strong></li></ul></ul>  |
| SubDimensions         | array |  介绍洞察单个指标的一个或多个对象。   |
| PercentChange            | 字符串 |  在您的整个客户群之间指标更改百分比。  |
| 维度           | 字符串 |  当前维度中所述的度量名称。 示例包括**EventType**、**市场**、 **DeviceType**、 **PackageVersion**、 **AcquisitionType**、 **AgeGroup**和**性别**。   |
| DimensionValue              | 字符串 | 当前维度中描述的度量值。 例如，如果**维度**， **EventType** **DimensionValue**可能**故障**或**挂起**。   |
| FactValue     | 字符串 | 在检测到洞察日期度量的绝对值。  |
| Direction | 字符串 |  更改 （**正值**或**负值**） 的方向。   |
| 日期              | 字符串 |  我们在其标识与当前洞察或当前维度相关更改日期。   |

### <a name="response-example"></a>回复示例

以下示例举例说明此请求的 JSON 响应正文。

```json
{
  "Value": [
    {
      "applicationId": "9NBLGGGZ5QDR",
      "insightDate": "2018-06-03T00:00:00",
      "dataType": "health",
      "insightDetail": [
        {
          "FactName": "HitCount",
          "SubDimensions": [
            {
              "FactName:": "HitCount",
              "PercentChange": "21",
              "DimensionValue:": "DE",
              "FactValue": "109",
              "Direction": "Positive",
              "Date": "6/3/2018 12:00:00 AM",
              "DimensionName": "Market"
            }
          ],
          "DimensionValue": "crash",
          "Date": "6/3/2018 12:00:00 AM",
          "DimensionName": "EventType"
        },
        {
          "FactName": "HitCount",
          "SubDimensions": [
            {
              "FactName:": "HitCount",
              "PercentChange": "71",
              "DimensionValue:": "JP",
              "FactValue": "112",
              "Direction": "Positive",
              "Date": "6/3/2018 12:00:00 AM",
              "DimensionName": "Market"
            }
          ],
          "DimensionValue": "hang",
          "Date": "6/3/2018 12:00:00 AM",
          "DimensionName": "EventType"
        },
      ],
      "insightId": "9CY0F3VBT1AS942AFQaeyO0k2zUKfyOhrOHc0036Iwc="
    }
  ],
  "@nextLink": null,
  "TotalCount": 2
}
```

## <a name="related-topics"></a>相关主题

* [见解报告](../publish/insights-report.md)
* [使用 Microsoft Store 服务访问分析数据](access-analytics-data-using-windows-store-services.md)
