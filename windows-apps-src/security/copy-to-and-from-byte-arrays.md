---
title: 复制到字节数组并从字节数组复制
description: 此示例代码显示了如何在通用 Windows 平台 (UWP) 应用中复制到字节数组并从字节数组复制。
ms.assetid: C343B08C-1FA1-40FD-8CA5-7FC9B707C5E3
author: msatranjr
ms.author: misatran
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10，uwp 安全
ms.localizationpriority: medium
ms.openlocfilehash: 22ce577f7d70b3750a365462b64181a27e71428e
ms.sourcegitcommit: 6cc275f2151f78db40c11ace381ee2d35f0155f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "5567159"
---
# <a name="copy-to-and-from-byte-arrays"></a>复制到字节数组并从字节数组复制



此示例代码显示了如何在通用 Windows 平台 (UWP) 应用中复制到字节数组并从字节数组复制。

```cs
public void ByteArrayCopy()
{
    // Initialize a byte array.
    byte[] bytes = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    // Create a buffer from the byte array.
    IBuffer buffer = CryptographicBuffer.CreateFromByteArray(bytes);

    // Encode the buffer into a hexadecimal string (for display);
    string hex = CryptographicBuffer.EncodeToHexString(buffer);

    // Copy the buffer back into a new byte array.
    byte[] newByteArray;
    CryptographicBuffer.CopyToByteArray(buffer, out newByteArray);
}
```