---
ms.assetid: B071F6BC-49D3-4E74-98EA-0461A1A55EFB
如果你有应用和应用内产品 (IAP) 的目录，你可以使用 Windows 应用商店收集 API 和 Windows 应用商店购买 API 来访问你的服务中的这些产品的所有权信息。
从服务查看和授予产品
---

# 从服务查看和授予产品


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 的文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


如果你有应用和应用内产品 (IAP) 的目录，你可以使用 *Windows 应用商店收集 API* 和 *Windows 应用商店购买 API* 来访问你的服务中的这些产品的所有权信息。

这些 API 由 REST 方法组合而成，旨在供开发人员用于跨平台服务支持的 IAP 目录。 这些 API 支持你执行以下操作：

-   Windows 应用商店收集 API：查询给定用户拥有的应用和 IAP，或将可消费产品报告为已完成。
-   Windows 应用商店购买 API：向给定用户授予免费应用或 IAP。

## 使用 Windows 应用商店收集 API 和 Windows 应用商店购买 API


Windows 应用商店收集 API 和购买 API 使用 Azure Active Directory (Azure AD) 身份验证访问客户所有权信息。 在你可以调用这些 API 前，必须在 Windows 开发人员中心仪表板中将 Azure AD 元数据应用到你的应用程序并生成若干个所需的访问令牌和密钥。 以下步骤介绍端到端过程：

1.  [在 Azure AD 中配置 Web 应用程序](#step-1:-configure-a-web-application-in-azure-ad)。 此应用程序在 Azure AD 的上下文中表示你的跨平台服务。
2.  [在 Windows 开发人员中心仪表板中将你的 Azure AD 客户端 ID 与应用程序相关联](#step-2:-associate-your-azure-ad-client-id-with-your-application-in-the-windows-dev-denter-dashboard)。
3.  在你的服务中，[生成 Azure AD 访问令牌](#step-3:-retrieve-access-tokens-from-azure-ad)，这些令牌表示你的发布者标识。
4.  在 Windows 应用的客户端代码中，[生成 Windows 应用商店 ID 密钥](#step-4:-generate-a-windows-store-id-key-from-client-side-code-in-your-app)（表示当前用户的标识），并将 Windows 应用商店 ID 密钥传递回你的服务。
5.  在你具有所需的 Azure AD 访问令牌和 Windows 应用商店 ID 密钥后，[从你的服务调用 Windows 应用商店收集 API 或购买 API](#step-5:-call-the-windows-store-collection-api-or-purchase-api-from-your-service)。

以下部分提供有关其中每个步骤的更多详细信息。

### 步骤 1：在 Azure AD 中配置 Web 应用程序

1.  按照[将应用程序与 Azure Active Directory 集成](http://go.microsoft.com/fwlink/?LinkId=722502)中的说明将 Web 应用程序添加到 Azure AD。
    **注意** 在**“向我们说明你的应用程序页”**上，确保你已选择**“Web 应用程序和/或 Web API”**。 这是必需的，以便你可以为你的应用程序获取密钥（也称为*客户端密码*）。 若要调用 Windows 应用商店收集 API 或购买 API，必须在稍后步骤从 Azure AD 中请求访问令牌时提供客户端密码。
2.  在 [Azure 管理门户](http://manage.windowsazure.com/)中，导航到**“Active Directory”**。 选择你的目录、单击顶部的“应用程序”****选项卡，然后选择你的应用程序。
3.  单击**“配置”**选项卡。 在此选项卡上，为你的应用程序获取客户端 ID 并请求密钥（这在稍后的步骤中称为*客户端密码*）。
4.  在屏幕底部，单击**“管理清单”**。 下载你的 Azure AD 应用程序清单并使用以下文本替换 `"identifierUris"` 部分。

    ```json
    "identifierUris" : [                                
            "https://onestore.microsoft.com",
            "https://onestore.microsoft.com/b2b/keys/create/collections",
            "https://onestore.microsoft.com/b2b/keys/create/purchase"
        ],
    ```

    这些字符串表示你的应用程序支持的受众。 在稍后的步骤中，你将创建与其中每个受众值关联的 Azure AD 访问令牌。 有关如何下载应用程序清单的详细信息，请参阅[了解 Azure Active Directory 应用程序清单]( http://go.microsoft.com/fwlink/?LinkId=722500)。

5.  保存你的应用程序清单，并在 [Azure 管理门户](http://manage.windowsazure.com/)中将其上传到你的应用程序。

### 步骤 2：在 Windows 开发人员中心仪表板中将你的 Azure AD 客户端 ID 与应用程序相关联

Windows 应用商店收集 API 和购买 API 仅提供已与你的 Azure AD 客户端 ID 关联的应用和 IAP 的用户所有权信息的访问权限。

1.  登录 [Windows 开发人员中心仪表板](https://dev.windows.com/overview)并选择你的应用。
2.  转到**“服务”**>**“产品收集和购买”**页，然后将你的 Azure AD 客户端 ID 输入到可用字段之一。

### 步骤 3：从 Azure AD 检索访问令牌

在你可以检索 Windows 应用商店 ID 密钥或调用 Windows 应用商店收集 API 或购买 API 前，你的服务必须请求三个表示你的发布者标识的 Azure AD 访问令牌。 其中每个访问令牌都与不同的受众 URI 相关联，每个令牌将通过不同的 API 调用使用。 每个令牌的生命周期为 60 分钟，你可以在它们到期后进行刷新。

若要创建访问令牌，请按照[使用客户端凭据的服务到服务调用](https://msdn.microsoft.com/library/azure/dn645543.aspx)中的说明在你的服务中使用 OAuth 2.0 API。 对于每个令牌，请指定以下参数数据：

-   对于 *client\_id* 和 *client\_secret* 参数，请为你的应用程序指定从 [Azure 管理门户](http://manage.windowsazure.com/)所获取的客户端 ID 和客户端密码。 若要生成带有 Windows 应用商店收集 API 或购买 API 所需的身份验证级别的访问令牌，这两个参数都是必需的。
-   对于 *resource* 参数，请指定以下应用 ID URI 之一（这些 URI 是你以前添加到应用程序清单的 `"identifierUris"` 部分的相同 URI）。 在此过程结束时，你应有三个访问令牌，其中每一个都有与之相关联的这些应用 ID URI 之一：
    -   **https://onestore.microsoft.com/b2b/keys/create/collections**：在稍后的步骤中，你将使用通过此 URI 创建的访问令牌请求与 Windows 应用商店收集 API 一起使用的 Windows 应用商店 ID 密钥。
    -   **https://onestore.microsoft.com/b2b/keys/create/purchase**：在稍后的步骤中，你将使用通过此 URI 创建的访问令牌请求与 Windows 应用商店购买 API 一起使用的 Windows 应用商店 ID 密钥。
    -   **https://onestore.microsoft.com**：在稍后的步骤中，你将在对 Windows 应用商店收集 API 或购买 API 的直接调用中使用你通过此 URI 创建的访问令牌。

    **重要提示** 仅限将 **https://onestore.microsoft.com** 受众与安全存储在你的服务中的访问令牌一起使用。 在服务之外公开访问令牌和此受众会让你的服务易受到重播攻击。

有关访问令牌的结构的更多详细信息，请参阅[受支持的令牌和声明类型](http://go.microsoft.com/fwlink/?LinkId=722501)。

**重要提示** 应仅在服务的上下文而非应用中创建 Azure AD 访问令牌。 客户端密码在发送到你的应用时可能会遭泄露。

 

### 步骤 4：从应用中的客户端代码生成 Windows 应用商店 ID 密钥

在你可以调用 Windows 应用商店收集 API 或购买 API 之前，你的服务必须获取 Windows 应用商店 ID 密钥。 这是 JSON Web 令牌 (JWT)，表示你想要访问其产品所有权信息的用户的标识。 有关此密钥中的声明的详细信息，请参阅 [Windows 应用商店 ID 密钥中的声明](#windowsstorekey)。

当前，获取 Windows 应用商店 ID 密钥的唯一方法是通过从应用中的客户端代码调用通用 Windows 平台 (UWP) API 以检索当前登录 Windows 应用商店的用户的标识。 若要生成 Windows 应用商店 ID 密钥：

1.  将以下访问令牌之一从你的服务传递到客户端应用：
    -   若要获取可以与 Windows 应用商店收集 API 一起使用的 Windows 应用商店 ID 密钥，请传递使用 **https://onestore.microsoft.com/b2b/keys/create/collections** 受众 URI 创建的 Azure AD 访问令牌。
    -   若要获取可以与 Windows 应用商店购买 API 一起使用的 Windows 应用商店 ID 密钥，请传递使用 **https://onestore.microsoft.com/b2b/keys/create/purchase** 受众 URI 创建的 Azure AD 访问令牌。

2.  在你的应用代码中，调用 [**CurrentApp**](https://msdn.microsoft.com/library/windows/apps/hh779765) 类的以下方法之一来检索 Windows 应用商店 ID 密钥。

    -   [
            **GetCustomerCollectionsIdAsync**](https://msdn.microsoft.com/library/windows/apps/mt608674)：如果计划使用 Windows 应用商店收集 API，请调用此方法。
    -   [
            **GetCustomerPurchaseIdAsync**](https://msdn.microsoft.com/library/windows/apps/mt608675)：如果计划使用 Windows 应用商店购买 API，请调用此方法。

    无论调用何种方法，都需要将你的 Azure AD 访问令牌传递给 *serviceTicket* 参数。 你可以选择将 ID 传递给在服务上下文中标识当前用户的 *publisherUserId* 参数。 如果你为服务维护用户 ID，可以使用此参数将这些用户 ID 与对 Windows 应用商店收集 API 或购买 API 进行的调用关联起来。

3.  在你的应用成功检索 Windows 应用商店 ID 密钥后，请将该密钥传递回你的服务。

**注意** 每个 Windows 应用商店 ID 密钥的有效期为 90 天。 密钥到期后，可以[续订该密钥](renew-a-windows-store-id-key.md)。 我们建议你续订 Windows 应用商店 ID 密钥，而非创建新密钥。

 

### 步骤 5：从你的服务调用 Windows 应用商店收集 API 或购买 API

在你的服务具有允许其访问特定用户的产品所有权信息的 Windows 应用商店 ID 密钥后，你的服务可以调用 Windows 应用商店收集 API 或购买 API。 使用适用于你的方案的说明：

-   [查询产品](query-for-products.md)
-   [将可消费产品报告为已完成](report-consumable-products-as-fulfilled.md)
-   [授予免费产品](grant-free-products.md)

对于每个方案，请将以下信息传递给 API：

-   你之前使用 **https://onestore.microsoft.com** 受众 URI 创建的 Azure AD 访问令牌。 此令牌代表你的发布者标识。 在请求标头中传递此令牌。
-   你从应用中的 [**GetCustomerCollectionsIdAsync**](https://msdn.microsoft.com/library/windows/apps/mt608674) 或 [**GetCustomerPurchaseIdAsync**](https://msdn.microsoft.com/library/windows/apps/mt608675) 检索的 Windows 应用商店 ID 密钥。 此密钥表示你想要访问其产品所有权信息的用户的标识。

## Windows 应用商店 ID 密钥中的声明


Windows 应用商店 ID 密钥是 JSON Web 令牌 (JWT)，该令牌表示你想要访问其产品所有权信息的用户的标识。 当使用 Base64 解码时，Windows 应用商店 ID 密钥包含以下声明。

| 声明名称                                                             | 说明                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| iat                                                                    | 标识颁发密钥的时间。 此声明可用于确定令牌的 有效期。 此值表示为纪元时间。                                                                                                                                                                                                                                       |
| iss                                                                    | 标识颁发者。 这与 *aud* 声明具有相同的值。                                                                                                                                                                                                                                                                                                                      |
| aud                                                                    | 标识受众。 必须是下列值之一：**https://collections.mp.microsoft.com/v6.0/keys** 或 **https://purchase.mp.microsoft.com/v6.0/keys**。                                                                                                                                                                                                                    |
| exp                                                                    | 标识在此时或之后不再接受密钥处理除续订密钥之外的任何操作的到期时间。 此声明的值表示为纪元时间。                                                                                                                                                                                               |
| nbf                                                                    | 标识接受令牌进行处理的时间。 此声明的值表示为纪元时间。                                                                                                                                                                                                                                                             |
| http://schemas.microsoft.com/marketplace/2015/08/claims/key/clientId   | 标识开发人员的客户端 ID。                                                                                                                                                                                                                                                                                                                                            |
| http://schemas.microsoft.com/marketplace/2015/08/claims/key/payload    | 包含计划仅由 Windows 应用商店服务使用的信息的不透明负载（已加密，并使用 Base64 编码）。                                                                                                                                                                                                                                                     |
| http://schemas.microsoft.com/marketplace/2015/08/claims/key/userId     | 标识服务上下文中的当前用户的用户 ID。 此值与你在创建密钥时传递给 [**GetCustomerCollectionsIdAsync**](https://msdn.microsoft.com/library/windows/apps/mt608674) 或 [**GetCustomerPurchaseIdAsync**](https://msdn.microsoft.com/library/windows/apps/mt608675) 方法的可选 *publisherUserId* 参数中的值相同。 |
| http://schemas.microsoft.com/marketplace/2015/08/claims/key/refreshUri | 可用于续订密钥的 URI。                                                                                                                                                                                                                                                                                                                                              |

 

以下是一个解码的 Windows 应用商店 ID 密钥标头的示例。

```
{ 
    "typ":"JWT", 
    "alg":"RS256", 
    "x5t":"agA_pgJ7Twx_Ex2_rEeQ2o5fZ5g" 
} 
```

以下是一个解码的 Windows 应用商店 ID 密钥声明集的示例。

```
{ 
    "http://schemas.microsoft.com/marketplace/2015/08/claims/key/clientId": "1d5773695a3b44928227393bfef1e13d", 
    "http://schemas.microsoft.com/marketplace/2015/08/claims/key/payload": "ZdcOq0/N2rjytCRzCHSqnfczv3f0343wfSydx7hghfu0snWzMqyoAGy5DSJ5rMSsKoQFAccs1iNlwlGrX+/eIwh/VlUhLrncyP8c18mNAzAGK+lTAd2oiMQWRRAZxPwGrJrwiq2fTq5NOVDnQS9Za6/GdRjeiQrv6c0x+WNKxSQ7LV/uH1x+IEhYVtDu53GiXIwekltwaV6EkQGphYy7tbNsW2GqxgcoLLMUVOsQjI+FYBA3MdQpalV/aFN4UrJDkMWJBnmz3vrxBNGEApLWTS4Bd3cMswXsV9m+VhOEfnv+6PrL2jq8OZFoF3FUUpY8Fet2DfFr6xjZs3CBS1095J2yyNFWKBZxAXXNjn+zkvqqiVRjjkjNajhuaNKJk4MGHfk2rZiMy/aosyaEpCyncdisHVSx/S4JwIuxTnfnlY24vS0OXy7mFiZjjB8qL03cLsBXM4utCyXSIggb90GAx0+EFlVoJD7+ZKlm1M90xO/QSMDlrzFyuqcXXDBOnt7rPynPTrOZLVF+ODI5HhWEqArkVnc5MYnrZD06YEwClmTDkHQcxCvU+XUEvTbEk69qR2sfnuXV4cJRRWseUTfYoGyuxkQ2eWAAI1BXGxYECIaAnWF0W6ThweL5ZZDdadW9Ug5U3fZd4WxiDlB/EZ3aTy8kYXTW4Uo0adTkCmdLibw=", 
    "http://schemas.microsoft.com/marketplace/2015/08/claims/key/userId": "infusQMLaYCrgtC0d/SZWoPB4FqLEwHXgZFuMJ6TuTY=", 
    "http://schemas.microsoft.com/marketplace/2015/08/claims/key/refreshUri": "https://collections.mp.microsoft.com/v6.0/b2b/keys/renew", 
    "iat": 1442395542, 
    "iss": "https://collections.mp.microsoft.com/v6.0/keys", 
    "aud": "https://collections.mp.microsoft.com/v6.0/keys", 
    "exp": 1450171541, 
    "nbf": 1442391941 
} 
```

## 相关主题

* [查询产品](query-for-products.md)
* [将可消费产品报告为已完成](report-consumable-products-as-fulfilled.md)
* [授予免费产品](grant-free-products.md)
* [续订 Windows 应用商店 ID 密钥](renew-a-windows-store-id-key.md)
* [将应用程序与 Azure Active Directory 集成](http://go.microsoft.com/fwlink/?LinkId=722502)
* [了解 Azure Active Directory 应用程序清单]( http://go.microsoft.com/fwlink/?LinkId=722500)
* [支持的令牌和声明类型](http://go.microsoft.com/fwlink/?LinkId=722501)
 

 





<!--HONumber=Mar16_HO1-->


