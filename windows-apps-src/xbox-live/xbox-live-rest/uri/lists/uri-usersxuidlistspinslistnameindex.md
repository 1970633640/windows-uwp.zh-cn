---
title: / 用户/xuid (xuid) / 列出/PIN / {listname} / 索引 （{索引}）？ insertIndex = {insertIndex}
assetID: edcb19bd-87a5-732b-0c45-6f7355fc2dd1
permalink: en-us/docs/xboxlive/rest/uri-usersxuidlistspinslistnameindex.html
author: KevinAsgari
description: " / 用户/xuid (xuid) / 列出/PIN / {listname} / 索引 （{索引}）？ insertIndex = {insertIndex}"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: d4b1be4ab591a5bea8d7bc70fb7f7dcb29e4f548
ms.sourcegitcommit: 2a63ee6770413bc35ace09b14f56b60007be7433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3931410"
---
# <a name="usersxuidxuidlistspinslistnameindexindexinsertindexinsertindex"></a>/ 用户/xuid (xuid) / 列出/PIN / {listname} / 索引 （{索引}）？ insertIndex = {insertIndex}
将移动列表中的一项。 这些 Uri 的域是`eplists.xboxlive.com`。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数 
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| XUID| 字符串| 用户的 XUID。| 
| listname| 字符串| 要操作的列表的名称。| 
| 索引| 字符串| 指定要移动的项的当前索引。 零或正整数索引值时，这是指当前索引的项，并调用的请求正文应为空。 但是，如果索引值为"-1"，必须由 ItemId 或提供商/ProviderID 调用，请求正文中指定要移动的项。 | 
  
<a id="ID4EHC"></a>

 
## <a name="valid-methods"></a>有效的方法

[POST](uri-usersxuidlistspinslistnameindexpost.md)

&nbsp;&nbsp;将列表中的项移到列表中的不同位置。
 
<a id="ID4ERC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ETC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[统一资源标识符 (URI) 引用](../atoc-xboxlivews-reference-uris.md)

   