---
title: 标题存储 Uri
assetID: 32bba1e4-0980-785e-c098-a96cd88a8e5f
permalink: en-us/docs/xboxlive/rest/atoc-reference-storagev2.html
author: KevinAsgari
description: " 标题存储 Uri"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 5a188c3406ad0ca3bfca78d6b45c548c72bf791e
ms.sourcegitcommit: 2a63ee6770413bc35ace09b14f56b60007be7433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3931294"
---
# <a name="title-storage-uris"></a>标题存储 Uri
 
本部分提供了从 Xbox Live*标题*存储服务的统一资源标识符 (URI) 地址和关联的超文本传输协议 (HTTP) 方法的详细信息。
 
所有平台上运行的游戏均可使用此服务。
 
这些 Uri 的域是 titlestorage.xboxlive.com。
 
<a id="ID4EFB"></a>

 
## <a name="in-this-section"></a>本部分内容

[/ 全局/scid / {scid}](uri-globalscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/ 全局 /data//scid / {scid} {路径}](uri-globalscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/global/scids/{scid}/data/{pathAndFileName},{type}](uri-globalscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载文件。

[/ json/用户/批次/scid / {scid} /data/ {pathAndFileName} json](uri-jsonusersbatchscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;从多个用户具有相同的文件名下载多个文件。

[/json/users/xuid({xuid}) /scids/ {scid}](uri-jsonusersxuidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/json/users/xuid({xuid}) /scids/ {scid} /data/ {路径}](uri-jsonusersxuidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/json/users/xuid({xuid}) /scids/ {scid} /data/ {pathAndFileName} json](uri-jsonusersxuidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载、 上传，或删除的文件。

[/sessions/ {sessionId} /scids/ {scid}](uri-sessionssessionidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/sessions/ {sessionId} {scid} /scids/ /data/ {路径}](uri-sessionssessionidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/sessions/ {sessionId} {scid} /scids/ /data/ {pathAndFileName} {类型}](uri-sessionssessionidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载文件。

[/ trustedplatform/用户/批次/scid / {scid} /data/ {pathAndFileName} {类型}](uri-trustedplatformusersbatchscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;从多个用户具有相同的文件名下载多个文件。

[/trustedplatform/users/xuid({xuid}) /scids/ {scid}](uri-trustedplatformusersxuidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/trustedplatform/users/xuid({xuid}) /scids/ {scid} /data/ {路径}](uri-trustedplatformusersxuidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/trustedplatform/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},{type}](uri-trustedplatformusersxuidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载、 上传，或删除的文件。

[/ untrustedplatform/用户/批次/scid / {scid} /data/ {pathAndFileName} {类型}](uri-untrustedplatformusersbatchscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;从多个用户具有相同的文件名下载多个文件。

[/untrustedplatform/users/xuid({xuid}) /scids/ {scid}](uri-untrustedplatformusersxuidscidsscid.md)

&nbsp;&nbsp;检索此存储类型的配额信息。

[/untrustedplatform/users/xuid({xuid}) /scids/ {scid} /data/ {路径}](uri-untrustedplatformusersxuidscidssciddatapath.md)

&nbsp;&nbsp;列出了在指定路径的文件信息。 

[/untrustedplatform/users/xuid({xuid}) /scids/ {scid} /data/ {pathAndFileName} {类型}](uri-untrustedplatformusersxuidscidssciddatapathandfilenametype.md)

&nbsp;&nbsp;下载、 上传，或删除的文件。
 
<a id="ID4E5C"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EAD"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[统一资源标识符 (URI) 引用](../atoc-xboxlivews-reference-uris.md)

   