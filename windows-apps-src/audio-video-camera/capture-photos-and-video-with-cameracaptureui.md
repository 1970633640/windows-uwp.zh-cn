---
ms.assetid: CC0D6E9B-128D-488B-912F-318F5EE2B8D3
description: 本文介绍如何使用 CameraCaptureUI 类通过内置于 Windows 中的照相机 UI 来捕获照片或视频。
title: 通过 Windows 内置照相机 UI 捕获照片和视频
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: d582d4815b4fb2168b187a1efff3795cc98aca02
ms.sourcegitcommit: 99595e4938213aafdb49635d684d8ba8eb3f697a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69487808"
---
# <a name="capture-photos-and-video-with-the-windows-built-in-camera-ui"></a>通过 Windows 内置照相机 UI 捕获照片和视频



本文介绍如何使用 CameraCaptureUI 类通过内置于 Windows 中的照相机 UI 来捕获照片或视频。 此功能易于使用。 只需几行代码, 应用程序就能获得用户捕获的照片或视频。

如果你希望提供你自己的相机 UI 或者你的方案需要对捕获操作进行更可靠的低级别控制，你应使用 [**MediaCapture**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) 对象并实现自己的捕获体验。 有关详细信息，请参阅[使用 MediaCapture 捕获基本的照片、视频和音频](basic-photo-video-and-audio-capture-with-MediaCapture.md)。

> [!NOTE]
> 如果你的应用程序仅使用 CameraCaptureUI, 则不应在应用程序清单文件中指定**网络摄像机**或**麦克风**功能。 如果这样做, 你的应用程序将以设备的相机隐私设置显示, 但即使用户拒绝对你的应用程序的照相机访问, 这也不会阻止 CameraCaptureUI 捕获媒体。 <p>这是因为 Windows 内置的摄像头应用是受信任的第一方应用，需要用户按下按钮来启动照片、音频和视频捕获。 如果你在使用 CameraCaptureUI 作为唯一的照片捕获机制时指定了网络摄像机或麦克风功能, 则在提交到 Microsoft Store 时, 你的应用程序可能无法使用 Windows 应用程序认证包证书。<p>
如果你使用 MediaCapture 以编程方式捕获音频、照片或视频, 则必须在应用程序清单文件中指定网络摄像机或麦克风功能。

## <a name="capture-a-photo-with-cameracaptureui"></a>使用 CameraCaptureUI 捕获照片

若要使用相机捕获 UI，请将 [**Windows.Media.Capture**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture) 命名空间包含在你的项目中。 若要针对返回的图像文件执行文件操作，请包含 [**Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage)。

[!code-cs[UsingCaptureUI](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetUsingCaptureUI)]

若要捕获照片，请创建新的 [**CameraCaptureUI**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUI) 对象。 通过使用对象的[**PhotoSettings**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.photosettings)属性, 您可以指定返回的照片的属性, 如照片的图像格式。 默认情况下, 相机捕获 UI 支持在返回照片之前对其进行裁剪。 这可以通过[**AllowCropping**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureuiphotocapturesettings.allowcropping)属性来禁用。 此示例设置 [**CroppedSizeInPixels**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureuiphotocapturesettings.croppedsizeinpixels) 以要求返回的图像像素为 200 x 200。

> [!NOTE]
> 移动设备系列中的设备不支持**CameraCaptureUI**中的图像裁剪。 在这些设备上运行应用时，将忽略 [**AllowCropping**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureuiphotocapturesettings.allowcropping) 属性的值。

调用 [**CaptureFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.capturefileasync) 并指定 [**CameraCaptureUIMode.Photo**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUIMode) 以指定应捕获的照片。 如果捕获成功，该方法将返回包含该图像的 [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) 实例。 如果用户取消捕获，则返回的对象为 Null。

[!code-cs[CapturePhoto](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetCapturePhoto)]

将为包含捕获的照片的 **StorageFile** 提供一个动态生成的名称，并将其保存在应用的本地文件夹中。 为了更好地组织您捕获的照片, 您可以将该文件移动到其他文件夹。

[!code-cs[CopyAndDeletePhoto](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetCopyAndDeletePhoto)]

若要在应用中使用你的照片，你可能希望创建可以与多个不同的通用 Windows 应用功能结合使用的 [**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) 对象。

首先, 将[**Windows 映像**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Imaging)命名空间包含在项目中。

[!code-cs[UsingSoftwareBitmap](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetUsingSoftwareBitmap)]

调用 [**OpenAsync**](https://docs.microsoft.com/uwp/api/windows.storage.istoragefile.openasync) 以从图像文件获得一个流。 调用 [**BitmapDecoder.CreateAsync**](https://docs.microsoft.com/uwp/api/windows.graphics.imaging.bitmapdecoder.createasync) 以获取流的位图解码器。 然后, 调用[**GetSoftwareBitmap**](https://docs.microsoft.com/uwp/api/windows.graphics.imaging.bitmapdecoder.getsoftwarebitmapasync)以获取图像的**SoftwareBitmap**表示形式。

[!code-cs[SoftwareBitmap](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetSoftwareBitmap)]

若要在你的 UI 中显示该图像，请在你的 XAML 页面中声明 [**Image**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Image) 控件。

[!code-xml[ImageControl](./code/CameraCaptureUIWin10/cs/MainPage.xaml#SnippetImageControl)]

若要在你的 XAML 页面中使用软件位图，请在你的项目中包括 [**Windows.UI.Xaml.Media.Imaging**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging) 命名空间的使用。

[!code-cs[UsingSoftwareBitmapSource](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetUsingSoftwareBitmapSource)]

**图像**控件要求图像源为 BGRA8 格式, 预乘的 alpha 或无 alpha。 调用静态方法[**SoftwareBitmap**](/uwp/api/windows.graphics.imaging.softwarebitmap.convert) , 以使用所需的格式创建新的软件位图。 接下来, 创建一个新的[**SoftwareBitmapSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging.SoftwareBitmapSource)对象, 并调用[**SetBitmapAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.softwarebitmapsource.setbitmapasync)将软件位图分配给该源。 最后，设置 **Image** 控件的 [**Source**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.image.source) 属性以显示 UI 中已捕获的照片。

[!code-cs[SetImageSource](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetSetImageSource)]

## <a name="capture-a-video-with-cameracaptureui"></a>使用 CameraCaptureUI 捕获视频

若要捕获视频，请创建新的 [**CameraCaptureUI**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUI) 对象。 通过使用对象的[**VideoSettings**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.videosettings)属性, 可以指定返回视频的属性, 例如视频的格式。

调用[**CaptureFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.capturefileasync)并指定[**视频**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.videosettings)来捕获视频。 如果捕获成功，该方法将返回包含该视频的 [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) 实例。 如果取消捕获, 则返回的对象为 null。

[!code-cs[CaptureVideo](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetCaptureVideo)]

针对已捕获的视频文件可以执行的操作取决于你的应用的方案。 本文的其余部分向你介绍了如何从一个或多个已捕获的视频快速创建媒体组合并将其显示在你的 UI 中。

首先, 添加一个[**MediaPlayerElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaPlayerElement)控件, 其中视频组合将显示在 XAML 页面上。

[!code-xml[MediaElement](./code/CameraCaptureUIWin10/cs/MainPage.xaml#SnippetMediaElement)]


当视频文件从相机捕获 UI 返回时, 通过调用 **[CreateFromStorageFile](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource.createfromstoragefile)** 创建新的[**MediaSource**](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) 。 调用与 **MediaPlayerElement** 关联的默认 **[MediaPlayer](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer)** 的 **[Play](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.Play)** 方法以播放视频。

[!code-cs[PlayVideo](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetPlayVideo)]
 

## <a name="related-topics"></a>相关主题

* [摄像头](camera.md)
* [基本的照片、 视频和音频捕获与 MediaCapture](basic-photo-video-and-audio-capture-with-MediaCapture.md)
* [**CameraCaptureUI**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUI) 
 

 




