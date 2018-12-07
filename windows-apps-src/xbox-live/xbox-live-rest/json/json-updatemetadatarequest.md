---
title: UpdateMetadataRequest (JSON)
assetID: 0bc210e3-c1dc-9267-e322-aadb9f0a074a
permalink: en-us/docs/xboxlive/rest/json-updatemetadatarequest.html
description: " UpdateMetadataRequest (JSON)"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: a76e4b12e0ffadb112913775b500ac0d39d413d5
ms.sourcegitcommit: d7613c791107f74b6a3dc12a372d9de916c0454b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2018
ms.locfileid: "8740838"
---
# <a name="updatemetadatarequest-json"></a>UpdateMetadataRequest (JSON)
应更新剪辑元数据。 
<a id="ID4EN"></a>

 
## <a name="updatemetadatarequest"></a>UpdateMetadataRequest
 
UpdateMetadataRequest 对象具有以下规范。
 
| 成员| 类型| 描述| 
| --- | --- | --- | 
| userCaption| 字符串| 更改游戏剪辑的用户输入非本地化字符串。| 
| 可见性| [GameClipVisibility 枚举](../enums/gvr-enum-gameclipvisibility.md)| 更改游戏剪辑的可见性，因为它在系统中发布。| 
| titleData| 字符串| 特定于游戏的属性包中。 最大大小： 10 KB。| 
  
<a id="ID4EBC"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 
更改用户剪辑名称和可见性：
 

```json
{
  "userCaption": "I've changed this 100 Times!",
  "visibility": "Owner"
}

```

 
更改只是游戏属性 （这只是一个示例，由于此字段的架构是由调用方负责）：
 

```json
{
  "titleData": "{ 'Id': '123456', 'Location': 'C:\\videos\\123456.mp4' }"
}

```

  
<a id="ID4EQC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ESC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

  
<a id="ID4E3C"></a>

 
##### <a name="reference"></a>参考 

[POST (/users/me/scids/{scid}/clips/{gameClipId})](../uri/dvr/uri-usersmescidclipsgameclipidpost.md)

   