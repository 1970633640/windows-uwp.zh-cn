---
title: PermissionCheckResult (JSON)
assetID: 1cf147fa-4ff1-3299-0822-0fc1726d1600
permalink: en-us/docs/xboxlive/rest/json-permissioncheckresult.html
author: KevinAsgari
description: " PermissionCheckResult (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 308301b41b407291ffad74337172c5be8f4d2c59
ms.sourcegitcommit: f5321b525034e2b3af202709e9b942ad5557e193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2018
ms.locfileid: "4022388"
---
# <a name="permissioncheckresult-json"></a>PermissionCheckResult (JSON)
从单个权限设置针对单个目标用户的单个用户检查的结果。 
<a id="ID4EP"></a>

 
## <a name="permissioncheckresult"></a>PermissionCheckResult
 
PermissionCheckResult 对象具有以下规范。
 
| 成员| 类型| 说明| 
| --- | --- | --- | 
| 原因| 字符串| 可选。 一个<b>PermissionResultCode</b>值，指示的权限被拒绝为什么如果<b>IsAllowed</b> false。| 
| restrictedSetting| 字符串| 可选。 如果<b>原因</b>成员<b>PermissionResultCode</b>的值指示请求程序特权检查失败，这指示哪些特权失败。| 
  
<a id="ID4E6B"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 

```json
{
    "reason": "MissingPrivilege",
    "restrictedSetting": "VideoCommunications"
}
    
```

  
<a id="ID4EIC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EKC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

   