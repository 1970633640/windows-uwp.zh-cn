---
author: mijacobs
Description: "列表动画可使你向集合（如相册或搜索结果列表）中插入或从中删除单个或多个项。"
title: "添加和删除 UWP 应用中的动画"
ms.assetid: A85006AE-4992-457a-B514-500B8BEF5DC8
label: Motion--add and delete animations
template: detail.hbs
translationtype: Human Translation
ms.sourcegitcommit: a4e9a90edd2aae9d2fd5d7bead948422d43dad59
ms.openlocfilehash: a795cf52c3d062d2131832ac3bc765f45097e849

---

# 添加和删除动画




列表动画可使你向集合（如相册或搜索结果列表）中插入或从中删除单个或多个项。

**重要的 API**

-   [**AddDeleteThemeTransition 类**](https://msdn.microsoft.com/library/windows/apps/br243048)


## 应做事项和禁止事项


-   使用列表动画向现有项目集添加单个新项。 例如，当有新的电子邮件到达或者将新照片导入现有的集合中时，可以使用列表动画。
-   使用列表动画可以向一个集合同时添加多个项目。 例如，在将一组新照片导入现有的集合时，可以使用列表动画。 应当同时执行多个项目的添加或删除操作，个别对象的操作之间没有延迟。
-   将添加和删除列表动画作为一对使用。 使用其中一个动画时，将对应的动画用作相反的操作。
-   将列表动画与可以一次性添加或删除一个元素或一组元素的项目列表结合使用。
-   不要使用列表动画来显示或删除容器。 这些动画面向已经显示的集合的成员。 使用弹出动画在应用图面的顶部显示或隐藏暂时容器。 使用内容过渡动画显示或替换作为应用图面一部分的容器。
-   不要在整个项目集上使用列表动画。 使用内容过渡动画添加或删除容器中的整个集合。



## 相关文章


**对于开发人员 (XAML)**
* [动画概述](https://msdn.microsoft.com/library/windows/apps/mt187350)
* [创建添加和删除列表的动画](https://msdn.microsoft.com/library/windows/apps/xaml/jj649430)
* [快速入门：使用库动画创建 UI 动画](https://msdn.microsoft.com/library/windows/apps/xaml/hh452703)
* [**AddDeleteThemeTransition 类**](https://msdn.microsoft.com/library/windows/apps/br243048)

 

 







<!--HONumber=Jun16_HO4-->


