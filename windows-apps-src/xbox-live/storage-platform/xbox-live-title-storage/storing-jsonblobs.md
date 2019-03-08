---
title: 存储 JSON blob
description: 了解如何在 Xbox Live 标题存储中存储 JSON blob。
ms.assetid: f424aca1-e671-4e31-84c6-098fda4a9558
ms.date: 04/04/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one, 标题存储
ms.localizationpriority: medium
ms.openlocfilehash: dabcd0634bb20bc6b82ae302c77338b5bb726a63
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57595062"
---
# <a name="storing-a-json-blob-in-xbox-live-title-storage"></a>在 Xbox Live 标题存储中存储 JSON blob

1.  使用 *PUT* 方法发送请求，以向标题存储发送数据。

        PUT https://titlestorage.xboxlive.com/json/users/xuid(1245111)/scids/{scid}/data/{pathAndFileName},json
        Content-Type: application/octet-stream
        x-xbl-contract-version: 1
        Authorization: XBL3.0 x=<userHash>;<STSTokenString>
        Content-Length: 240
        Connection: Keep-Alive



-   用户必须在会话中才能更新。

-   STSTokenString 是为简便起见使用的占位符，应该将其替换为由身份验证请求返回的令牌。

2.  发送 JSON 对象。

        {
            "startlevel":"1",
            "expression":"smile"
        }

#### <a name="reference"></a>参考

**/json/users/xuid({xuid})/scids/{scid}/data/{pathAndFileName},json)**
