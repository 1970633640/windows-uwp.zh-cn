---
description: 在 Microsoft Store 分析 API 中使用此方法以获取详细的数据的特定错误 Xbox One 游戏。
title: 获取 Xbox One 游戏内错误的详细信息
ms.date: 11/06/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 服务, Microsoft Store 分析 API, 错误, 详细信息
ms.localizationpriority: medium
ms.openlocfilehash: da3252c42a0c2e2bd02465985737125cc053a616
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57589962"
---
# <a name="get-details-for-an-error-in-your-xbox-one-game"></a>获取 Xbox One 游戏内错误的详细信息

在 Microsoft Store analytics API 以获取详细的数据的特定错误 Xbox One 游戏引入通过 Xbox 开发人员门户 (XDP) 和 XDP 分析合作伙伴中心仪表板中提供了使用此方法。 此方法仅可以检索过去 30 天内发生的错误的详细信息。

可以使用此方法之前，必须先使用[收到错误报告数据为你的 Xbox One 游戏](get-error-reporting-data-for-your-xbox-one-game.md)方法来检索你想要获取详细的信息的错误的 ID。

## <a name="prerequisites"></a>必备条件


若要使用此方法，首先需要执行以下操作：

* 完成 Microsoft Store 分析 API 的所有[先决条件](access-analytics-data-using-windows-store-services.md#prerequisites)（如果尚未这样做）。
* [获取 Azure AD 访问令牌](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。
* 获取希望获取详细信息的错误的 ID。 若要获取此 ID，请使用[收到错误报告数据为你的 Xbox One 游戏](get-error-reporting-data-for-your-xbox-one-game.md)方法，并使用**failureHash**该方法的响应正文中的值。

## <a name="request"></a>请求


### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/failuredetails``` |


### <a name="request-header"></a>请求头

| 标头        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** *token*&lt;&gt;。 |


### <a name="request-parameters"></a>请求参数

| 参数        | 在任务栏的搜索框中键入   |  描述      |  必需  
|---------------|--------|---------------|------|
| applicationId | 字符串 | **Store ID**的 Xbox One 的游戏为其检索错误详细信息。 **Store ID**可在合作伙伴中心中的应用标识页上。 举例**Store ID**是 9WZDNCRFJ3Q8。 |  是  |
| failureHash | 字符串 | 你希望获取详细信息的错误的唯一 ID。 若要获取此值感兴趣的错误，请使用[收到错误报告数据为你的 Xbox One 游戏](get-error-reporting-data-for-your-xbox-one-game.md)方法，并使用**failureHash**该方法的响应正文中的值。 |  是  |
| startDate | 日期 | 要检索的详细错误数据日期范围中的开始日期。 默认值为当前日期之前 30 天。 |  否  |
| endDate | 日期 | 要检索的详细错误数据日期范围中的结束日期。 默认值为当前日期。 |  否  |
| top | int | 要在请求中返回的数据行数。 如果未指定，最大值和默认值为 10000。 当查询中存在多行数据时，响应正文中包含的下一个链接可用于请求下一页数据。 |  否  |
| skip | int | 要在查询中跳过的行数。 使用此参数可以浏览较大的数据集。 例如，top=10 和 skip=0，将检索前 10 行数据；top=10 和 skip=10，将检索之后的 10 行数据，依此类推。 |  否  |
| filter |字符串  | 在响应中筛选行的一条或多条语句。 每条语句包含的响应正文中的字段名称和值使用 **eq** 或 **ne** 运算符进行关联，并且语句可以使用 **and** 或 **or** 进行组合。 *filter* 参数中的字符串值必须使用单引号括起来。 你可以指定响应正文中的以下字段：<p/><ul><li><strong>market</strong></li><li><strong>date</strong></li><li><strong>cabId</strong></li><li><strong>cabExpirationTime</strong></li><li><strong>deviceType</strong></li><li><strong>deviceModel</strong></li><li><strong>osVersion</strong></li><li><strong>osRelease</strong></li><li><strong>packageVersion</strong></li><li><strong>osBuild</strong></li></ul> | 否   |
| orderby | 字符串 | 对结果数据值进行排序的语句。 语法是 <em>orderby=field [order],field [order],...</em>。<em>field</em> 参数可以是以下字符串之一。<ul><li><strong>market</strong></li><li><strong>date</strong></li><li><strong>cabId</strong></li><li><strong>cabExpirationTime</strong></li><li><strong>deviceType</strong></li><li><strong>deviceModel</strong></li><li><strong>osVersion</strong></li><li><strong>osRelease</strong></li><li><strong>packageVersion</strong></li><li><strong>osBuild</strong></li></ul><p><em>order</em> 参数是可选的，可以是 <strong>asc</strong> 或 <strong>desc</strong>，用于指定每个字段的升序或降序排列。 默认值为 <strong>asc</strong>。</p><p>下面是一个 <em>orderby</em> 字符串的示例：<em>orderby=date,market</em></p> |  否  |


### <a name="request-example"></a>请求示例

下面的示例演示多个请求的适用于 Xbox One 游戏中获取详细的错误数据。 替换*applicationId*值替换**Store ID**为您的游戏。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/failuredetails?applicationId=BRRT4NJ9B3D1&failureHash=012e33e3-dbc9-b12f-c124-9d9810f05d8b&startDate=2016-11-05&endDate=2016-11-06&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>

GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/failuredetails?applicationId=BRRT4NJ9B3D1&failureHash=012e33e3-dbc9-b12f-c124-9d9810f05d8b&startDate=2016-11-05&endDate=2016-11-06&top=10&skip=0&filter=market eq 'US' and deviceType eq 'Windows.Desktop' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应


### <a name="response-body"></a>响应正文

| 值      | 在任务栏的搜索框中键入    | 描述    |
|------------|---------|------------|
| 值      | 数组   | 包含详细错误数据的对象数组。 有关每个对象中的数据的详细信息，请参阅以下[错误详细信息值](#error-detail-values)部分。          |
| @nextLink  | 字符串  | 如果存在数据的其他页，此字符串中包含的 URI 可用于请求下一页数据。 例如，当请求的 **top** 参数设置为 10，但查询的错误超过 10 行时，就会返回此值。 |
| TotalCount | 整数 | 查询的数据结果中的行总数。        |


<span id="error-detail-values"/>

### <a name="error-detail-values"></a>错误详细信息值

*Value* 数组中的元素包含以下值。

| 值           | 在任务栏的搜索框中键入    | 描述     |
|-----------------|---------|----------------------------|
| applicationId   | 字符串  | **Store ID**的 Xbox One 游戏为其检索详细的错误数据。      |
| failureHash     | 字符串  | 错误的唯一标识符。     |
| failureName     | 字符串  | 故障的名称，它由四个部分组成：一个或多个问题类、异常/错误检查代码、发生故障的映像的名称和相关的函数名称。           |
| 日期            | 字符串  | 错误数据的日期范围内的第一个日期。 如果请求指定了某一天，此值就是该日期。 如果请求指定了一周、月或其他日期范围，此值是该日期范围内的第一个日期。 |
| cabId           | 字符串  | 与此错误相关联的 CAB 文件的唯一 ID。   |
| cabExpirationTime  | 字符串  | CAB 文件已过期且不能再下载时的日期和时间，以 ISO 8601 格式表示。   |
| market          | 字符串  | 设备市场的 ISO 3166 国家/地区代码。     |
| osBuild         | 字符串  | 发生错误的操作系统的版本号。       |
| packageVersion  | 字符串  | 游戏与此错误关联的包的版本。    |
| deviceModel           | 字符串  | 指定在其发生错误时运行该游戏在 Xbox One 控制台的以下字符串之一。<p/><ul><li><strong>Microsoft-Xbox One</strong></li><li><strong>Microsoft-Xbox One S</strong></li><li><strong>Microsoft-Xbox One X</strong></li></ul>  |
| osVersion       | 字符串  | 出现错误的操作系统版本。 这始终是值**Windows 10**。    |
| osRelease       | 字符串  |  Windows 10 OS 版本或试验环指定 （作为 OS 版本中 subpopulation) 发生了错误的以下字符串之一。<p/><ul><li><strong>版本 1507</strong></li><li><strong>版本 1511</strong></li><li><strong>版本 1607</strong></li><li><strong>版本 1703</strong></li><li><strong>版本 1709</strong></li><li><strong>1803 的版本</strong></li><li><strong>发布预览</strong></li><li><strong>深入了解快速</strong></li><li><strong>深入了解速度缓慢</strong></li></ul><p>如果操作系统版本或外部测试 Ring 未知，则此字段的值为 <strong>Unknown</strong>。</p>    |
| deviceType      | 字符串  | 出现错误的设备的类型。 这始终是值**控制台**。     |
| cabDownloadable           | 布尔  | 指示是否可为此用户下载 CAB 文件。   |


### <a name="response-example"></a>响应示例

以下示例举例说明此请求的 JSON 响应正文。

```json
{
  "Value": [
    {
      "applicationId": "BRRT4NJ9B3D1",
      "failureHash": "012345-5dbc9-b12f-c124-9d9810f05d8b",
      "failureName": "STOWED_EXCEPTION_System.UriFormatException_exe!ContosoSports.GroupedItems+_ItemView_ItemClick_d__9.MoveNext",
      "date": "2018-02-05 09:11:25",
      "cabId": "133637331323",
      "cabExpirationTime": "2016-12-05 09:11:25",
      "market": "US",
      "osBuild": "10.0.17134",
      "packageVersion": "1.0.2.6",
      "deviceModel": "Microsoft-Xbox One",
      "osVersion": "Windows 10",
      "osRelease": "Version 1803",
      "deviceType": "Console",
      "cabDownloadable": false
    }
  ],
  "@nextLink": null,
  "TotalCount": 1
}
```

## <a name="related-topics"></a>相关主题

* [使用 Microsoft Store 服务的访问分析数据](access-analytics-data-using-windows-store-services.md)
* [获取错误报告数据为你的 Xbox One 游戏](get-error-reporting-data-for-your-xbox-one-game.md)
* [获取游戏中你的 Xbox One 的错误的堆栈跟踪](get-the-stack-trace-for-an-error-in-your-xbox-one-game.md)
* [下载您的 Xbox One 游戏中的错误的 CAB 文件](download-the-cab-file-for-an-error-in-your-xbox-one-game.md)
