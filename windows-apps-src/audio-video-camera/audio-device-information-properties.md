---
author: drewbatgit
ms.assetid: 3b75d881-bdcf-402b-a330-23cd29d68e53
description: "本文列出了与音频设备相关的 DeviceInformation 属性"
title: "音频设备信息属性"
ms.author: drewbat
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, uwp
ms.openlocfilehash: 0992c0fc3c6fe9d70b7867275d28e6bba78171ab
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
ms.translationtype: HT
ms.contentlocale: zh-CN
---
# <a name="audio-device-information-properties"></a>音频设备信息属性

本文列出了与音频设备相关的设备信息属性。 在 Windows 上，每台硬件设备均已关联了 [**DeviceInformation**](https://msdn.microsoft.com/library/windows/apps/BR225393) 属性，该属性提供关于设备的详细信息，可供你在需要关于设备的特定信息时或生成设备选择器时使用。 有关在 Windows 上枚举设备的常规信息，请参阅[枚举设备](../devices-sensors/enumerate-devices.md)和[设备信息属性](../devices-sensors/device-information-properties.md)。


|名称|类型|说明|
|------------------------------------------------------------|------------|------------------------------------------------------|
|**System.Devices.AudioDevice.Microphone.SensitivityInDbfs**|Double|以相对于满刻度的分贝 (dBFS) 为单位指定麦克风敏感度。|
|**System.Devices.AudioDevice.Microphone.SignalToNoiseRationInDb**|Double|指定以分贝 (dB) 单位测量的麦克风信号噪声比 (SNR)。|
|**System.Devices.AudioDevice.SpeechProcessingSupported**|布尔值|指示音频设备是否支持语音处理。|
|**System.Devices.AudioDevice.RawProcessingSupported**|布尔值|指示音频设备是否支持原始处理。|
|**System.Devices.MicrophoneArray.Geometry**|未签名的字符[]|麦克风阵列的几何结构数据。|

## <a name="related-topics"></a>相关主题

* [枚举设备](../devices-sensors/enumerate-devices.md)
* [设备信息属性](../devices-sensors/device-information-properties.md)
* [生成设备选择器](../devices-sensors/build-a-device-selector.md)
* [媒体播放](media-playback.md)




