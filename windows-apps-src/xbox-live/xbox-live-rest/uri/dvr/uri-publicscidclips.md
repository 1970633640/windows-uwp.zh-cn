---
title: /public/scids/{scid}/clips
assetID: 55a1f0ae-08bb-6d1e-a1da-cbeb481c42ee
permalink: en-us/docs/xboxlive/rest/uri-publicscidclips.html
author: KevinAsgari
description: " /public/scids/{scid}/clips"
ms.author: kevinasg
ms.date: 10/12/2017
ms.topic: article
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 131a1eb67d4a33c3fbd2f5f818499ffeea851f3d
ms.sourcegitcommit: 144f5f127fc4fbd852f2f6780ef26054192d68fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2018
ms.locfileid: "5993721"
---
# <a name="publicscidsscidclips"></a>/public/scids/{scid}/clips
访问公开的剪辑。 此 URI 实际上可以指定两种形式，`/public/scids/{scid}/clips`和`/public/titles/{titleId}/clips`。 有关详细信息，请参阅下方。 此 URI 的域是`gameclipsmetadata.xboxlive.com`。
 
  * [URI 参数](#ID4E1)
 
<a id="ID4E1"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| scid| 字符串| 公共剪辑主要服务配置标识符。| 
| titleid| 字符串| 职务公共剪辑的 Id。 不能在相同的 URI 的 scid 中指定。 如果已指定，将用于查找的主 SCID。| 
  
<a id="ID4E6B"></a>

 
## <a name="valid-methods"></a>有效的方法

[GET (/public/scids/{scid}/clips)](uri-publicscidclipsget.md)

&nbsp;&nbsp;列表公共剪辑。
 
<a id="ID4EJC"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4ELC"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[市场 URI](../marketplace/atoc-reference-marketplace.md)

   