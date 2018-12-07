---
title: Xbox Live API 的新增功能 - 2017 年 7 月
description: Xbox Live API 的新增功能 - 2017 年 7 月
ms.assetid: ''
ms.date: 07/16/2017
ms.topic: article
keywords: Xbox live, xbox, 游戏, uwp, windows 10, xbox one, 新增功能, 2017 年 7 月
ms.localizationpriority: medium
ms.openlocfilehash: 47db721a98b71fd6f4b5175a88ddccd00048d8d9
ms.sourcegitcommit: d7613c791107f74b6a3dc12a372d9de916c0454b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2018
ms.locfileid: "8739395"
---
# <a name="whats-new-for-the-xbox-live-apis---july-2017"></a>Xbox Live API 的新增功能 - 2017 年 7 月

请参阅[新增功能 - 2017 年 6 月](1706-whats-new.md)文章了解 2017 年 6 月版本中增加了哪些功能。

你也可以查看 [Xbox Live API GitHub 提交历史记录](https://github.com/Microsoft/xbox-live-api/commits/master)，了解 Xbox Live API 的所有最新的代码更改。

## <a name="xbox-live-features"></a>Xbox Live 功能

### <a name="multiplayer-updates"></a>多人游戏更新

查询活动句柄和搜索句柄现在在响应中包含自定义会话属性。

### <a name="tournaments"></a>锦标赛

添加了新 API 以支持锦标赛。 你现在可以使用 xbox::services::tournaments::tournament_service 类从你的游戏访问锦标赛服务。
这些新锦标赛 API 支持以下场景：
* 查询服务以查找当前标题的所有现有锦标赛。
* 从服务检索有关锦标赛的详细信息。
* 查询服务以检索锦标赛的团队列表。
* 从服务检索有关锦标赛团队的详细信息。
* 使用实时活动 (RTA) 订阅跟踪锦标赛和团队的变化。
