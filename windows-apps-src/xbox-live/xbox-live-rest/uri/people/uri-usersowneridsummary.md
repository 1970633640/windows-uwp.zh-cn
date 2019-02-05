---
title: /users/{ownerId}/summary
assetID: 63f8ed09-532d-381e-59e6-2849893df5bf
permalink: en-us/docs/xboxlive/rest/uri-usersowneridsummary.html
description: " /users/{ownerId}/summary"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: f8ad32fb2033c97a408ccb0f6cc6871b01caf5c5
ms.sourcegitcommit: b975c8fc8cf0770dd73d8749733ae5636f2ee296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "9058488"
---
# <a name="usersowneridsummary"></a>/users/{ownerId}/summary
有关从调用方的角度来看所有者访问摘要数据。

  * [URI 参数](#ID4EQ)

<a id="ID4EQ"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 说明|
| --- | --- | --- |
| ownerId| 字符串| 正在访问其资源的用户的标识符。 可能的值为"我"、 xuid({xuid}) 或 gt({gamertag})。 示例值： <code>me</code>， <code>xuid(2603643534573581)</code>， <code>gt(SomeGamertag)</code>|

<a id="ID4ESB"></a>


## <a name="valid-methods"></a>有效的方法

[GET (/users/{ownerId}/summary)](uri-usersowneridsummaryget.md)

&nbsp;&nbsp;从调用方的角度来看，获取有关所有者的摘要数据。

<a id="ID4E3B"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4E5B"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/users/{ownerId}/summary](uri-usersowneridsummaryget.md)
