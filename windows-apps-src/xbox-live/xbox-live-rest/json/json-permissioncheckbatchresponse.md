---
title: PermissionCheckBatchResponse (JSON)
assetID: f157ed8d-7483-1b34-bc3d-e3fcf6a7d055
permalink: en-us/docs/xboxlive/rest/json-permissioncheckbatchresponse.html
author: KevinAsgari
description: " PermissionCheckBatchResponse (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 9bc3d574274bdef6d0033e9f5313457706dd509e
ms.sourcegitcommit: d10fb9eb5f75f2d10e1c543a177402b50fe4019e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "4566052"
---
# <a name="permissioncheckbatchresponse-json"></a>PermissionCheckBatchResponse (JSON)
结果的批处理权限检查的多个用户的权限值列表。 
<a id="ID4EN"></a>

 
## <a name="permissioncheckbatchresponse"></a>PermissionCheckBatchResponse
 
PermissionCheckBatchResponse 对象具有以下规范。
 
| 成员| 类型| 描述| 
| --- | --- | --- | 
| Responses| [PermissionCheckBatchUserResponse (JSON)](json-permissioncheckbatchuserresponse.md)的数组| 必需。 原始请求中，如请求中所示的相同顺序要求提供每项权限[PermissionCheckBatchUserResponse (JSON)](json-permissioncheckbatchuserresponse.md)对象。| 
  
<a id="ID4EQB"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 

```json
{
    "responses":
    [
        {
            "user": {"xuid":"12345"},
            "permissions":
            [
                {
                    "isAllowed":true
                },
                {
                    "isAllowed":true
                }
            ]
        },
        {
            "user": {"xuid":"54321"},
            "permissions":
            [
                {
                    "isAllowed":false,
                    "reasons":
                    [
                        {"reason":"NotAllowed"}
                    ]
                },
                {
                    "isAllowed":false,
                    "reasons":
                    [
                        {"reason":"PrivilegeRestrictsTarget", "restrictedSetting":"AllowProfileViewing"}
                    ]
                }
            ]
        }
    ]
}
    
```

  
<a id="ID4EZB"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4E2B"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

   