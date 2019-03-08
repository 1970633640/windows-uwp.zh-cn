---
title: XboxServices.config
description: 描述用于将 UWP 游戏与 Xbox Live 配置相关联的 XboxServices.config 文件。
ms.date: 03/29/2018
ms.topic: article
keywords: Xbox live, xbox, 游戏, uwp, windows 10, xbox one, 服务配置, xboxservices.config
ms.localizationpriority: medium
ms.openlocfilehash: 8ff538d691627bf4bb12b3ef6f8b1360e59ac701
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57606682"
---
# <a name="xboxservicesconfig-file-description"></a>XboxServices.config 文件描述

在开发启用 Xbox Live 的 UWP 游戏时，项目中必须包括 XboxServices.config 文件。  此文件，使 Xbox Live SDK，可将您的游戏与合作伙伴中心应用和你的 Xbox Live 服务配置相关联。 此文件包含一个 JSON 对象，详细介绍服务配置 ID、作品 ID 等信息。

如果你要使用 Unity，利用 Xbox Live 插件来设计 Xbox Live 创意者计划游戏，Xbox Live 关联向导会自动创建该文件。

## <a name="xboxservicesconfig-fields"></a>XboxServices.config 字段

>[!NOTE]
> Xbox Live 关联向导创建的文件可能包含下述字段以外的其他字段，但服务不会使用这些字段。

配置文件的 JSON 对象中定义了以下字段：

字段 | 描述
--- | ---
PrimaryServiceConfigId  |  Xbox Live 服务配置 ID (SCID)。 在[合作伙伴中心](https://partner.microsoft.com/dashboard)，可以在上找到此值**Xbox Live**页 （对于 Creators 计划） 或**Xbox Live 安装**页 （对于完整 Xbox Live 游戏） 下,**Services**部分，了解您的应用程序。
TitleId  |  应用的十进制作品 ID。 在[合作伙伴中心](https://partner.microsoft.com/dashboard)，可以在上找到此值**Xbox Live**页 （对于 Creators 计划） 或**Xbox Live 安装**页 （对于完整 Xbox Live 游戏） 下,**Services**部分，了解您的应用程序。
XboxLiveCreatorsTitle  |  如果为“true”，则指示应用是 Xbox Live 创意者计划应用。 否则为“false”。
范围  |  **（可选）** 定义应用所用功能的范围。 有关详细描述，请见下文。

### <a name="scope-field"></a>“范围”字段

**范围**字段是可选字段，可用于指示游戏使用的功能。


如果未指定**范围**字段，则会将范围设置为默认值，该默认值取决于 **XboxLiveCreatorsTitle** 字段的值，如下表中所述：

XboxLiveCreatorsTitle 值 | 默认“范围”值
--- | ---
“true”  |  “xbl.signin xbl.friends”
“false”  |  “xboxlive.signin”



下面的列表描述了**范围**字段的有效值。

“范围”值 | 描述
--- | ---
xbl.signin  | 对创意者计划游戏包括登录功能。 对于创意者计划游戏是必需的。
xbl.friends | 对创意者计划游戏包括好友和社交排行榜功能。
xboxlive.signin | 对访问 Xbox Live 全部功能的游戏包括登录功能。 对于非创意者计划游戏是必需的。

目前，指定**范围**字段的唯一原因是，如果你要创建一款 Xbox Live 创意者计划游戏，并且你的游戏不需要访问好友列表或社交排行榜（限定在你的好友范围的排行榜）。 在这种情况下，你可以向 XboxServices.config 文件中添加下面的一行：

```
  "Scope" : "xbl.signin"
```

添加这一行后，当你首次启动应用时，可以防止 UWP 应用请求好友列表的访问权限。

## <a name="example-xboxservicesconfig-file"></a>示例 XboxServices.config 文件

```
{
  "PrimaryServiceConfigId": "00000000-0000-0000-0000-000064382e34",
  "TitleId": 9039138423,
  "XboxLiveCreatorsTitle": true,
  "Scope" : "xbl.signin xbl.friends"
}
```
