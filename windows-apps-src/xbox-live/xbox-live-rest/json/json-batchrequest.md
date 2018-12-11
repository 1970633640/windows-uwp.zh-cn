---
title: BatchRequest (JSON)
assetID: 2ca34506-8801-efc5-7c83-3c9ec5572276
permalink: en-us/docs/xboxlive/rest/json-batchrequest.html
description: " BatchRequest (JSON)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 51073c71700613edcd7c22e18cc0c00a9222d7e5
ms.sourcegitcommit: 8921a9cc0dd3e5665345ae8eca7ab7aeb83ccc6f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "8891515"
---
# <a name="batchrequest-json"></a>BatchRequest (JSON)
用来筛选状态信息，如用户、 设备和标题属性的数组。
<a id="ID4EN"></a>


## <a name="batchrequest"></a>BatchRequest

BatchRequest 对象具有以下规范。

| 成员| 类型| 描述|
| --- | --- | --- |
| 用户| 字符串的数组| 用户想要了解，最多个一次 1100 Xuid 其状态的列表 XUIDs。|
| deviceTypes| 字符串的数组| 使用你想要了解有关用户的设备类型的列表。 如果该数组留空，则默认为所有可能的设备类型 （即，不会被筛选掉）。|
| 主题作品| 32 位无符号整数的数组| 设备的列表类型你想要了解有关其的用户。 如果该数组留空，则默认为所有可能的游戏 （即，不会被筛选掉）。|
| level| 字符串| 可能值： <ul><li>用户-获取用户节点</li><li>设备-获取用户和设备节点</li><li>游戏-获取基本标题级别信息</li><li>所有-获取完整状态信息和媒体信息</li></ul>默认值为"标题"。| 
| onlineOnly| 布尔值| 如果此属性为 true，批处理操作会筛选掉记录脱机用户 （包括遮盖的）。 如果未提供，则将返回在线和离线用户。|

<a id="ID4EAD"></a>


## <a name="sample-json-syntax"></a>JSON 语法示例


```json
{
  users:
  [
    "1234567890",
    "4567890123",
    "7890123456"
  ]
}


```


<a id="ID4EJD"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4ELD"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)


<a id="ID4EXD"></a>


##### <a name="reference"></a>参考   
