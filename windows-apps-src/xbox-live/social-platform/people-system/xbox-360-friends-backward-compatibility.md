---
title: "Xbox 360 好友向后兼容性"
author: KevinAsgari
description: "了解 Xbox Live 社交平台如何为 Xbox 360 好友系统提供向后兼容性。"
ms.assetid: aeca67b0-2e24-4f3b-b8ff-74823ee0fb36
ms.author: kevinasg
ms.date: 04-04-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "xbox live, xbox, 游戏, uwp, windows 10, xbox one, 好友, xbox 360, 社交平台, 人脉系统"
ms.openlocfilehash: 093369b6be3a9a3139eb35cf38627f22709d610e
ms.sourcegitcommit: 90fbdc0e25e0dff40c571d6687143dd7e16ab8a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2017
---
# <a name="xbox-360-friends-backward-compatibility"></a>Xbox 360 好友向后兼容性

Xbox Live 人脉系统在同一个服务基础结构内同时承载 Xbox 360 好友和新的人脉模型，这两个模型都是为每位用户保留的一个后端列表的一部分。 Xbox 360 好友并不是一次“复制”到新的人脉系统，然后完全单独地进行管理。

## <a name="how-xbox-360-friends-work"></a>Xbox 360 好友的工作原理

人脉系统内包含的实体是旧 Xbox 360 好友的一个精确超集；所有 Xbox 360 好友始终会出现在用户的人脉列表内，虽然人脉列表所包含的联系人比旧客户端中仍然保留的最多 100 个联系人要多得多。 人脉服务与之前的 Xbox 360 好友服务完全向后兼容，没有对之前的调用方进行可见更改；新服务目前正在处理现在与 Xbox 360 好友相关的所有管理。 应用的全局视图基于他们使用的 API；调用旧 API 将只返回旧的 Xbox 360 好友关系，而调用人脉 API 将返回超集人脉全局视图。

使用调用新人脉系统的客户端，用户可以随意添加所需数量的单向关系。 这些关系不会出现在 Xbox 360 中。 通过 Xbox 360 客户端添加新关系，让该关系出现在调用新人脉 API 的客户端中。 此“差异”的存在由设计决定，目的是为了让 Xbox 360 中可能出现的 100 用户中的用户在构建管理用户体验时，或在管理旧邀请流程时不需要新客户端。 新客户端只需用来以全新的方式“思考”世界，并不需要了解旧行为知识。 新的人脉客户端可以选择识别在其人脉列表中有旧好友的用户，然后在“添加”时间询问用户是否希望同时发送旧好友邀请。 这本质上让原本简单的向新客户端添加用户变得复杂，所以不太可能发生。 可以理解的权衡做法是对基于人脉的客户端上发生的任何添加进行双重管理；用户随后必须通过旧客户端添加同一个人。 这还意味着，只使用过新客户端的人一段时间过后可能有很多人脉关系，但如果他们访问旧客户端，就会发现一个完全空着的好友列表。

通过 Xbox 360 删除好友意味着这个人也会从使用新人脉系统的客户端中删除。 与上述的不对称“添加”行为不同，通过人脉系统客户端删除某人也会将其从旧的 Xbox 360 好友列表中删除。 有此要求的原因是有关删除的最糟糕示例场景：骚扰；新旧客户端上与他人有矛盾的用户都不应该需要在两个客户端上删除这个人。 删除关系的频率比添加新好友的频率要低得多，而且会被自然地解读为意味着这个人已经从所有客户端上删除了。 遇到的极端示例是，用户从 Xbox 360 上删除某人只是为了释放 100 个联系人限制的空间，他更希望在新客户端的人脉列表中保留此联系人。 理想情况是，Xbox 360 体验为好友列表几乎已满的用户提供一个在新客户端中保留关系的选项；实际上，实现此方案需要更新 Xbox 360 以使其迅速了解情况，并需要代表应用执行一项重大工作以支持显然属于少数派的这些用户。