---
title: 标题存储 URI
assetID: 32bba1e4-0980-785e-c098-a96cd88a8e5f
permalink: en-us/docs/xboxlive/rest/atoc-reference-storagev2.html
author: KevinAsgari
description: " 标题存储 URI"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: e642974c22306d6f9c66d6254f2a32afe2c70a4e
ms.sourcegitcommit: 6cc275f2151f78db40c11ace381ee2d35f0155f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "5563561"
---
# <a name="title-storage-uris"></a>标题存储 URI
 
本部分提供了从*标题存储*的 Xbox Live 服务的统一资源标识符 (URI) 地址和关联的超文本传输协议 (HTTP) 方法的详细信息。
 
所有平台上运行的游戏均可使用此服务。
 
这些 Uri 的域是 titlestorage.xboxlive.com。
 
<a id="ID4EFB"></a>

 
## <a name="in-this-section"></a>本部分内容

[/global/scids/{scid}](uri-globalscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/global/scids/{scid}/data/{path}](uri-globalscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/global/scids/{scid}/data/{pathAndFileName},{type}](uri-globalscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载文件。

[/json/users/batch/scids/{scid}/data/{pathAndFileName},json](uri-jsonusersbatchscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;从多个用户具有相同的文件名下载多个文件。

[/json/users/xuid({xuid})/scids/{scid}](uri-jsonusersxuidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/json/users/xuid({xuid})/scids/{scid}/data/{path}](uri-jsonusersxuidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json](uri-jsonusersxuidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载、 上传，或删除某个文件。

[/sessions/{sessionId}/scids/{scid}](uri-sessionssessionidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/sessions/{sessionId}/scids/{scid}/data/{path}](uri-sessionssessionidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/sessions/{sessionId}/scids/{scid}/data/{pathAndFileName},{type}](uri-sessionssessionidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载文件。

[/trustedplatform/users/batch/scids/{scid}/data/{pathAndFileName},{type}](uri-trustedplatformusersbatchscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;从多个用户具有相同的文件名下载多个文件。

[/trustedplatform/users/xuid({xuid})/scids/{scid}](uri-trustedplatformusersxuidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/trustedplatform/users/xuid({xuid})/scids/{scid}/data/{path}](uri-trustedplatformusersxuidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/trustedplatform/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},{type}](uri-trustedplatformusersxuidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载、 上传，或删除某个文件。

[/untrustedplatform/users/batch/scids/{scid}/data/{pathAndFileName},{type}](uri-untrustedplatformusersbatchscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;从多个用户具有相同的文件名下载多个文件。

[/untrustedplatform/users/xuid({xuid})/scids/{scid}](uri-untrustedplatformusersxuidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/untrustedplatform/users/xuid({xuid})/scids/{scid}/data/{path}](uri-untrustedplatformusersxuidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/untrustedplatform/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},{type}](uri-untrustedplatformusersxuidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载、 上传，或删除某个文件。
 
<a id="ID4E5C"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EAD"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[统一资源标识符 (URI) 参考](../atoc-xboxlivews-reference-uris.md)

   