---
title: 编码和解码数据
description: 此示例代码显示了如何在通用 Windows 平台 (UWP) 应用中对 Base64 和十六进制数据进行编码和解码。
ms.assetid: 2CC23863-E840-48F4-B087-0479045743AC
author: msatranjr
ms.author: misatran
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10，uwp 安全
ms.localizationpriority: medium
ms.openlocfilehash: 76c43f5b72b47c9ce88a0ee12223ff099127ff8f
ms.sourcegitcommit: ca96031debe1e76d4501621a7680079244ef1c60
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2018
ms.locfileid: "5811944"
---
# <a name="encode-and-decode-data"></a>编码和解码数据



此示例代码显示了如何在通用 Windows 平台 (UWP) 应用中对 Base64 和十六进制数据进行编码和解码。

```cs
public void EncodeDecodeBase64()
{
    // Define a Base64 encoded string.
    String strBase64 = "uiwyeroiugfyqcajkds897945234==";

    // Decoded the string from Base64 to binary.
    IBuffer buffer = CryptographicBuffer.DecodeFromBase64String(strBase64);

    // Encode the buffer back into a Base64 string.
    String strBase64New = CryptographicBuffer.EncodeToBase64String(buffer);
}

public void EncodeDecodeHex()
{
    // Define a hexadecimal string.
    String strHex = "30310AFF";

    // Decode a hexadecimal string to binary.
    IBuffer buffer = CryptographicBuffer.DecodeFromHexString(strHex);

    // Encode the buffer back into a hexadecimal string.
    String strHexNew = CryptographicBuffer.EncodeToHexString(buffer);
}
```
