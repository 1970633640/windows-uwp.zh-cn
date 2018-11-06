---
title: /sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type}
assetID: f5e91763-0704-8526-77d4-c55dfec3b5a5
permalink: en-us/docs/xboxlive/rest/uri-sessionssessionidscidssciddatapathandfilenametype.html
author: KevinAsgari
description: " /sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type}"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: d2c2c592e6bfd1eca029378dda230b2fa72ee5c0
ms.sourcegitcommit: e814a13978f33654d8e995584f4b047cb53e0aef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "6026639"
---
# <a name="sessionssessionidscidssciddatapathandfilenametype"></a>/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type}
下载文件。 这些 Uri 的域是`titlestorage.xboxlive.com`。
 
  * [URI 参数](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| sessionId| 字符串| 若要查找会话的 ID。| 
| scid| guid| 若要查找的服务配置 ID。| 
| pathAndFileName| 字符串| 要访问的项的路径和文件名。 有效的字符 （至当前阶段并包括最终正斜杠） 的路径部分包括 (A-Z) 的大写字母、 小写字母 (a-z)、 数字 (0-9)、 下划线 (_)，并且正斜杠 （/）。路径部分可能为空。有效的字符 （最终正斜杠后的所有内容） 的文件名称部分包括 (A-Z) 的大写字母、 小写字母 (a-z)、 数字 (0-9) 下划线 (_)，句点 （.） 和连字符 （-）。 文件名称不能为空，以句号结尾或包含两个连续句点。| 
| type| 字符串| 数据的格式。 可能的值为二进制文件或 json。| 
  
<a id="ID4EOC"></a>

 
## <a name="valid-methods"></a>有效的方法

[DELETE (/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type})](uri-sessionssessionidscidssciddatapathandfilenametype-delete.md)

&nbsp;&nbsp;删除文件。 

[GET (/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type})](uri-sessionssessionidscidssciddatapathandfilenametype-get.md)

&nbsp;&nbsp;下载文件。

[PUT (/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type})](uri-sessionssessionidscidssciddatapathandfilenametype-put.md)

&nbsp;&nbsp;将文件上传。 可在其中的数据和元数据发送一条消息，或在其中的数据和元数据发送一系列的较小的块多块上载的完整上载上传数据。 可以为一条消息发送小于 4 兆字节的文件。 数据类型 json 不支持多块上载。 
 
<a id="ID4E5C"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EAD"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[标题存储 URI](atoc-reference-storagev2.md)

   