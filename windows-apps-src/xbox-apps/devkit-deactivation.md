---
author: Mtoepke
title: "Xbox One 开发人员模式停用"
description: "如何停用开发人员模式。"
ms.author: mtoepke
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.assetid: 244124dd-d80a-4a72-91db-1c9c2fbc7c3c
ms.openlocfilehash: 46e9e013336f19aedafdb21e0417c878c7c7e8a1
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="xbox-one-developer-mode-deactivation"></a>Xbox One 开发人员模式停用

* [切换到零售模式](#switch-to-retail-mode)
* [使用“开发人员模式激活”应用停用主机](#deactivate-your-console-using-the-dev-mode-activation-app)  
* [重置主机](#reset-your-console)
* [使用 Windows 开发人员中心停用主机](#deactivate-your-console-using-windows-dev-center)

如果你决定不再希望将主机用于开发，请使用以下步骤停用开发人员模式。

## <a name="switch-to-retail-mode"></a>切换到零售模式
首先，将你的 Xbox One 主机返回到零售模式。

1. 打开**开发人员主页**。
2. 单击**退出开发人员模式**。  主机将在零售模式下重新启动。  

   ![退出开发人员模式](images/deactivation-leave-dev-mode.png)

现在，可使用以下方法之一停用你的主机。

## <a name="deactivate-your-console-using-the-dev-mode-activation-app"></a>使用“开发人员模式激活”应用停用主机

在主机上停用开发人员模式的首选方法是使用“开发人员模式激活”应用。 

1. 导航到**我的游戏和应用** > **应用**。
  
   ![激活步骤 3](images/activation-step-3.png)    
   
2.  打开“开发人员模式激活”应用。    
3.  单击**停用**。
  
![停用主机](images/deactivation-app.png)

## <a name="reset-your-console"></a>重置主机

也可以通过重置主机停用开发人员模式。  

> [!NOTE]
> 在重置主机时，将丢失所有本地保存的游戏数据。

若要重置主机，请执行以下步骤：

1.  转到**我的游戏和应用**。  
2.  选择**应用**，然后选择**设置**。  
3.  转到左侧窗格中的**系统**，然后选择右侧窗格中的**主机信息和更新**。  
4.  转到**主机信息和更新**。  
   
    ![主机信息和更新](images/deactivation-console-info-updates.png)  
    
5.  单击**重置主机**。
    
    ![重置主机](images/deactivation-reset-console.png)
    
6.  接下来，单击**重置和删除所有内容**。 此选项用于将主机重置为其原始零售状态。  将删除所有应用、游戏和本地保存数据。 请注意，如果选择另一选项**重置并保留我的游戏和应用**，将无法从开发人员计划中删除你的主机。  
   
    ![重置和删除所有内容](images/deactivation-reset-remove.png)

## <a name="deactivate-your-console-using-windows-dev-center"></a>使用 Windows 开发人员中心停用主机

如果你因某种原因而无法访问你的主机，还使用 Windows 开发人员中心来停用主机上的开发人员模式。

1. 转到 [developer.microsoft.com/xboxdevices](https://developer.microsoft.com/xboxdevices)。    
2. 使用你的开发人员中心帐户登录到开发人员中心。    
3. 通过匹配序列号、主机 ID 或设备 ID，在主机列表中找到要停用的主机。  
4. 单击**停用**。  
  
![使用 DevCenter 执行停用](images/deactivation-devcenter.png)

如果你之前未将 Xbox One 主机返回到零售模式，请立即执行此操作。

1. 启动**开发人员主页**。
2. 单击**退出开发人员模式**。  主机将在零售模式下重新启动。

![激活步骤 13](images/deactivation-leave-dev-mode.png)

## <a name="see-also"></a>另请参阅
- [Xbox One 开发人员模式激活](devkit-activation.md)
- [Xbox One 上的 UWP](index.md)
