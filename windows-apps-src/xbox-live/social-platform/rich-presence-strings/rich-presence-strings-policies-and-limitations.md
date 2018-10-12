---
title: “完整状态”策略和限制
author: KevinAsgari
description: 了解 Xbox Live“完整状态”系统的策略和限制。
ms.assetid: 0ad21a75-0524-45a8-8d8a-0dec0f7d6d6f
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one, 完整状态, 策略
ms.localizationpriority: medium
ms.openlocfilehash: 02c5a39dadd50326b7008d73ff6f47e1b4faeb7b
ms.sourcegitcommit: d10fb9eb5f75f2d10e1c543a177402b50fe4019e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "4563542"
---
# <a name="rich-presence-policies-and-limitations"></a>“完整状态”策略和限制

在实现游戏的“完整状态”时，必须遵守以下策略和限制。

-   每个标题必须至少有 1 个字符串集，但没有数量上限。
-   你必须为每个枚举和每个“完整状态”字符串定义默认字符串以及特定区域性字符串。
-   你可以使用数字或字符串统计信息来填充你字符串中的参数。 你不能使用 DateTime 统计信息。
-   如果你为“完整状态”字符串使用统计信息，那么这些统计信息（包括统计信息的任何枚举）还必须在同一个 SCID 和沙盒中提供。
-   你有一个总计包含 44 个字符的行（包括参数值）。 这与 Xbox 360“完整状态”的限制类似。 我们将对客户端进行探索，看看是否可以增加该字符串的长度。 如果字符串可以更长，我们将发布结果。
    -   需要 Unicode 字符，且这些字符必须能够与 UTF-8 编码结合使用来支持显示。
-   你的友好名称必须遵循以下规则：
    -   允许的字符有 'A' 到 'Z'、'a' 到 'z'、下划线 ('\_')、'0' 到 '9'。

        没有字符限制。

-   你的字符串没有完成字符串验证；你必须执行所有字符串验证，如拼写检查、验证字符串是否已正确本地化。
    -   如果我们认为字符串集不适宜（如侮辱性或冒犯性语言），Microsoft 将阻止标题使用“完整状态”，直到字符串更新为我们满意的状态。
-   如果你的标题未与数据平台集成，你的字符串中则没有将统计信息用作参数的选项。
    -   在这种情况下，所有字符串必须完全预定义（不允许使用令牌）。
-   枚举名称在所有枚举中必须是唯一的，而且对于统计信息名称也必须是唯一的。
-   如果行超过了可以显示的字符数，将会出现换行符，行会被自动截断。
