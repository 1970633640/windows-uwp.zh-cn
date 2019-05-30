---
ms.assetid: 76776b0f-3163-48c9-835b-3f4213968079
title: 数据访问
description: 本部分讨论在专用数据库中存储设备上的数据，并在通用 Windows 平台 (UWP) 应用中使用对象关系映射。
ms.date: 11/13/2017
ms.topic: article
keywords: windows 10, uwp, 数据, 数据库, 关系, 表, sqlite
ms.localizationpriority: medium
ms.openlocfilehash: 8ce2bbb1b72eaa33001e86c9aa81b334e338cb53
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66362612"
---
# <a name="data-access"></a>数据访问

可以使用 SQLite 数据库将数据存储在用户的设备上。 还可以直接将你的应用连接到 SQL Server 数据库，不需要使用任何类型的服务层。

| 主题 | 描述|
|-------|------------|
| [在 UWP 应用中使用 SQLite 数据库](sqlite-databases.md) | 展示了如何使用 SQLite 在用户设备上的轻量级数据库中存储和检索数据。 SQLite 是一种无服务器的嵌入式数据库引擎。 |
| [在 UWP 应用中使用 SQL Server 数据库](sql-server-databases.md) | 展示了如何使用 [System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.sqlclient?redirectedfrom=MSDN) 命名空间中的类直接连接到 SQL Server 数据库，然后存储和检索数据。 无需任何服务层。 |

## <a name="related-topics"></a>相关主题

* [客户订单数据库示例](https://github.com/Microsoft/Windows-appsample-customers-orders-database)
