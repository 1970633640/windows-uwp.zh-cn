---  
author: WilliamsJason
title: "Xbox Live 测试用户管理 API 参考"
description: "了解如何以编程方式访问用户管理 API。"
translationtype: Human Translation
ms.sourcegitcommit: 67f158b1d3d5ece14c36483a2513a2db2f478660
ms.openlocfilehash: 66fe038fdb54ac5cb9086bf9225d0a5d573b39c8

---  

#Xbox Live 用户管理#

**请求**

你可以获取主机中的用户列表，也可以更新该列表，如添加、删除、登录、注销或修改现有用户。

| 方法        | 请求 URI     | 
| ------------- |-----------------|
| GET           | /ext/user |
| PUT           | /ext/user |
<br>

**URI 参数**

* 无

**请求标头**

* 无

**请求正文**

调用 PUT 应包含具有以下结构的 JSON 数组：

* 用户
  * AutoSignIn（可选）：用于禁用或启用自动登录 EmailAddress 或 UserId 指定帐户的布尔值。
  * EmailAddress（可选，但如果未提供 UserId，则必须提供，除非登录的是赞助用户）：用于指定要修改/添加/删除的用户的电子邮件。
  * 密码（可选，但如果用户当前不在主机上，则必须提供）：用于向主机添加新用户的密码。
  * SignedIn（可选）：用于指定是否应登录或注销所提供帐户的布尔值。
  * UserId（可选，但如果未提供 EmailAddress，则必须提供，除非登录的是赞助用户）：用于指定要修改/添加/删除的用户的 UserId。
  * SponsoredUser（可选）：用于指定是否添加赞助用户的布尔值。
  * 删除（可选）：用于指定是否要从主机中删除此用户的布尔值。

###响应###

**响应正文**

调用 GET 将返回具有以下属性的 JSON 数组：

* 用户
  * AutoSignIn（可选）
  * EmailAddress（可选）
  * Gamertag
  * SignedIn
  * UserId
  * XboxUserId
  * SponsoredUser（可选）
  
**状态代码**

此 API 具有以下预期状态代码。

| HTTP 状态代码   | 说明     | 
| ------------------ |-----------------|
| 200                | 调用 GET 成功，并且在响应正文中已返回用户的 JSON 数组 |
| 204                | 调用 PUT 成功，并且主机中的用户已更新 |
| 4XX                | 无效请求数据或格式的各种错误 |
| 5XX                | 意外失败的错误代码 |
<br>





<!--HONumber=Aug16_HO3-->


