---
title: JavaScript 对象表示法 (JSON) 对象参考
assetID: 8efcc6f3-d88a-1b15-bcfc-d79a24581b0a
permalink: en-us/docs/xboxlive/rest/atoc-xboxlivews-reference-json.html
description: " JavaScript 对象表示法 (JSON) 对象参考"
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 703b0750dabfdad55d55534bbe7a66a69d988f53
ms.sourcegitcommit: d2517e522cacc5240f7dffd5bc1eaa278e3f7768
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2018
ms.locfileid: "8336854"
---
# <a name="javascript-object-notation-json-object-reference"></a>JavaScript 对象表示法 (JSON) 对象参考
 
JavaScript 对象表示法 (JSON) 是轻量、 基于标准的且面向对象表示法封装 web 上的数据。
 
Xbox Live 服务定义中，请求和响应，该服务使用的 JSON 对象。 本部分提供有关每个使用 Xbox Live 服务的 JSON 对象的参考信息。
 
<a id="ID4EHB"></a>

 
## <a name="in-this-section"></a>本部分内容

[Achievement (JSON)](json-achievementv2.md)

&nbsp;&nbsp;成就对象 （版本 2）。

[ActivityRecord (JSON)](json-activityrecord.md)

&nbsp;&nbsp;有关一个或多个用户的完整状态进行了格式化，本地化字符串。

[ActivityRequest (JSON)](json-activityrequest.md)

&nbsp;&nbsp;有关一个或多个用户的完整状态信息请求。

[AggregateSessionsResponse (JSON)](json-aggregatesessionsresponse.md)

&nbsp;&nbsp;为用户的适用性会话包含聚合的数据。

[BatchRequest (JSON)](json-batchrequest.md)

&nbsp;&nbsp;用来筛选状态信息，如用户、 设备和游戏的属性的数组。

[DeviceEndpoint (JSON)](json-deviceendpoint.md)

[DeviceRecord (JSON)](json-devicerecord.md)

&nbsp;&nbsp;有关设备，包括其类型和游戏在其上的信息。

[Feedback (JSON)](json-feedback.md)

&nbsp;&nbsp;包含有关玩家的反馈信息。

[GameClip (JSON)](json-gameclip.md)

[GameClipsServiceErrorResponse (JSON)](json-gameclipsserviceerrorresponse.md)

&nbsp;&nbsp;/Users/ {ownerId} {scid} /scids/ /clips/ {gameClipId} 响应的可选部分/uri/格式 / {gameClipUriType} API。

[GameClipThumbnail (JSON)](json-gameclipthumbnail.md)

&nbsp;&nbsp;包含一个单独的缩略图的相关信息。 可以有多个大小每个剪辑，并由客户端，可选择正确显示。

[GameClipUri (JSON)](json-gameclipuri.md)

[GameMessage (JSON)](json-gamemessage.md)

&nbsp;&nbsp;一个游戏会话的消息队列中定义为一条消息的数据的 JSON 对象。

[GameResult (JSON)](json-gameresult.md)

&nbsp;&nbsp;表示介绍游戏会话的结果的数据的 JSON 对象。

[GameSession (JSON)](json-gamesession.md)

&nbsp;&nbsp;多人游戏会话表示游戏数据的 JSON 对象。

[GameSessionSummary (JSON)](json-gamesessionsummary.md)

&nbsp;&nbsp;游戏会话表示摘要数据的 JSON 对象。

[GetClipResponse (JSON)](json-getclipresponse.md)

&nbsp;&nbsp;包装游戏剪辑。

[HopperStatsResults (JSON)](json-hopperstatsresults.md)

&nbsp;&nbsp;表示漏斗的统计信息的 JSON 对象。

[InitialUploadRequest (JSON)](json-initialuploadrequest.md)

&nbsp;&nbsp;POST GameClip 正文上传请求。

[InitialUploadResponse (JSON)](json-initialuploadresponse.md)

[inventoryItem (JSON)](json-inventoryitem.md)

&nbsp;&nbsp;核心库存项目表示标准项可授予权利。

[LastSeenRecord (JSON)](json-lastseenrecord.md)

&nbsp;&nbsp;有关系统上一次看到用户，当用户在没有有效 DeviceRecord 提供的信息。

[MatchTicket (JSON)](json-matchticket.md)

&nbsp;&nbsp;表示玩家用于查找其他玩家通过多人游戏会话目录 (MPSD) 的匹配票证的 JSON 对象。

[MediaAsset (JSON)](json-mediaasset.md)

&nbsp;&nbsp;与成就或其奖励关联的媒体资产。

[MediaRecord (JSON)](json-mediarecord.md)

[MediaRequest (JSON)](json-mediarequest.md)

[MultiplayerActivityDetails (JSON)](json-multiplayeractivitydetails.md)

&nbsp;&nbsp;表示**Microsoft.Xbox.Services.Multiplayer.MultiplayerActivityDetails**的 JSON 对象。

[MultiplayerSessionReference (JSON)](json-multiplayersessionreference.md)

&nbsp;&nbsp;表示**MultiplayerSessionReference**的 JSON 对象。 

[MultiplayerSessionRequest (JSON)](json-multiplayersessionrequest.md)

&nbsp;&nbsp;请求的 JSON 对象传递**MultiplayerSession**对象的操作。

[MultiplayerSession (JSON)](json-multiplayersession.md)

&nbsp;&nbsp;表示**MultiplayerSession**的 JSON 对象。 

[PagingInfo (JSON)](json-paginginfo.md)

&nbsp;&nbsp;包含分页信息中的数据的页面将返回的结果。

[PeopleList (JSON)](json-peoplelist.md)

&nbsp;&nbsp;[Person](json-person.md)对象的集合。

[PermissionCheckBatchRequest (JSON)](json-permissioncheckbatchrequest.md)

&nbsp;&nbsp;PermissionCheckBatchRequest 对象的集合。

[PermissionCheckBatchResponse (JSON)](json-permissioncheckbatchresponse.md)

&nbsp;&nbsp;结果的批处理权限检查的多个用户的权限值列表。

[PermissionCheckBatchUserResponse (JSON)](json-permissioncheckbatchuserresponse.md)

&nbsp;&nbsp;批处理权限的原因检查的一个目标用户的权限值列表。

[PermissionCheckResponse (JSON)](json-permissioncheckresponse.md)

&nbsp;&nbsp;从单个权限设置针对单个目标用户的单个用户检查的结果。

[PermissionCheckResult (JSON)](json-permissioncheckresult.md)

&nbsp;&nbsp;从单个权限设置针对单个目标用户的单个用户检查的结果。

[Person (JSON)](json-person.md)

&nbsp;&nbsp;人脉系统中的单个用户相关的元数据。

[PersonSummary (JSON)](json-personsummary.md)

&nbsp;&nbsp;[个人 (JSON)](json-person.md)对象的集合。

[Player (JSON)](json-player.md)

&nbsp;&nbsp;在游戏会话包含玩家数据。

[PresenceRecord (JSON)](json-presencerecord.md)

&nbsp;&nbsp;联机状态相关的单个用户的数据。

[Profile (JSON)](json-profile.md)

&nbsp;&nbsp;用户的个人配置文件设置。

[Progression (JSON)](json-progression.md)

&nbsp;&nbsp;在用户解锁成就的进度。

[Property (JSON)](json-property.md)

&nbsp;&nbsp;包含匹配请求条件为提供的客户端的属性数据。

[QueryClipsResponse (JSON)](json-queryclipsresponse.md)

&nbsp;&nbsp;包装返回的游戏剪辑，以及列表的分页信息的列表。

[quotaInfo (JSON)](json-quota.md)

&nbsp;&nbsp;包含有关游戏组的配额信息。

[Requirement (JSON)](json-requirement.md)

&nbsp;&nbsp;解锁成就和远用户是向满足这些条件。

[ResetReputation (JSON)](json-resetreputation.md)

&nbsp;&nbsp;包含新的基本信誉评分应更改用户的现有评分。

[Reward (JSON)](json-reward.md)

&nbsp;&nbsp;与成就关联的奖励。

[RichPresenceRequest (JSON)](json-richpresencerequest.md)

&nbsp;&nbsp;完整状态的信息应使用哪些信息请求。

[ServiceError (JSON)](json-serviceerror.md)

&nbsp;&nbsp;包含有关错误对服务调用失败时返回的信息。

[ServiceErrorResponse (JSON)](json-serviceerrorresponse.md)

&nbsp;&nbsp;当遇到服务错误时，将返回一个相应的 HTTP 错误代码。 （可选） 服务还可能包括 ServiceErrorResponse 对象，如下面定义。 在生产环境中可能包含较少的数据。

[SessionEntry (JSON)](json-sessionentry.md)

&nbsp;&nbsp;用于健身会话中包含的数据。

[TitleAssociation (JSON)](json-titleassociation.md)

&nbsp;&nbsp;与成就关联的标题。

[TitleBlob (JSON)](json-titleblob.md)

&nbsp;&nbsp;包含有关作品存储中的信息。

[TitleRecord (JSON)](json-titlerecord.md)

&nbsp;&nbsp;有关游戏，包括其名称和上次修改时间戳的信息。

[TitleRequest (JSON)](json-titlerequest.md)

&nbsp;&nbsp;有关游戏的请求。

[UpdateMetadataRequest (JSON)](json-updatemetadatarequest.md)

&nbsp;&nbsp;应更新剪辑元数据。

[User (JSON)](json-user.md)

&nbsp;&nbsp;包含用户排行榜数据。

[UserClaims (JSON)](json-userclaims.md)

&nbsp;&nbsp;返回当前身份验证的用户的信息。

[UserList (JSON)](json-userlist.md)

&nbsp;&nbsp;[用户](json-user.md)对象的集合。

[UserSettings (JSON)](json-usersettings.md)

&nbsp;&nbsp;返回当前身份验证的用户的设置。

[UserTitle (JSON)](json-usertitlev2.md)

&nbsp;&nbsp;包含用户的游戏数据。

[VerifyStringResult (JSON)](json-verifystringresult.md)

&nbsp;&nbsp;结果代码对应于每个提交给[/system/strings/validate](../uri/stringserver/uri-systemstringsvalidate.md)的字符串。

[XuidList (JSON)](json-xuidlist.md)

&nbsp;&nbsp;要对其执行操作的 Xuid 列表。
 
<a id="ID4ENH"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4EPH"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[Xbox Live 服务 RESTful 参考](../atoc-xboxlivews-reference.md)

  
<a id="ID4EZH"></a>

 
##### <a name="external-links-ecma-international-standard-262-ecmascript-language-specificationhttpwwwecma-internationalorgpublicationsfilesecma-stecma-262pdf"></a>外部链接[ECMA 国际标准 262: ECMAScript 语言规范](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-262.pdf)

   