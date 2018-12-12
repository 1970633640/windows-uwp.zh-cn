---
title: VerifyStringResult (JSON)
assetID: 272c688e-179e-c7e9-086b-e76d0d4bcb57
permalink: en-us/docs/xboxlive/rest/json-verifystringresult.html
description: " VerifyStringResult (JSON)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: b01793222be80efccdca1f24f5226a2e9ff78064
ms.sourcegitcommit: 49d58bc66c1c9f2a4f81473bcb25af79e2b1088d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "8927423"
---
# <a name="verifystringresult-json"></a>VerifyStringResult (JSON)
结果代码对应于提交到[/system/strings/validate](../uri/stringserver/uri-systemstringsvalidate.md)每个字符串。
<a id="ID4ER"></a>


## <a name="verifystringresult"></a>VerifyStringResult

VerifyStringResult 对象具有以下规范。

| 成员| 类型| 描述|
| --- | --- | --- |
| resultCode| 32 位无符号的整数| 必需。 HResult 代码对应于提交字符串。|
| offendingString| 字符串| 必需。 字符串值，导致被拒绝的字符串。|

<a id="ID4EXB"></a>


## <a name="sample-json-syntax"></a>JSON 语法示例


```json
{
    "verifyStringResult":
    [
        {"resultCode": "1", "offendingString": "badword"},
        {"resultCode": "0", "offendingString": ""},
        {"resultCode": "0", "offendingString": ""},
        {"resultCode": "0", "offendingString": ""},
    ]
}

```


#### <a name="common-hresult-values"></a>常见的 HResult 值

| 值| 错误名称|
| --- | --- | --- | --- | --- |
| 0| 成功|
| 1| 具有冒犯性字符串|
| 2| 过长的字符串|
| 3| 未知的错误|

<a id="ID4ELD"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4END"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)


<a id="ID4EXD"></a>


##### <a name="reference"></a>参考

[POST (/system/strings/validate)](../uri/stringserver/uri-systemstringsvalidatepost.md)
