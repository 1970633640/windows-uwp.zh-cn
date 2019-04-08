---
ms.assetid: 66a9cfe2-b212-4c73-8a36-963c33270099
description: 本文列出 UWP 应用支持的 HTTP Live Streaming (HLS) 协议标记。
title: HTTP Live Streaming (HLS) 标记支持
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 7c6664d13e76a5774172094d632de9db25109fdc
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57613082"
---
# <a name="http-live-streaming-hls-tag-support"></a>HTTP Live Streaming (HLS) 标记支持
下表列出了 UWP 应用支持的 HLS 标记。

> [!NOTE] 
> 以“X-”开头的自定义标记可以作为定时元数据加以访问，如文章[媒体项、播放列表和曲目](media-playback-with-mediasource.md)中所述。

|Tag |已引入 HLS 协议版本中|HLS 协议文档草案版本|客户端要求|7 月发布的 Windows 10|Windows 10 版本 1511|Windows 10 版本 1607 |
|---------------------|-----------|--------------|---------|--------------|-----|-----|
|4.3.1.  基本标记                 |             |                   |         |             |     |    |
| 4.3.1.1.  EXTM3U |1|0|必填|支持|支持|支持|
| 4.3.1.2.  EXT-X-VERSION |2|3|必填|支持|支持|支持
|4.3.2.  媒体段标记                 |             |                   |         |             |     |    | 
| 4.3.2.1.  EXTINF  |1|0|必填|支持|支持|支持
| 4.3.2.2.  EXT-X-BYTERANGE |4|7|可选|支持|支持|支持|
| 4.3.2.3.  EXT-X-DISCONTINUITY |1|2|可选|支持|支持|支持|
| 4.3.2.4.  EXT-X-KEY |1|0|可选|支持|支持|支持|
|&nbsp;&nbsp;&nbsp; 方法|1|0|属性|“NONE、AES-128”|“NONE、AES-128”|“NONE、AES-128、SAMPLE-AES”|
|&nbsp;&nbsp;&nbsp; URI|1|0|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp; IV|2|3|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp; KEYFORMAT|5|9|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp; KEYFORMATVERSIONS|5|9|属性|不支持|不支持|不支持|
| 4.3.2.5.  EXT-X-MAP |5|9|可选|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp; URI|5|9|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp; BYTERANGE|5|9|属性|不支持|不支持|不支持|
| 4.3.2.6.  EXT-X-PROGRAM-DATE-TIME |1|0|可选|不支持|不支持|不支持|
|4.3.3.  媒体播放列表标记                 |             |                   |         |             |     |    | 
| 4.3.3.1.  EXT-X-TARGETDURATION  |1|0|必填|支持|支持|支持|
| 4.3.3.2.  EXT-X-MEDIA-SEQUENCE  |1|0|可选|支持|支持|支持|
| 4.3.3.3.  EXT-X-DISCONTINUITY-SEQUENCE|6|12|可选|不支持|不支持|不支持|
| 4.3.3.4.  EXT-X-ENDLIST |1|0|可选|支持|支持|支持|
| 4.3.3.5.  EXT-X-PLAYLIST-TYPE |3|6|可选|支持|支持|支持|
| 4.3.3.6.  EXT-X-I-FRAMES-ONLY |4|7|可选|不支持|不支持|不支持|
|4.3.4.  主播放列表标记                 |             |                   |         |             |     |    |
| 4.3.4.1.  EXT-X-MEDIA |4|7|可选|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  类型|4|7|属性|“AUDIO、VIDEO”|“AUDIO、VIDEO”|“AUDIO、VIDEO、SUBTITLES”|
|&nbsp;&nbsp;&nbsp;  URI|4|7|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  组 ID|4|7|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  语言|4|7|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  ASSOC 语言|6|13|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp;  名称|4|7|属性|不支持|不支持|支持|
|&nbsp;&nbsp;&nbsp;  默认值|4|7|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp;  自动选择|4|7|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp;  强制|5|9|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp;  流 ID|6|12|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp;  特征|5|9|属性|不支持|不支持|不支持|
| 4.3.4.2.  EXT-X-STREAM-INF  |1|0|必填|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  带宽|1|0|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  程序 ID|1|0|属性|NA|NA|NA|
|&nbsp;&nbsp;&nbsp;  平均带宽|7|14|属性|不支持|不支持|不支持|
|&nbsp;&nbsp;&nbsp;  编解码器|1|0|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  解决方法|2|3|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  帧速率|7|15|属性|NA|NA|NA|
|&nbsp;&nbsp;&nbsp;  音频|4|7|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  视频|4|7|属性|支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  对白字幕|5|9|属性|不支持|不支持|支持|
|&nbsp;&nbsp;&nbsp;  关闭字幕|6|12|属性|不支持|不支持|不支持|
| 4.3.4.3.  EXT-X-I-FRAME-STREAM-INF  |4|7|可选|不支持|不支持|不支持|
| 4.3.4.4.  EXT-X-SESSION-DATA  |7|14|可选|不支持|不支持|不支持|
| 4.3.4.5.  EXT-X-SESSION-KEY |7|17|可选|不支持|不支持|不支持|
|4.3.5.  媒体或主播放列表标记                  |             |                   |         |             |     |    |
| 4.3.5.1.  EXT-X-INDEPENDENT-SEGMENTS |6|13|可选|不支持|支持|支持|
| 4.3.5.2.  EXT-X-START  |6|12|可选|不支持|部分支持|部分支持|
|&nbsp;&nbsp;&nbsp;  时间偏移量|6|12|属性|不支持|支持|支持|
|&nbsp;&nbsp;&nbsp;  精确|6|12|属性|不支持|默认“不”支持|默认“不”支持|



## <a name="related-topics"></a>相关主题

* [媒体播放](media-playback.md)
* [自适应流式处理](adaptive-streaming.md)
 

 




