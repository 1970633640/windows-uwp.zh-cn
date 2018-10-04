---
title: UserSettings (JSON)
assetID: 17c030cb-05e0-f78e-5ab1-cdbd8b801ceb
permalink: en-us/docs/xboxlive/rest/json-usersettings.html
author: KevinAsgari
description: " UserSettings (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 20ac62403a8248011928089ea81cdf6418259db1
ms.sourcegitcommit: 5c9a47b135c5f587214675e39c1ac058c0380f4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "4353418"
---
# <a name="usersettings-json"></a>UserSettings (JSON)
返回当前身份验证的用户的设置。 
<a id="ID4EN"></a>

 
## <a name="usersettings"></a>UserSettings
 
UserSettings 对象具有以下规范。
 
| 成员| 类型| 描述| 
| --- | --- | --- | 
| id| 32 位无符号的整数| 设置的标识符。| 
| 源| 32 位无符号的整数| 表示设置的源。 | 
| titleId| 32 位无符号的整数| 标题与设置关联的标识符。 | 
| 值| 8 位无符号整数的数组| 表示设置的值。 客户端检索设置必须了解表示格式能够读取数据。 | 
  
<a id="ID4EJC"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 

```json
{
   "id":268697600,
   "source":1,
   "titleId":1297287259,
   "value":"CAAAAA=="
}
    
```

  
<a id="ID4ESC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EUC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

   