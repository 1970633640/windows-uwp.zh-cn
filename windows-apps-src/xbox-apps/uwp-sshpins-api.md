---
author: WilliamsJason
title: 设备门户 SSH Pin 码 API 参考
description: 了解如何以编程方式删除所有受信任的 SSH Pin 码。
ms.localizationpriority: medium
ms.openlocfilehash: 88ba9d3e35650c8c581b9ddb76911636fc18c72e
ms.sourcegitcommit: c104b653601d9b81cfc8bb6032ca434cff8fe9b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2018
ms.locfileid: "1921223"
---
# <a name="ssh-pins-api-reference"></a>SSH Pin 码 API 参考
可以使用此 REST API 删除开发工具包上的所有受信任 SSH Pin 码。

## <a name="remove-trusted-ssh-pins"></a>删除受信任的 SSH Pin 码

**请求**

方法      | 请求 URI
:------     | :-----
删除 | /ext/app/sshpins
<br />
**URI 参数**

- 无

**请求标头**

- 无

**请求正文**   

- 无

**响应**   

- 无 

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
204 | 清除 Pin 码的请求已成功。
4XX | 错误代码
5XX | 错误代码

<br />
**可用设备系列**

* Windows Xbox

