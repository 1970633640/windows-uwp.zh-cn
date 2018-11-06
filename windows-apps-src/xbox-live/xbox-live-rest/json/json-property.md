---
title: Property (JSON)
assetID: 93de547e-d936-6fcc-92cb-e4dd284dd609
permalink: en-us/docs/xboxlive/rest/json-property.html
author: KevinAsgari
description: " Property (JSON)"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: d37054d03f6ebe8299db78673dc631c9b4b4bc16
ms.sourcegitcommit: e814a13978f33654d8e995584f4b047cb53e0aef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "6049106"
---
# <a name="property-json"></a>Property (JSON)
包含匹配请求条件为提供的客户端的属性数据。
<a id="ID4EN"></a>


## <a name="property"></a>属性

属性对象具有以下规范。

| 成员| 类型| 描述|
| --- | --- | --- |
| id| 字符串| 此属性的 id。|
| type| 32 位有符号整数 | 该属性的类型。 支持的值包括： <ul><li>0 = 整型</li><li>1 = string</li></ul>| 
| 值| 字符串| 此属性的值。|

<a id="ID4EGC"></a>


## <a name="sample-json-syntax"></a>JSON 语法示例


```json
{
    "id":"1",
    "value":"20",
    "type":0
}

```


<a id="ID4EPC"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4ERC"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)
