---
title: 本地化字符串
author: shrutimundra
description: 了解如何在 Windows 开发人员中心本地化字符串
ms.assetid: e0f307d2-ea02-48ea-bcdf-828272a894d4
ms.author: kevinasg
ms.date: 11/17/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
keywords: Xbox Live, Xbox, 游戏, uwp, windows 10, Xbox one, 本地化字符串, Windows 开发人员中心
ms.openlocfilehash: fac642adad099bf930a4ddabba151384a83db17c
ms.sourcegitcommit: e4f3e1b2d08a02b9920e78e802234e5b674e7223
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "4205386"
---
# <a name="configuring-localized-strings-on-windows-dev-center"></a>在 Windows 开发人员中心配置本地化字符串

可以使用此页面将所有 Xbox Live 配置本地化为你的游戏支持的所有语言。 在所有后续 Xbox Live 页面中创建的所有服务配置都将添加到你要下载的文件中。

你可以使用 [Windows 开发人员中心](https://developer.microsoft.com/dashboard)来配置与你的游戏关联的所有语言的本地化字符串。 通过执行以下操作添加配置：

1. 导航至作品中的**本地化字符串**部分（位于**服务** > **Xbox Live** > **本地化字符串**下）。
2. 单击**下载**按钮会将 localization.xml 文件下载到本地计算机上。

![开发人员中心上本地化字符串配置页面的屏幕截图](../../images/dev-center/localized-strings/localized-strings-1.png)

3. 你可以通过复制添加本地化的字符串 <Value locale="en-US">Maze 播放</Value> 标记，并将区域设置的值更改为你选择的语言和本地化字符串的值。 你必须在开发人员显示区域设置中拥有至少一个值标记，以避免出现错误。

![编辑本地化字符串](../../images/dev-center/localized-strings/localized-strings.gif)

4. 添加所有本地化字符串后，可以通过拖动或浏览本地计算机来上传文件。

![上传 localization.xml 文件的按钮的图像](../../images/dev-center/localized-strings/localized-strings-2.png)

请注意，上传 localization.xml 文件时可能会出现以下错误：

| 错误 | 原因 |
|---------------------------|-------------|
| XSD 验证失败：命名空间‘http://config.mgt.xboxlive.com/schema/localization/1’中的元素‘LocalizedString’不能包含文本。 需要的可能元素列表：命名空间‘http://config.mgt.xboxlive.com/schema/localization/1’中的‘值’ | XML 文档格式不正确时会发生此情况 |
| 本地化字符串缺少开发人员显示区域设置的项目 | 本地化字符串缺少其区域设置与开发人员显示区域设置不匹配的项目时，会发生这种情况 |
| XSD 验证失败：‘区域设置’属性无效 - 根据其数据类型‘http://config.mgt.xboxlive.com/schema/localization/1:NonEmptyString’‘ ’值无效 - 模式约束失败。 | 发生这种情况时的本地化的字符串缺少中的区域设置值 <Value> tag|