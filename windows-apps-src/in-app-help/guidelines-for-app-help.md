---
author: QuinnRadich
Description: "以下指南描述了如何为你的应用设计有效的“帮助”内容。"
title: "应用帮助指南"
label: Guidelines for app help
template: detail.hbs
ms.sourcegitcommit: 0aa2db498ab7ec25839da259dd0026b0a7cd2b13
ms.openlocfilehash: f2522afa91abe26303a85cbfbabd5ec5b3dba59c

---

# 应用帮助指南

\[ 已针对 Windows 10 上的通用 Windows 平台 (UWP) 应用更新。 有关 Windows 8.x 文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

应用程序可能会很复杂，而为用户提供有效的帮助可大幅改善他们的体验。 并非所有应用程序都需要为其用户提供帮助，并且提供的帮助类型可能有很大的不同，具体取决于应用程序以及用户使用方式。

如果你决定提供帮助，请考虑在此列出的指南。 并且请记住，无用的帮助可能比完全不帮助更糟。

## <span id="intuitive_design"></span><span id="INTUITIVE_DESIGN"></span>直观设计

即使帮助内容再有用，你的应用也无法依靠它来为用户提供良好的体验。 如果有人无法立即发现并使用应用的关键功能，该用户将不会使用你的应用。 没有帮助内容可以更改这样的第一印象。

直观和用户友好的设计是编写有用帮助的第一步。 它不但可使用户长时间参与以使他们使用更高级的功能，它还为用户提供应用核心功能的知识，以便他们在继续使用的过程中依靠这些知识。

## <span id="general_instructions"></span><span id="GENERAL_INSTRUCTIONS"></span>常规说明

除非用户已经遇到问题，否则他们不会查看帮助内容，因此帮助需要为该问题提供简短且有效的解答。 如果帮助不是立即有用，或者帮助过于复杂，则用户更有可能忽略它。

无论类型如何，所有帮助都应遵循以下基本原则：

-   **易于理解：**使用户迷惑的帮助比完全没有帮助更糟。

-   **简单明了：**查找帮助的用户希望向他们直接呈现明确的解答。

-   **相关：**用户不希望必须搜索他们的特定问题。 他们希望最相关的帮助要首先呈现给他们（这称为“上下文帮助”），或者他们希望有轻松导航的界面。

-   **直接：**当用户查找帮助时，他们希望看到帮助。 如果应用包含报告 Bug、提供反馈、查看服务条款或者类似功能的页面，它们应在主帮助页面上包含为链接或脚注，而不是作为重要的项目。

-   **一致：**无论类型如何，帮助仍然是应用的一部分，其处理方式应与 UI 的任何其他部分相同。 在应用其余部分中通用的可用性、可访问性和样式的相同设计原则也应呈现在你所提供的帮助中。

## <span id="types_of_help"></span><span id="TYPES_OF_HELP"></span>帮助的类型

帮助内容有三个主要类别，每种类别都具有不同的优势，并且适用于不同的用途。 你可以在应用中根据需求使用它们的任意组合。

### <span id="instructional_ui"></span><span id="INSTRUCTIONAL_UI"></span>说明性 UI

理想情况下，用户无需说明即可使用应用的所有核心功能，但偶尔应用会依赖使用特定手势，或者应用可能有不明显的辅助功能。 在这些情况下，应使用说明性 UI 来向用户提供有关如何执行特定任务的指令。

[请参阅说明性 UI 指南](instructional-ui.md)

### <span id="in_app_help"></span><span id="IN_APP_HELP"></span>应用内帮助

显示帮助的标准方法是在用户请求时在应用程序内显示它。 可使用多种方法实现此目的，如通过帮助页面或信息说明。 此方法非常适合通用帮助，可毫不复杂地直接回答用户的问题。

[请参阅应用内帮助指南](in-app-help.md)

### <span id="external_help"></span><span id="EXTERNAL_HELP"></span>外部帮助

对于由于太大而无法容纳在应用程序中的详细教程、高级功能或帮助主题库，指向外部网页的链接是理想之选。 应尽量慎用这些链接，因为它们会使用户离开应用程序体验。

[请参阅外部帮助指南](external-help.md)

\[本文包含特定于通用 Windows 平台 (UWP) 应用和 Windows 10 的信息。 有关 Windows 8.1 指南，请下载 [Windows 8.1 指南 PDF](https://go.microsoft.com/fwlink/p/?linkid=258743)。\]



<!--HONumber=Jun16_HO4-->


