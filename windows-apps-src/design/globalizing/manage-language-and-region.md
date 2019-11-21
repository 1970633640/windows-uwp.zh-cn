---
Description: This topic defines the terms user profile language list, app manifest language list, and app runtime language list. 我们将在此主题和此功能区域中的其他主题中使用以上术语，因此了解它们的含义非常重要。
title: 了解用户配置文件语言和应用清单语言
ms.assetid: 22D3A937-736A-4121-8285-A55DED56E594
template: detail.hbs
ms.date: 11/08/2017
ms.topic: article
keywords: windows 10, uwp, 全球化, 可本地化性, 本地化
ms.localizationpriority: medium
ms.openlocfilehash: 79edf30733f7bca443c5fd12103fbd5d93909732
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2019
ms.locfileid: "74258068"
---
# <a name="understand-user-profile-languages-and-app-manifest-languages"></a>了解用户配置文件语言和应用清单语言
Windows 用户可以使用**设置** > **时间和语言** > **区域和语言**来配置首选显示语言的排序列表或一种首选显示语言。 某种语言可能会具有区域变体。 例如，可以选择西班牙使用的西班牙语、墨西哥使用的西班牙语、美国使用的西班牙语等。

在**设置** > **时间和语言** > **区域和语言**中，用户还可以独立于语言指定他们在世界上的所在位置（称为地区）。 请注意，显示语言（以及区域变体）设置不是地区设置的决定因素，反之亦然。 例如，尽管某位用户可能目前居住在法国，但选择的却是西班牙语（墨西哥）作为首选 Windows 显示语言。

对于 UWP 应用，语言以 [BCP-47 语言标记](https://tools.ietf.org/html/bcp47)表示。 例如，BCP-47 语言标记“en-US”对应**设置**中的英语（美国）。 相应的 UWP API 将接受并返回 BCP-47 语言标记的字符串表示形式。

另请参阅 [IANA 语言子标记注册表](https://www.iana.org/assignments/language-subtag-registry)。

以下三部分定义了术语“用户配置文件语言列表”、“应用部件清单语言列表”和“应用运行时语言列表”。 我们将在此主题和此功能区域中的其他主题中使用以上术语，因此了解它们的含义非常重要。

## <a name="user-profile-language-list"></a>用户配置文件语言列表
用户配置文件语言列表是用户在**设置** > **时间和语言** > **区域和语言** > **语言**中配置的列表的名称。 在代码中，可以使用 [**GlobalizationPreferences.Languages**](/uwp/api/windows.system.userprofile.globalizationpreferences.Languages) 属性将用户配置文件语言列表作为字符串只读列表进行访问，其中每个字符串均为单个 [BCP-47 语言标记](https://tools.ietf.org/html/bcp47)，例如“en-US”或“ja-JP”。

```csharp
    IReadOnlyList<string> userLanguages = Windows.System.UserProfile.GlobalizationPreferences.Languages;
```

## <a name="app-manifest-language-list"></a>应用部件清单语言列表
应用部件清单语言列表是你的应用声明（或将声明）支持的语言列表。 随着应用从开发生命周期一直到本地化的过程中，此列表会不断扩展。

尽管此列表是在编译时确定的，但可以通过两种方式来精确控制它的确定方式。 一种方式是让 Visual Studio 从项目的文件中确定此列表。 为此，首先在应用包清单源文件 (`Package.appxmanifest`) 中的**应用程序**选项卡上设置应用的**默认语言**。 然后，确认同一文件中包含此配置（默认包含）。

```xml
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
```

每次 Visual Studio 生成构建的应用包清单文件 (`AppxManifest.xml`) 时，它会将源文件中的单个 `Resource` 元素扩展到在项目中所找到的所有语言限定符集中（请参阅[定制语言、比例、高对比度和其他限定符的资源](../../app-resources/tailor-resources-lang-scale-contrast.md)）。 例如，如果已开始本地化，并且具有文件夹名称或文件名称中包含“en-US”、“ja-JP”和“fr-FR”的字符串、图像和/或文件资源，则构建的 `AppxManifest.xml` 文件将包含以下内容（列表中的第一个条目为设置的默认语言）。

```xml
  <Resources>
    <Resource Language="EN-US" />
    <Resource Language="JA-JP" />
    <Resource Language="FR-FR" />
  </Resources>
```

另一种方式是将应用包清单源文件 (`Package.appxmanifest`) 中的单个“x-generate”`<Resource>` 元素替换为 `<Resource>` 元素的扩展列表（注意要首先列出默认语言）。 尽管该方法会涉及更多的维护工作，但如果使用的是自定义构建系统，这可能是合适的方法。

首先，应用部件清单语言列表将仅包含一种语言。 可能是 en-US。 但最后，由于你已手动配置清单或向项目添加已翻译的资源，因此，此列表将扩展。

当应用在 Microsoft Store 中发布后，应用部件清单语言列表中的语言就是向客户显示的语言。 有关 Microsoft Store 专门支持的 BCP-47 语言标记列表，请参阅[支持的语言](../../publish/supported-languages.md)。

在代码中，可以使用 [**ApplicationLanguages.ManifestLanguages**](/uwp/api/windows.globalization.applicationlanguages.ManifestLanguages) 属性将应用部件清单语言列表作为字符串只读列表进行访问，其中每个字符串均为单个 BCP-47 语言标记。

```csharp
    IReadOnlyList<string> userLanguages = Windows.Globalization.ApplicationLanguages.ManifestLanguages;
```

## <a name="app-runtime-language-list"></a>应用运行时语言列表
我们所关注的第三个语言列表是刚刚描述的那两个列表之间的交集。 在运行时，应用已声明支持的语言列表（应用部件清单语言列表）会与用户已声明作为首选项的语言列表（用户配置文件语言列表）进行比较。 应用运行时语言列表会设置为此交集（如果此交集不为空），或者仅设置为应用的默认语言（如果此交集为空）。

更具体地说，应用运行时语言列表是由以下项组成的。

1.  **（可选）主要语言替代**。 [  **PrimaryLanguageOverride**](/uwp/api/Windows.Globalization.ApplicationLanguages.PrimaryLanguageOverride) 是一个简单的替代设置，适用于让用户独立选择语言的应用，或者有充分理由替代默认语言选择的应用。 若要了解详细信息，请参阅[应用程序资源和本地化示例](https://code.msdn.microsoft.com/windowsapps/Application-resources-and-cd0c6eaa)。
2.  **受应用支持的用户语言**。 这是由应用部件清单语言列表筛选的用户配置文件语言列表。 通过受应用支持的语言筛选用户的语言可以保持以下对象之间的一致性：软件开发工具包 (SDK)、类库、从属框架包以及应用。
3.  **如果 1 和 2 为空，则使用默认语言或第一种受应用支持的语言**。 如果用户配置文件语言列表不包含应用支持的任何语言，应用运行时语言则为应用支持的第一种语言。

在代码中，可以使用 [ResourceContext.QualifierValues](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.QualifierValues) 属性以字符串的形式访问应用运行时语言列表，其中包含以分号分隔的 BCP-47 语言标记列表。

```csharp
    string runtimeLanguages = Windows.ApplicationModel.Resources.Core.ResourceContext.GetForCurrentView().QualifierValues["Language"];
```

也可以将它作为字符串只读列表进行访问，其中每个字符串都包含一个 BCP-47 语言标记。 可以使用 [**ResourceContext.Languages**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.Languages) 属性或 [**ApplicationLanguages.Languages**](/uwp/api/windows.globalization.applicationlanguages.Languages) 属性执行此操作。

```csharp
    IReadOnlyList<string> runtimeLanguages = Windows.ApplicationModel.Resources.Core.ResourceContext.GetForCurrentView().Languages;

    runtimeLanguages = Windows.Globalization.ApplicationLanguages.Languages;
```

应用运行时语言列表确定 Windows 为应用加载的资源，以及用于设置日期、时间、数字和其他组件格式的语言。 请参阅[全球化日期/时间/数字格式](use-global-ready-formats.md)。

**注意**：如果用户配置文件语言和应用部件清单语言是彼此的区域变体，用户的区域变体则用作应用运行时语言。 例如，如果用户首选 en-GB，而应用支持 en-US，应用运行时语言则为 en-GB。 这将确保日期、时间和数字的格式更接近用户的期望 (en-GB)，但仍然会使用应用支持的语言 (en-US) 加载本地化资源（由于语言匹配）。

## <a name="qualify-resource-files-with-their-language"></a>使用资源文件的语言限定资源文件
使用语言资源限定符命名资源文件或其文件夹。 若要了解有关资源限定符的详细信息，请参阅[定制语言、比例、高对比度和其他限定符的资源](../../app-resources/tailor-resources-lang-scale-contrast.md)。 A resource file can be an image (or other asset), or it can be a resource container file, such as a *.resw* that contains text strings.

**Note** Even resources in your app's default language must specify the language qualifier. For example, if your app's default language is English (United States), then qualify your assets as `\Assets\Images\en-US\logo.png`.

- Windows performs complex matching, including across regional variants such as en-US and en-GB. So include the region sub-tag as appropriate. 请参阅[资源管理系统匹配语言标记的方式](../../app-resources/how-rms-matches-lang-tags.md)。
- Specify a language script sub-tag in the qualifier when there is no Suppress-Script value defined for the language. For example, instead of zh-CN or zh-TW, use zh-Hant, zh-Hant-TW, or zh-Hans (for more detail, see the [IANA language subtag registry](https://www.iana.org/assignments/language-subtag-registry)).
- For languages that have a single standard dialect, there is no need to include the region qualifier. For example, use ja instead of ja-JP.
- 某些工具和其他组件（如机器翻译程序）可能会发现特定的语言标记（如区域方言信息）在理解数据方面很有帮助。

### <a name="not-all-resources-need-to-be-localized"></a>Not all resources need to be localized

Localization might not be required for all resources.

- At a minimum, ensure all resources exist in the default language.
- A subset of some resources might suffice for a closely related language (partial localization). 例如，如果应用的整个资源集都使用西班牙语，那么你可能不会将应用的全部 UI 本地化为加泰罗尼亚语。 For users who speak Catalan and then Spanish, the resources that are not available in Catalan appear in Spanish.
- Some resources might require exceptions for specific languages, while the majority of other resources map to a common resource. In this case, mark the resource intended to be used for all languages with the undetermined language tag 'und'. Windows interprets the 'und' language tag as a wildcard (similar to '\*') in that it matches the top app language after any other specific match. 例如，如果某些资源对于芬兰语有所不同，但是这些资源的剩余部分对于所有语言都相同，应该使用芬兰语语言标记对芬兰语资源进行标记，而剩余部分则应该通过“und”进行标记。
- For resources that are based on a language script, such as a font or height of text, use the undetermined language tag with a specified script: 'und-&lt;script&gt;'. 例如，对于拉丁语字体，请使用 `und-Latn\\fonts.css`；对于西里尔文字体，请使用 `und-Cryl\\fonts.css`。

## <a name="set-the-http-accept-language-request-header"></a>设置 HTTP 接受的语言请求标头
请考虑所调用的 Web 服务是否具有与应用相同的本地化程度范围。 UWP 应用和桌面应用以典型的 Web 请求形式发出的 HTTP 请求以及 XMLHttpRequest (XHR) 使用标准 HTTP 接受的语言请求标头。 默认情况下，HTTP 标头设置为用户配置文件语言列表。 列表中的每种语言进一步扩展为包含中性语言和权重 (q)。 例如，fr-FR 和 en-US 的用户语言列表会产生 fr-FR、fr、en-US、en 的 HTTP 接受的语言请求标头（“fr-FR,fr;q=0.8,en-US;q=0.5,en;q=0.3”）。 但是，如果天气应用（以此为例）以法语（法国）显示 UI，但用户在其首选项列表中排在最顶端的语言是德语，你则需要从服务中显式请求使用法语（法国），以便在应用内保持一致性。

## <a name="apis-in-the-windowsglobalization-namespace"></a>Windows.Globalization 命名空间中的 API
通常，[**Windows.Globalization**](/uwp/api/windows.globalization?branch=live) 命名空间中的 API 使用应用运行时语言列表确定语言。 如果没有任何一种语言有匹配的格式，则使用用户区域设置。 该区域设置即用于系统时钟的区域设置。 **设置** > **时间和语言** > **区域和语言** > **其他日期、时间和区域设置** > **区域: 更改日期、时间或数字格式**中提供了用户区域设置。 **Windows.Globalization** API 还具有指定要使用的语言列表的替代，而不是应用运行时语言列表。

通过使用 [**Language**](/uwp/api/windows.globalization.language?branch=live) 类，可以检查有关特定语言的详细信息，例如语言的脚本、显示名称和本地名称。

## <a name="use-geographic-region-when-appropriate"></a>在适当的时候使用地理区域
在**设置** > **时间和语言** > **区域和语言** > **国家或地区**中，用户可以指定其在世界上的所在位置。 可以使用此设置（而不是语言）来选择要显示给用户的内容。 例如，新应用可能会默认为从此区域显示内容。

在代码中，可以通过使用 [**GlobalizationPreferences.HomeGeographicRegion**](/uwp/api/windows.system.userprofile.globalizationpreferences.HomeGeographicRegion) 属性访问此设置。

通过使用 [**GeographicRegion**](/uwp/api/windows.globalization.geographicregion?branch=live) 类，可以检查有关特定区域的详细信息，例如其显示名称、本地名称以及使用的货币。

## <a name="examples"></a>示例
下表包含针对各种语言和区域设置用户将在应用的 UI 中看到的内容的示例。

<table border="1">
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">应用部件清单语言列表</th>
<th align="left">用户配置文件语言列表</th>
<th align="left">应用的主要语言替代（可选）</th>
<th align="left">应用运行时语言列表</th>
<th align="left">用户在应用中看到的内容</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">英语(英国) (默认)； 德语(德国)</td>
<td align="left">英语(英国)</td>
<td align="left">无</td>
<td align="left">英语(英国)</td>
<td align="left">UI：英语(英国)<br>日期/时间/数字：英语(英国)</td>
</tr>
<tr>
<td align="left">德语(德国)（默认）；法语(法国)；意大利语(意大利)</td>
<td align="left">法语(奥地利)</td>
<td align="left">无</td>
<td align="left">法语(奥地利)</td>
<td align="left">UI：法语(法国)（从“法语(奥地利)”回退）<br>日期/时间/数字：法语(奥地利)</td>
</tr>
<tr>
<td align="left">英语(美国)（默认）；法语(法国)；英语(英国)</td>
<td align="left">英语(加拿大)； 法语(加拿大)</td>
<td align="left">无</td>
<td align="left">英语(加拿大)； 法语(加拿大)</td>
<td align="left">UI：英语(美国)（从“英语(加拿大)”回退）<br>日期/时间/数字：英语(加拿大)</td>
</tr>
<tr>
<td align="left">西班牙语(西班牙)（默认）；西班牙语(墨西哥)；西班牙语(拉丁美洲)；葡萄牙语(巴西)</td>
<td align="left">英语(美国)</td>
<td align="left">无</td>
<td align="left">西班牙语(西班牙)</td>
<td align="left">UI：西班牙语(西班牙)（由于没有可用于英语的回退，因此使用默认值）<br>日期/时间/数字西班牙语(西班牙)</td>
</tr>
<tr>
<td align="left">加泰罗尼亚语（默认）；西班牙语(西班牙)；法语(法国)</td>
<td align="left">加泰罗尼亚语； 法语(法国)</td>
<td align="left">无</td>
<td align="left">加泰罗尼亚语； 法语(法国)</td>
<td align="left">UI：大部分使用加泰罗尼亚语，部分使用法语(法国)，因为不是所有的字符串都使用加泰罗尼亚语<br>日期/时间/数字：加泰罗尼亚语</td>
</tr>
<tr>
<td align="left">英语(英国)（默认）；法语(法国)；德语(德国)</td>
<td align="left">德语(德国)； 英语(英国)</td>
<td align="left">英语(英国)（用户在应用的 UI 中选择）</td>
<td align="left">英语(英国)；德语(德国)</td>
<td align="left">UI：英语(英国)（语言替代）<br>日期/时间/数字 英语(英国)</td>
</tr>
</tbody>
</table>

>[!NOTE]
> For a list of standard country/region codes used by Microsoft, see the [Official Country/Region List](https://globalready.azurewebsites.net/marketreadiness/OfficialCountryregion).

## <a name="important-apis"></a>重要的 API
* [GlobalizationPreferences.Languages](/uwp/api/windows.system.userprofile.globalizationpreferences.Languages)
* [ApplicationLanguages.ManifestLanguages](/uwp/api/windows.globalization.applicationlanguages.ManifestLanguages)
* [PrimaryLanguageOverride](/uwp/api/Windows.Globalization.ApplicationLanguages.PrimaryLanguageOverride)
* [ResourceContext.QualifierValues](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.QualifierValues)
* [ResourceContext.Languages](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.Languages)
* [ApplicationLanguages.Languages](/uwp/api/windows.globalization.applicationlanguages.Languages)
* [Windows.Globalization](/uwp/api/windows.globalization?branch=live)
* [语言](/uwp/api/windows.globalization.language?branch=live)
* [GlobalizationPreferences.HomeGeographicRegion](/uwp/api/windows.system.userprofile.globalizationpreferences.HomeGeographicRegion)
* [GeographicRegion](/uwp/api/windows.globalization.geographicregion?branch=live)

## <a name="related-topics"></a>相关主题
* [BCP-47 language tag](https://tools.ietf.org/html/bcp47)
* [IANA language subtag registry](https://www.iana.org/assignments/language-subtag-registry)
* [定制语言、比例、高对比度和其他限定符的资源](../../app-resources/tailor-resources-lang-scale-contrast.md)
* [支持的语言](../../publish/supported-languages.md)
* [Globalize your date/time/number formats](use-global-ready-formats.md)
* [资源管理系统如何匹配语言标记](../../app-resources/how-rms-matches-lang-tags.md)

## <a name="samples"></a>示例
* [Application resources and localization sample](https://code.msdn.microsoft.com/windowsapps/Application-resources-and-cd0c6eaa)
