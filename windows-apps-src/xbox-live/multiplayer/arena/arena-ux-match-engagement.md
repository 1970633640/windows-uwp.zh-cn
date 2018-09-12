---
title: 比赛参与
author: KevinAsgari
description: 描述玩家在锦标赛经历中不断进阶的 UX 阶段。
ms.author: kevinasg
ms.date: 10-10-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one, arena, 锦标赛, ux
ms.localizationpriority: medium
ms.openlocfilehash: 7d69ab3a5f2ce6092a2aac8dd9cb532ac0848b16
ms.sourcegitcommit: 2a63ee6770413bc35ace09b14f56b60007be7433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3927738"
---
# <a name="match-engagement"></a>比赛参与

玩家在锦标赛中注册并报到后，即可准备开始玩游戏。 参与者可以处于以下四个阶段之一。 每个阶段都包含一套独特的标准，引导用户完成游戏内锦标赛体验。 四个阶段如下：

1.  就绪（Arena UI 或游戏内）
2.  比赛（游戏内）
3.  结果（Arena UI 或游戏内）
4.  结束（Arena UI 或游戏内）

> [!NOTE]  
> 比赛是四个阶段中唯一不受 Arena UI 支持的阶段。 至少，你的游戏必须在每场比赛结束时将参与者重定向到 Arena UI（当“比赛”阶段完成时），以便参与者查看结果。

###### <a name="diagram-the-four-stages-of-participant-progression-after-check-in"></a>图示：参与者在报到后进阶的四个阶段。

![比赛参与流程图](../../images/arena/arena-ux-match-flow.png)

![比赛参与流程条](../../images/arena/arena-ux-match-flow-bar.png)

## <a name="1-ready-waiting-for-match"></a>1. 就绪（“等待比赛”）

![“等待比赛”图示](../../images/arena/arena-ux-flow-ready.png)

### <a name="user-impact"></a>用户影响

在这个阶段，玩家预期要在比赛中玩游戏，但尚不知道对手是谁。 当锦标赛已开始、参与者等待自己的比赛会话开始时，将触发此阶段。 产生此等待期的原因可能是：

* 报到期间仍处于开放状态。
* 下一轮尚未开始。
* 参与者在当前轮中轮空。

### <a name="when-a-bye-is-needed"></a>需要轮空时

在锦标赛的任何一轮中都会有轮空，尽管我们尽量展开种子以避免这种情况。

只要单淘汰制或双淘汰制锦标赛涉及许多玩家或团队，并且数量不是 2 的幂（即 4、8、16、32，64、128 或 256），则必须设置轮空。 轮空仅仅意味着团队不必参加锦标赛的第一轮，而是可以直接进入第二轮。

### <a name="discovery"></a>发现

![团队发现屏幕截图](../../images/arena/arena-ux-team-discovery.png)

在“就绪”阶段，参与者可在以下三个位置了解自己的状态：

* Arena UI：锦标赛详细信息页面
* 游戏内：锦标赛列表、推广、比赛大厅

> [!TIP]  
> **UX 建议**  
> 表示玩家正在等待活动中的下一场比赛。 示例：“比赛挂起”或“收到轮空”通知。  
>
> 如果此阶段受支持，请提供返回锦标赛详细信息页面的方法。  
>
> 提供活动背景：锦标赛名称、状态、风格、描述、开始时间/结束时间等等。


###### <a name="ui-example-in-game-multiplayer-lobby"></a>UI 示例：游戏内的多人游戏大厅

![锦标赛大厅屏幕截图](../../images/arena/arena-ux-tournament-lobby.png)

无论在哪里升级锦标赛或显示比赛详细信息，都会在统一的位置显示锦标赛状态和原因。

当玩家必须做出决定时，请参考以下重要指南：

* 离开游戏以了解详细信息。
* 在锦标赛中需要执行哪些后续步骤。

### <a name="under-the-hood"></a>后台
如果游戏支持此阶段，则在比赛准备就绪后进展至比赛阶段。

 
## <a name="2-playing"></a>2. 比赛

![进行比赛图示](../../images/arena/arena-ux-flow-play.png)

### <a name="user-impact"></a>用户影响

已知玩家的下一场比赛，并且已创建多玩家会话。 在此阶段中，游戏使玩家通过标准的游戏流（比赛设置屏幕、游戏大厅等）。 这是在比赛就绪后用户到达的阶段。

### <a name="discovery"></a>发现

有两种方法可通知锦标赛参与者，并使其从游戏外加入锦标赛：

* **Xbox Toast 通知** – 当显示通知时，参与者可以按 ![nexus 按钮](../../images/xbox-nexus.png)（Nexus 按钮）来启动游戏并进入比赛。

  ![比赛就绪 Toast](../../images/arena/arena-ux-match-ready-toast.png)

* Arena 锦标赛详细信息页面 – 参与者可选择 **Play** 启动游戏并进入比赛
 
> [!TIP]  
> **UX 建议：** 确认进入比赛。  
> 显示 UI，以通知和/或确认参与者将直接进入比赛大厅。

###### <a name="ui-example-match-entry-confirmation-dialog-box"></a>UI 示例：比赛入口确认对话框

![比赛入口确认对话框](../../images/arena/arena-ux-confirm-match-entry.png)

在参与者从游戏外的位置选择进入锦标赛后，显示此 UI。 在启动游戏之后、进入比赛大厅之前执行此操作。

> [!TIP]  
> **UX 建议：** 提供一个用于取消的选项。

参与者可能决定要完成其他任务来准备锦标赛。 有必要支持参与者随意改变主意。 你的游戏可以提供附加选项：

* 留在游戏中。 （参与者将转到主菜单）。
* 返回到 Arena UI。
* 如果参与者选择退出游戏，我们建议你的游戏向参与者通知达到作废超时限制之前的剩余时间。

###### <a name="ui-example-match-entry-confirmation--leave-game-warning"></a>UI 示例：match entry confirmation – 离开游戏警告

![比赛入口作废确认对话框](../../images/arena/arena-ux-confirm-match-cancel.png)

### <a name="playing-a-match"></a>进行比赛

会话模板定义比赛的开始时间。 将它设置为标准 UTC 格式的日期-时间，如 `2009-06-15T13:45:30.0900000Z`。 锦标赛组织者可以随意在开始时间之前尽量提前（包括与开始时间同时）创建会话。 比赛通知于开始时间发送至比赛参与者，因此游戏在开始时间前绝不会激活。 一般情况下，应像处理游戏中的多玩家会话一样对待 Arena 会话。 但有几个区别：

* 你的游戏无法更改游戏会话的名单。
* 缺少面向存在连接速度问题的玩家的常见审核流程。
* 你的游戏必须参与仲裁。

### <a name="match-lobby-details"></a>比赛大厅详细信息

锦标赛比赛大厅应包含详细信息，用以指明这是锦标赛，与标准的多玩家比赛不同。 此类详细信息的示例包括计时、团队依赖关系、连续轮和阶段。 当比赛结束时，要么前进到步骤 3（等待结果），要么使玩家返回到 Arena UI。

###### <a name="ui-example-match-lobby-details"></a>UI 示例：比赛大厅详细信息

![比赛大厅详细信息屏幕](../../images/arena/arena-ux-match-lobby-details.png)

**A** - 强调这是“锦标赛”或“Arena”比赛。  
**B** - 锦标赛详细信息  
   1. 锦标赛名称（最多 128 个字符）  
   2. 风格，游戏模式  
   3. 轮或阶段号  

**C** -“Ready Up/Play”按钮 – 参与者可能已进入锦标赛，但还需要一些时间才能开始比赛会话。 例如，比赛可能需要进行设置，如人物选择。 此功能可在其他团队成员就绪时通知他们。  
**D** - 倒计时器
  * 此计时器基于 **作废超时限制**（由游戏设置）。
  * 这会警告双方团队，如果到此时间无法满足最低团队要求，游戏将作废，活动团队获胜。  

**E** - 广播提醒  
**F** - 团队名称 + 参与者

 
### <a name="under-the-hood"></a>后台

#### <a name="protocol-activation"></a>协议激活

Arena UI 可在用户做好比赛准备时（例如，在接受 Arena 发送的“比赛就绪”Toast 时）直接带其进入游戏，从而启动比赛。 协议激活发生在以下两个时间：启动游戏时或游戏已运行时。 在这两种情况下，激活类似于用户接受游戏邀请后游戏被激活时发生的情况。

* **如果游戏正在启动** -- 当游戏启动时，将触发**已激活**事件。 如果该初始激活为 Arena 协议激活，则意味着你的游戏由尝试在锦标赛中比赛的用户启动。 游戏应尽快绕过主菜单和登录屏幕，尽快跳到比赛。 参与用户的 Xbox 用户 ID (XUID) 在激活 URI 中提供，并且应该已经登录。

* **如果游戏已经在运行** -- 当游戏已经运行时，Arena 协议激活也能触发**激活**事件。 如果游戏在接收协议激活时处于空闲状态，它应立即跳转到锦标赛比赛。 这是安全做法，因为激活事件仅通过显式用户操作（对指引比赛的 Toast 执行操作或从 Arena UI 跳到比赛）触发。 如果游戏在玩游戏期间收到协议激活，游戏应让用户选择离开游戏（如果需要，则先保存）并以最适合的方式进入锦标赛比赛。

* **如果参与者绕过 Xbox Toast 通知** -- 我们建议已启用 Arena 的游戏始终在启动时查询 Arena，以确定用户是否在活动的比赛中。 在这种情况下，游戏应显示“确认比赛入口”UI，告诉用户他们有比赛并询问他们是否要进入比赛。  

  这可以确保参与者在错过比赛 Toast 而只启动游戏时（期望进入比赛）可以正确切换到锦标赛比赛中。 或者，在游戏崩溃的情况下，参与者只需重新启动游戏即可回到比赛中。

> [!NOTE]  
> 游戏应检查协议激活 URI 上的 XUID。 如果它与游戏的当前玩家不匹配，该游戏还必须切换用户上下文。

#### <a name="forfeit-time-out"></a>作废超时

在作废时间（即开始时间加上作废超时，请参阅“比赛图示”）之前，会话中必须至少有一个玩家处于活动状态。 如果在作废时间之前没有人以活动状态加入会话，比赛将取消，并通过 Arena 仲裁为两个团队都判输。
 
## <a name="3-results"></a>3. 结果

![比赛结果图示](../../images/arena/arena-ux-flow-results.png)

在此阶段中，玩家已完成比赛，结果已上报进行仲裁。 此时，尚未确定团队是否仍在锦标赛中。 同时，“结束游戏”屏幕体验应继续报告会话的结果（这一点与任何多玩家比赛相同）。

然后，显示锦标赛结果 - 无比赛（无游戏）、胜、负、平局、排名或无显示。

如果结果立即生成，则可能会跳过此阶段。

### <a name="reporting-results"></a>报告结果

比赛结果使用*仲裁*功能通过会话报告回 Arena 和锦标赛组织者。 仲裁是使用比赛会话确保比赛安全和报告结果的框架。

当比赛会话开始时，它将被视为已仲裁会话。 它具有仲裁框架执行的固定时间线。
 
### <a name="arbitration-time-out"></a>仲裁超时

仲裁超时是在比赛开始时间之后参与者必须参加比赛并报告结果的最长时间。 此值在锦标赛组织者运行事件的会话模板以及 UGT 和作废运行事件的 Arena 多玩家游戏模式中设置，因此所需时间与你的游戏所需时间一样多。

游戏可在开始时间与仲裁时间之间的任何时间报告结果。 在会话的每位活动成员提交结果后，仲裁发生在作废时间与仲裁时间之间的任何时间。 例如，如果在作废时间只有一位成员在会话中处于活动状态，则他们可以（且应该）发布结果，且会发生仲裁。 无论在仲裁时间有多少个结果可用，如果尚未仲裁，都会发生仲裁。

如果用户碰巧在已被仲裁的会话中（因为仲裁超时已到期、游戏服务器仲裁会话或用户加入时间已晚），你的游戏应结束比赛并向用户显示仲裁结果。

仲裁结果始终包括每个团队的结果。 在报告单个玩家的比分时，其中不仅包括该玩家所属团队的结果，而且包含每个团队的整套结果。
只要第一个客户端向 Xbox Live 报告结果，便会自动开始仲裁。 只要所有客户端都报告结果，仲裁便结束。 有些情况下，参与者的比赛时间可能比会话模板中指定的仲裁时间长。 这会引发比赛在参与者准备就绪之前被强制结束的风险。

> [!TIP]  
> **UX 建议：** 提供固定的比赛会话时间框架。
>
> 比赛会话中的预定义时间限制将减少因仲裁超时而出现问题的风险。

有两种选择可防止比赛在参与者完成比赛之前结束：

* 为仲裁超时设置宽松的时间框架。
* 如果固定的时间框架与你的游戏的玩游戏风格冲突，请尝试以下解决方案：
   1.   确定尚未报告结果，并且仲裁超时即将到期（例如，只剩五分钟）。
   2.   显示 UI，提醒参与者他们的游戏将在 X 分钟后结束。 可对所有锦标赛实现此选项，如果仲裁超时很宽松，多少参与者可能从来不会看到此选项。

### <a name="returning-to-the-arena-ui-by-using-a-dedicated-a-button-press"></a>通过按下专用按钮返回 Arena UI

如果你的游戏不显示锦标赛结果或游戏内的阶段进展，建议参与者通过某种方式返回到可提供此信息的 UI。 这可能是 Arena UI 或第三方锦标赛组织者应用。 理想情况下，此服务在比赛结束后出现，或在玩家请求放弃正在进行的比赛时作为响应出现。 可从结束游戏报告屏幕中完成此操作。

> [!TIP]  
> **UX 建议**  
> 将一个控制器按钮专门用作供玩家返回到 Xbox 操作面板中的 Arena 中心的快捷方式。  
>
> ![Arena 中心控制器按钮](../../images/arena/arena-ux-arena-hub-button.png)

### <a name="redirect-participants-at-the-end-of-a-match"></a>在比赛结束时重定向参与者

当参与者完成比赛时，你的游戏清晰指明后续步骤是非常重要的。 这包括查看锦标赛轮或阶段结果的方法（如果游戏内未提供）。

> [!TIP]  
> **UX 建议：** 使用弹出覆盖。
>
> 正在生成锦标赛结果并且结束游戏经历已完成时，会显示此 UI。

### <a name="recommended-ui-data"></a>建议的 UI 数据：

* 锦标赛名称
* 下一步
* 下一轮或阶段详细信息
* 团队战绩
* 仲裁结果
* 到锦标赛详细信息的深度链接
* 留在游戏中的选项

### <a name="under-the-hood"></a>后台

调用 Arena UI 后，你的游戏应继续运行，可能在同一个屏幕中，等待其他协议激活事件。 然后，如果玩家有其他要进行的比赛，游戏将准备前往。 当玩家从一个比赛转到另一个比赛时，在 游戏与 Arena UI 之间切换可以加快用户体验。

###### <a name="ui-example-tournament-arbitrated-resultswinning-team"></a>UI 示例：锦标赛仲裁结果 - 获胜团队

![你已获胜屏幕](../../images/arena/arena-ux-won-game-redirect.png)

###### <a name="ui-example-end-of-tournament-resultsmatch-ended"></a>UI 示例：锦标赛结束结果 - 比赛已结束 

![你输掉比赛屏幕](../../images/arena/arena-ux-lost-game-redirect.png)

## <a name="4-end"></a>4. 结束

![比赛结束图示](../../images/arena/arena-ux-flow-end.png)

当锦标赛本身已结束并报告最终结果时，会出现锦标赛结束阶段流。

参与者被告知锦标赛已结束或玩家已被淘汰。

### <a name="discovery"></a>发现

Arena UI 显示结果并为最终获胜者庆祝：

* 锦标赛详情页面
* 参与者在其玩家或俱乐部活动源中分享的结果
* 发布到玩家个人资料中的锦标赛结果

你的游戏可以显示游戏内锦标赛结果：

* 在参与者完成的最后一轮游戏结束体验之后。
* 在锦标赛浏览功能中的 **My Tournaments** 下列出。


###### <a name="ui-example-end-of-tournament-resultstournament-ended"></a>UI 示例：锦标赛结束结果 - 锦标赛已结束

![锦标赛结束屏幕](../../images/arena/arena-ux-tournament-completed.png)

* 如果此阶段受支持，则提供用于返回 Arena UI 或锦标赛组织者应用的选项。
* 显示事件名称。
* 如果团队有多个成员，则显示团队名称。
* 显示团队在活动中的战绩（如果可用）。 如果不提供战绩（或者除了战绩外），你的游戏应指明玩家对此次活动的参与已结束。
* 你的游戏会指明后续步骤（例如，“观看实时流”、“查找其他锦标赛”、“留在游戏中”）。
* 你的游戏会提供团队参与结束的原因：
  * 已拒绝 - 团队不符合进入锦标赛的资格。
  * 被淘汰 - 团队输掉了锦标赛比赛。
  * 被逐出 - 团队被从活动的锦标赛中除名。
  * 已完成 - 团队已完成锦标赛的最后一轮。