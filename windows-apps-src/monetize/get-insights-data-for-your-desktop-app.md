---
author: mcleanbyron
description: 在 Microsoft Store 分析 API 中使用此方法，可获取桌面应用程序的见解数据。
title: 获取桌面应用程序的见解数据
ms.author: mcleans
ms.date: 07/31/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp，应用商店服务，Microsoft Store 分析 API，见解
ms.localizationpriority: medium
ms.openlocfilehash: e7ca6eed40af37276b5b4c98ec7b1b709bdadfb9
ms.sourcegitcommit: 7efffcc715a4be26f0cf7f7e249653d8c356319b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "3123264"
---
# <a name="get-insights-data-for-your-desktop-application"></a>获取桌面应用程序的见解数据

在 Microsoft Store 分析 API 中使用此方法来获取与已添加到[Windows 桌面应用程序](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)的桌面应用程序的运行状况指标的数据相关的见解。 此数据也是在 Windows 开发人员中心仪表板的桌面应用程序在[运行状况报告](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program#health-report)中可用。

## <a name="prerequisites"></a>必备条件

若要使用此方法，首先需要执行以下操作：

* 如果尚未开始操作，请先完成 Microsoft Store 分析 API 的所有[先决条件](access-analytics-data-using-windows-store-services.md#prerequisites)。
* [获取 Azure AD 访问令牌](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

## <a name="request"></a>请求


### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI       |
|--------|----------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/insights``` |


### <a name="request-header"></a>请求头

| 标头        | 类型   | 说明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** &lt;*token*&gt;。 |


### <a name="request-parameters"></a>请求参数

| 参数        | 类型   |  说明      |  必需  
|---------------|--------|---------------|------|
| applicationId | 字符串 | 你想要获取的见解数据的桌面应用程序的产品 ID。 要获取桌面应用程序的产品 ID，请打开任意[桌面应用程序的开发人员中心分析报告](https://msdn.microsoft.com/library/windows/desktop/mt826504)（如**运行状况报告**）并从 URL 检索产品 ID。 如果未指定此参数，响应正文将包含注册到帐户的所有应用的见解数据。  |  否  |
| startDate | date | 开始菜单的见解数据日期范围中要检索的日期。 默认值为当前日期之前 30 天。 |  否  |
| endDate | date | 中的结束日期的见解数据日期范围以检索。 默认值为当前日期。 |  否  |
| filter | 字符串  | 在响应中筛选行的一条或多条语句。 每条语句包含的响应正文中的字段名称和值使用 **eq** 或 **ne** 运算符进行关联，并且语句可以使用 **and** 或 **or** 进行组合。 *filter* 参数中的字符串值必须使用单引号括起来。 例如，*筛选器 = dataType eq 购置*。 <p/><p/>当前此方法仅支持筛选器**运行状况**。  | 否   |

### <a name="request-example"></a>请求示例

以下示例演示了一个请求用于获取的见解数据。 *ApplicationId*值替换为桌面应用程序的相应值。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/insights?applicationId=10238467886765136388&startDate=6/1/2018&endDate=6/15/2018&filter=dataType eq 'health' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

### <a name="response-body"></a>响应正文

| 值      | 类型   | 说明                  |
|------------|--------|-------------------------------------------------------|
| 值      | array  | 包含应用的见解数据的对象数组。 有关每个对象中的数据的详细信息，请参阅下面的[相关的见解值](#insight-values)部分。                                                                                                                      |
| TotalCount | int    | 查询的数据结果中的行总数。                 |


### <a name="insight-values"></a>相关的见解值

*Value* 数组中的元素包含以下值。

| 值               | 类型   | 描述                           |
|---------------------|--------|-------------------------------------------|
| applicationId       | 字符串 | 要为其检索见解数据的桌面应用程序的产品 ID。     |
| insightDate                | 字符串 | 我们标识特定指标的更改的日期。 此日期表示一周中，我们检测到了显著增加结束或减少的指标，与之前的周进行比较。 |
| 数据类型     | 字符串 | 指定此相关的见解通知的常规分析区域的字符串。 目前，此方法仅支持**运行状况**。    |
| insightDetail          | array | 一个或多个[InsightDetail 值](#insightdetail-values)表示当前相关的见解的详细信息。    |


### <a name="insightdetail-values"></a>InsightDetail 值

| 值               | 类型   | 说明                           |
|---------------------|--------|-------------------------------------------|
| FactName           | 字符串 | 一个字符串，指示的当前相关的见解和当前维度描述的指标。 目前，此方法仅支持值**点击次数**。  |
| SubDimensions         | array |  介绍相关的见解的单个跃点数的一个或多个对象。   |
| PercentChange            | 字符串 |  指标跨整个客户群的销售量更改百分比。  |
| 具有           | 字符串 |  在当前的维度中所述的指标的名称。 示例包括**事件类型**、**市场**、 **DeviceType**，以及**PackageVersion**。   |
| DimensionValue              | 字符串 | 在当前的维度中所述的指标值。 例如，如果**具有****事件类型**， **DimensionValue**可能**崩溃**或**挂起**。   |
| FactValue     | 字符串 | 相关的见解的检测的日期指标的绝对值。  |
| Direction | 字符串 |  更改 （**正**或**负**） 的方向。   |
| 日期              | 字符串 |  我们确定与当前的见解或当前维度相关的更改的日期。   |

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

* [Windows 桌面应用程序计划](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
* [运行状况报告](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program#health-report)
* [使用 Microsoft Store 服务访问分析数据](access-analytics-data-using-windows-store-services.md)
