---
title: 对社交服务进行编程
description: 提供如何使用 Xbox Live 社会管理器 API 的代码示例。
ms.assetid: 101d059a-e03f-472c-8300-800aa5730ee2
ms.date: 04/04/2017
ms.topic: article
keywords: Xbox live, xbox, 游戏, uwp, windows 10, xbox one, 社交管理器, 示例
ms.localizationpriority: medium
ms.openlocfilehash: 5039d9ed205cadfee3b2e64527a1f58f1624accc
ms.sourcegitcommit: 8921a9cc0dd3e5665345ae8eca7ab7aeb83ccc6f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "8898165"
---
# <a name="programming-social-services"></a>对社交服务进行编程

> [!NOTE]
> 本文演示高级 API 的使用。  作为起点，请看一看[社交管理器 API 简介](../intro-to-social-manager.md)，它让开发大大简化。  如果你在社交管理器中发现了不受支持的场景，请告知 DAM。

以下代码示例演示如何使用 Xbox Live 检索社交关系。 它将生成系统上所有用户的列表，并检索第一个用户。 然后检索该用户的所有社交关系。 最后将显示这些关系中每个关系的公共属性。

```cpp
XboxLiveContext^ xboxLiveContext = NULL;

// An XboxLiveContext for a user should be created only once, or you may encounter unpredictable behavior.
void OneTimeInit()
{
  // Get the XboxLiveContext.  This should only be done once per user after signing in.
  xboxLiveContext = ref new Microsoft::Xbox::Services::XboxLiveContext(User::Users->GetAt(0));
}

void Example_SocialService_GetSocialRelationshipsAsync()
{
    // Generate a list of users on the system.
    // Create an XboxLiveContext from user 0 (the first one returned).
    // This user's authentication token will be used for service requests.
    XboxLiveContext^ xboxLiveContext = ref new Microsoft::Xbox::Services::XboxLiveContext(User::Users->GetAt(0));

    // Asynchronously retrieve all social relationships from that context.
    auto asyncOp = xboxLiveContext->SocialService->GetSocialRelationshipsAsync();

    create_task( asyncOp )
    .then([](XboxSocialRelationshipResult^ result)
    {
        // For each social relationship of the specified user...
        for( XboxSocialRelationship^ xboxSocialRelationship : result->Items )
        {
            // ...display the public properties of the relationship.
            LogComment( xboxSocialRelationship->XboxUserId );
            LogComment( xboxSocialRelationship->IsFavorite.ToString() );
        }

    })
    .wait();
}
```
