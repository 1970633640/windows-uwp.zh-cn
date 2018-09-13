---
title: 属性 (JSON)
assetID: 93de547e-d936-6fcc-92cb-e4dd284dd609
permalink: en-us/docs/xboxlive/rest/json-property.html
author: KevinAsgari
description: " 属性 (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 033a87580680b054f5eefec7c543215e4351ace3
ms.sourcegitcommit: c8f6866100a4b38fdda8394ea185b02d7af66411
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2018
ms.locfileid: "3957996"
---
# <a name="property-json"></a>属性 (JSON)
包含匹配请求条件为提供的客户端的属性数据。
<a id="ID4EN"></a>


## <a name="property"></a>属性

属性对象具有以下规范。

| 成员| 类型| 描述|
| --- | --- | --- |
| id| 字符串| 此属性 id。|
| type| 32 位有符号的整数 | 该属性的类型。 支持的值包括： <ul><li>0 = 整型</li><li>1 = string</li></ul>| 
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

[JavaScript 对象表示法 (JSON) 对象引用](atoc-xboxlivews-reference-json.md)
