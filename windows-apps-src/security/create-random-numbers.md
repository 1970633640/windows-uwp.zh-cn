---
title: 创建随机数
description: 此示例代码显示了如何在通用 Windows 平台 (UWP) 应用中创建随机数或在加密中使用的缓冲区。
ms.assetid: 15746824-F93A-4DC7-836E-EBA916D2CFD3
author: msatranjr
ms.author: misatran
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp 安全
ms.localizationpriority: medium
ms.openlocfilehash: 595b4ab47e3c6c833a4b8f2e692a0cc0c8ffcaa4
ms.sourcegitcommit: 7aa1933e6970f878faf50d59e1f799b90afd7cc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2018
ms.locfileid: "3376103"
---
# <a name="create-random-numbers"></a>创建随机数



此示例代码显示了如何在通用 Windows 平台 (UWP) 应用中创建随机数或在加密中使用的缓冲区。

```cs
public string GenerateRandomData()
{
    // Define the length, in bytes, of the buffer.
    uint length = 32;

    // Generate random data and copy it to a buffer.
    IBuffer buffer = CryptographicBuffer.GenerateRandom(length);

    // Encode the buffer to a hexadecimal string (for display).
    string randomHex = CryptographicBuffer.EncodeToHexString(buffer);

    return randomHex;
}

public uint GenerateRandomNumber()
{
    // Generate a random number.
    uint random = CryptographicBuffer.GenerateRandomNumber();
    return random;
}
```