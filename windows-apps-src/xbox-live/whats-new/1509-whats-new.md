---
title: Xbox Live SDK 的新增功能 - 2015 年 9 月
author: KevinAsgari
description: Xbox Live SDK 的新增功能 - 2015 年 9 月
ms.assetid: 84b82fde-f6f3-4dc2-b2df-c7c7313a2cc3
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 7e348254e7e1d7ab233ee1a82e7223a57ebd2781
ms.sourcegitcommit: e6daa7ff878f2f0c7015aca9787e7f2730abcfbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "4314526"
---
# <a name="whats-new-for-the-xbox-live-sdk---september-2015"></a>Xbox Live SDK 的新增功能 - 2015 年 9 月

请参阅[新增功能 - 2015 年 8 月](1508-whats-new.md)文章了解 2015 年 8 月版本中增加了哪些功能。

Xbox Live SDK 的 9 月版本包括下列更新：

## <a name="os-and-tool-support"></a>操作系统和工具支持 ##
Xbox Live SDK 支持 Windows 10 RTM [版本 10.0.10240] 和 Visual Studio 2015 RTM [版本 14.0.23107.0]。

## <a name="contextual-search-apis"></a>上下文搜索 API
* 支持你的游戏或应用程序从你选择的具有实时统计信息的游戏搜索广播。
* 请参见 Microsoft::Xbox::Services::ContextualSearch 中的新 API

## <a name="app-insights-for-events"></a>事件的 App Insights

| 注意 |
|------|
| App Insights 仅适用于 UWP 游戏。  如果你在开发 XDK 游戏，此部分对你不适用 |

<p/>

* 使用 write_in_game_event() 编写的事件可以使用 AppInsights 查看
* 未来将推出相关文档，在此期间请通过你的 DAM 了解相关信息

## <a name="logging"></a>日志记录
* xbox::services::experimental 中的 service_call_logging_config
* 若要通过主机上的 xbTrace.exe 开始和停止，你必须调用 service_call_logging_config 类中的 register_for_protocol_activation。  请在游戏初始化期间进行一次此调用。

## <a name="resync-for-rta"></a>RTA 的重新同步
* 当 RTA 服务认为用户信息可能已过期时可能发生重新同步
* 标题应会为其所订阅的订阅调用相应的 HTTP 调用
* 标题不必重新订阅
* 添加了 xbox::services::real_time_activity_service::add_resync_handler
* 删除了 xbox::services::real_time_activity_service::remove_resync_handler
* 添加了 http_status_429_too_many_requests
* 当游戏因发送了过多的 http 请求而被阻止时将出现此错误条件

## <a name="documentation"></a>文档
* 迁移到 Xbox Live 服务 API 2.0
* 错误处理
* Windows 10 中的 Xbox Live 身份验证
* 上下文搜索
