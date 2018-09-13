---
title: / trustedplatform/用户/批次/scid / {scid} /data/ {pathAndFileName} {类型}
assetID: c92d247a-5ea1-7a06-36db-7c67a1dc3151
permalink: en-us/docs/xboxlive/rest/uri-trustedplatformusersbatchscidssciddatapathandfilenametype.html
author: KevinAsgari
description: " / trustedplatform/用户/批次/scid / {scid} /data/ {pathAndFileName} {类型}"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 0278b9a090f648dd2092641efcaa2c7a346d96b1
ms.sourcegitcommit: c8f6866100a4b38fdda8394ea185b02d7af66411
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2018
ms.locfileid: "3959948"
---
# <a name="trustedplatformusersbatchscidssciddatapathandfilenametype"></a>/ trustedplatform/用户/批次/scid / {scid} /data/ {pathAndFileName} {类型}
从多个用户具有相同的文件名下载多个文件。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| scid| guid| 要查找的服务配置 ID。| 
| pathAndFileName| 字符串| 要访问的项的路径和文件名。 有效的字符 （达且包括最终正斜杠） 的路径部分包含大写字母 (A-Z)、 小写字母 (a-z)、 数字 (0-9)，下划线 (_) 和正斜杠 （/）。路径部分可能为空。有效的字符的文件名部分 （最终正斜杠后面的所有内容） 包含大写字母 (A-Z)、 小写字母 (a-z)、 数字 (0-9)，下划线 (_)，句点 （.） 和连字符 （-）。 文件名称不能为空，以句号结尾或包含两个连续句点。| 
| type| 字符串| 数据的格式。 可能的值为二进制文件或 json。| 
  
<a id="ID4EFC"></a>

 
## <a name="valid-methods"></a>有效的方法

[POST](uri-trustedplatformusersbatchscidssciddatapathandfilenametype-post.md)

&nbsp;&nbsp;从多个用户具有相同的文件名下载多个文件。
 
<a id="ID4EPC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ERC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[标题存储 Uri](atoc-reference-storagev2.md)

   