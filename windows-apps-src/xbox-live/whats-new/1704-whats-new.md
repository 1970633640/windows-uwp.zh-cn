---
title: Xbox Live API 的新增功能 - 2017 年 4 月
author: KevinAsgari
description: Xbox Live API 的新增功能 - 2017 年 4 月
ms.assetid: ''
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one, 竞技场, 锦标赛
ms.localizationpriority: low
ms.openlocfilehash: 45c56f06597a945a5a9a83488241a4db5421654a
ms.sourcegitcommit: 01760b73fa8cdb423a9aa1f63e72e70647d8f6ab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/24/2018
---
# <a name="whats-new-for-the-xbox-live-apis---april-2017"></a>Xbox Live API 的新增功能 - 2017 年 4 月

请参阅[新增功能 - 2017 年 3 月](1703-whats-new.md)文章了解 2017 年 3 月版本中增加了哪些功能。

## <a name="xbox-services-apis"></a>Xbox 服务 API

### <a name="visual-studio-2017"></a>Visual Studio 2017

对于通用 Windows 平台 (UWP) 和 Xbox One 游戏，Xbox Live API 均已更新为支持 Visual Studio 2017。

### <a name="tournaments"></a>锦标赛

添加了新 API 以支持锦标赛。 你现在可以使用 `xbox::services::tournaments::tournament_service` 类从你的游戏访问锦标赛服务。

这些新锦标赛 API 支持以下场景：

* 查询服务以查找当前标题的所有现有锦标赛。
* 从服务检索有关锦标赛的详细信息。
* 查询服务以检索锦标赛的团队列表。
* 从服务检索有关锦标赛团队的详细信息。
* 使用实时活动 (RTA) 订阅跟踪锦标赛和团队的变化。
