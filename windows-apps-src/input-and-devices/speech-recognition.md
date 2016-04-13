---
Description: 使用语音识别提供输入内容、指定操作或命令并完成任务。
title: 语音识别
ms.assetid: 553C0FB7-35BC-4894-9EF1-906139E17552
label: Speech recognition
template: detail.hbs
---

# 语音识别


\[ 已针对 Windows 10 上的 UWP 应用更新。 有关 Windows 8.x 的文章，请参阅[存档](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

使用语音识别提供输入内容、指定操作或命令并完成任务。

**重要的 API**

-   [**Windows.Media.SpeechRecognition**](https://msdn.microsoft.com/library/windows/apps/dn653262)



语音识别由以下部分构成：语音运行时、用于为运行时编程的识别 API、用于听写和 Web 搜索的现成语法，以及帮助用户发现和使用语音识别功能的默认系统 UI。


## <span id="Set_up_the_audio_feed"> </span> <span id="set_up_the_audio_feed"> </span> <span id="SET_UP_THE_AUDIO_FEED"> </span>设置音频源


确保你的设备具有麦克风或等效硬件。

在[应用程序包清单](https://msdn.microsoft.com/library/windows/apps/br211474)（**package.appxmanifest** 文件）中设置**“麦克风”**设备功能 ([**DeviceCapability**](https://msdn.microsoft.com/library/windows/apps/br211430)) 以获取麦克风音频源的访问权限。 这允许应用从所连接的麦克风录制音频。

请参阅[应用功能声明](https://msdn.microsoft.com/library/windows/apps/mt270968)。

## <span id="Recognize_speech_input"> </span> <span id="recognize_speech_input"> </span> <span id="RECOGNIZE_SPEECH_INPUT"> </span>识别语音输入


*约束*可定义该应用在语音输入中识别出的字词和短语（词汇）。 约束是语音识别的核心，它除了能提高语音识别准确度，还能为你的应用带来其他优势。

执行语音识别时，你可以使用各种类型的约束：

1.  **预定义的语法** ([**SpeechRecognitionTopicConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631446))。

    预定义的听写和 Web 搜索语法在无需你创作语法的情况下为你的应用提供语音识别。 使用这些语法时，语音识别由远程 Web 服务执行，并且结果将返回到设备。

    默认自由文本听写语法可以识别用户以特定语言说出的大部分字词或短语，并且为识别短语进行了优化。 如果没有为 [**SpeechRecognizer**](https://msdn.microsoft.com/library/windows/apps/dn653226) 对象指定任何约束，将使用预定义的听写语法。 当你不希望限制用户可说内容的种类时，自由文本听写非常有用。 典型用法包括为一条消息创建笔记或听写其内容。

    诸如听写语法等 Web 搜索语法包含了用户可能说出的大量字词和短语。 但是，优化它的目的是识别用户搜索 Web 时通常使用的术语。

    **注意** 由于预定义的听写和 Web 搜索语法可能很大，而且处于联机状态（不在设备上），性能可能不如安装在设备上的自定义语法快。

     

    These predefined grammars can be used to recognize up to 10 seconds of speech input and require no authoring effort on your part. However, they do require a connection to a network.

    To use web-service constraints, speech input and dictation support must be enabled in **Settings** by turning on the "Get to know me" option in the Settings -&gt; Privacy -&gt; Speech, inking, and typing page.

    Here, we show how to test whether speech input is enabled and open the Settings -&gt; Privacy -&gt; Speech, inking, and typing page, if not.

    First, we initialize a global variable (HResultPrivacyStatementDeclined) to the HResult value of 0x80045509. See [Exception handling for in C\# or Visual Basic](https://msdn.microsoft.com/library/windows/apps/dn532194).

```    CSharp
private static uint HResultPrivacyStatementDeclined = 0x80045509;</code></pre></td>
    </tr>
    </tbody>
    </table>
```

    We then catch any standard exceptions during recogntion and test if the [**HResult**](https://msdn.microsoft.com/library/windows/apps/br206579) value is equal to the value of the HResultPrivacyStatementDeclined variable. If so, we display a warning and call `await Windows.System.Launcher.LaunchUriAsync(new Uri("ms-settings:privacy-accounts"));` to open the Settings page.

    <span codelanguage="CSharp"></span>
```    CSharp
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C#</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
catch (Exception exception)
    {
      // Handle the speech privacy policy error.
      if ((uint)exception.HResult == HResultPrivacyStatementDeclined)
      {
        resultTextBlock.Visibility = Visibility.Visible;
        resultTextBlock.Text = "The privacy statement was declined. 
          Go to Settings -> Privacy -> Speech, inking and typing, and ensure you 
          have viewed the privacy policy, and &#39;Get To Know You&#39; is enabled.";
        // Open the privacy/speech, inking, and typing settings page.
        await Windows.System.Launcher.LaunchUriAsync(new Uri("ms-settings:privacy-accounts")); 
      }
      else
      {
        var messageDialog = new Windows.UI.Popups.MessageDialog(exception.Message, "Exception");
        await messageDialog.ShowAsync();
      }
    }
```

2.  **编程列表约束** ([**SpeechRecognitionListConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631421)).

    编程列表约束提供一种轻型方法，用于使用字词或短语的列表创建一种简单的语法。 列表约束非常适用于识别清晰的短语。 因为语音识别引擎仅须处理语音即可确认匹配，所以采用某种语法明确指定所有字词也可提高识别准确度。 也可以以编程方式更新该列表。

    列表约束由字符串数组组成，此数组表示你的应用将为识别操作接受的语音输入。 你可以通过创建语音识别列表约束对象并传递字符串数组在应用中创建列表约束。 然后，将该对象添加到识别器的约束集合。 当语音识别器识别数组中的任何一个字符串时，识别成功。

3.  **SRGS 语法** ([**SpeechRecognitionGrammarFileConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631412)).

    语音识别语法规范 (SRGS) 语法是一个静态文档，与编程列表约束不同，它使用由 [SRGS 版本 1.0](http://go.microsoft.com/fwlink/p/?LinkID=262302) 定义的 XML 格式。 SRGS 语法提供了对语音识别体验的最大控制，方法是让你在单个识别中捕获多个语义含义。

4.  **语音命令约束** ([**SpeechRecognitionVoiceCommandDefinitionConstraint**](https://msdn.microsoft.com/library/windows/apps/dn653220))

    使用语音命令定义 (VCD) XML 文件定义用户可以在激活应用时说出以启动操作的命令。 有关详细信息，请参阅[在 Cortana 中使用语音命令启动前台应用](launch-a-foreground-app-with-voice-commands-in-cortana.md)。

**注意** 使用哪种类型的约束类型取决于待创建识别体验的复杂程度。 对于特定识别任务，任一类型都可能是最佳选择，你也可能在应用中发现所有类型的约束的用途。
要开始使用约束，请参阅[定义自定义识别约束](define-custom-recognition-constraints.md)。

 

预定义的通用 Windows 应用听写语法可识别使用某种语言的大部分字词和短语。 如果语音识别器对象在没有自定义约束的情况下实例化，它会自动激活。

在该示例中，我们展示如何：

-   创建语音识别器。
-   编译默认 Universal Windows App 约束（未向语音识别器的语法集添加任何语法）。
-   开始使用 [**RecognizeWithUIAsync**](https://msdn.microsoft.com/library/windows/apps/dn653245) 方法提供的基本识别 UI 和 TTS 反馈侦听语音。 如果不需要默认 UI，则使用 [**RecognizeAsync**](https://msdn.microsoft.com/library/windows/apps/dn653244) 方法。

```CSharp
private async void StartRecognizing_Click(object sender, RoutedEventArgs e)
{
    // Create an instance of SpeechRecognizer.
    var speechRecognizer = new Windows.Media.SpeechRecognition.SpeechRecognizer();

    // Compile the dictation grammar by default.
    await speechRecognizer.CompileConstraintsAsync();

    // Start recognition.
    Windows.Media.SpeechRecognition.SpeechRecognitionResult speechRecognitionResult = await speechRecognizer.RecognizeWithUIAsync();

    // Do something with the recognition result.
    var messageDialog = new Windows.UI.Popups.MessageDialog(speechRecognitionResult.Text, "Text spoken");
    await messageDialog.ShowAsync();
}
```

## <span id="Customize_the_recognition_UI"> </span> <span id="customize_the_recognition_ui"> </span> <span id="CUSTOMIZE_THE_RECOGNITION_UI"> </span>自定义识别 UI


当你的应用通过调用 [**SpeechRecognizer.RecognizeWithUIAsync**](https://msdn.microsoft.com/library/windows/apps/dn653245) 来尝试进行语音识别时，多个屏幕将按以下顺序显示。

如果你使用基于预定义语法的约束（听写或 Web 搜索）：

-   “侦听”****屏幕。
-   “思考”****屏幕。
-   “听到你说”****屏幕或错误屏幕。

如果你使用的约束基于字词或短语列表，或者基于 SRGS 语法文件：

-   “侦听”****屏幕。
-   “你说的是”****屏幕，如果用户所说的内容可以解释为不止一种可能性结果。
-   “听到你说”****屏幕或错误屏幕。

下图演示了语音识别器在不同屏幕间的流程的示例，该识别器使用基于 SRGS 语法文件的约束。 在本例中，语音识别是成功的。

![基于 sgrs 语法文件的约束的初始识别屏幕](images/speech-listening-initial.png)

![基于 sgrs 语法文件的约束的中间识别屏幕](images/speech-listening-intermediate.png)

![基于 sgrs 语法文件的约束的最终识别屏幕](images/speech-listening-complete.png)

**Listening** 屏幕可提供应用可识别的字词或短语的示例。 下面我们介绍如何使用 [**SpeechRecognizerUIOptions**](https://msdn.microsoft.com/library/windows/apps/dn653234) 类的属性（通过调用 [**SpeechRecognizer.UIOptions**](https://msdn.microsoft.com/library/windows/apps/dn653254) 属性获取）自定义“侦听”****屏幕上的内容。

```CSharp
private async void WeatherSearch_Click(object sender, RoutedEventArgs e)
{
    // Create an instance of SpeechRecognizer.
    var speechRecognizer = new Windows.Media.SpeechRecognition.SpeechRecognizer();

    // Listen for audio input issues.
    speechRecognizer.RecognitionQualityDegrading += speechRecognizer_RecognitionQualityDegrading;

    // Add a web search grammar to the recognizer.
    var webSearchGrammar = new Windows.Media.SpeechRecognition.SpeechRecognitionTopicConstraint(Windows.Media.SpeechRecognition.SpeechRecognitionScenario.WebSearch, "webSearch");


    speechRecognizer.UIOptions.AudiblePrompt = "Say what you want to search for...";
    speechRecognizer.UIOptions.ExampleText = @"Ex. &#39;weather for London&#39;";
    speechRecognizer.Constraints.Add(webSearchGrammar);

    // Compile the constraint.
    await speechRecognizer.CompileConstraintsAsync();

    // Start recognition.
    Windows.Media.SpeechRecognition.SpeechRecognitionResult speechRecognitionResult = await speechRecognizer.RecognizeWithUIAsync();
    //await speechRecognizer.RecognizeWithUIAsync();

    // Do something with the recognition result.
    var messageDialog = new Windows.UI.Popups.MessageDialog(speechRecognitionResult.Text, "Text spoken");
    await messageDialog.ShowAsync();
}
```

## <span id="related_topics"> </span>相关文章


**开发人员**
* [语音交互](speech-interactions.md)
**设计人员**
* [语音设计指南](https://msdn.microsoft.com/library/windows/apps/dn596121)
**示例**
* [语音识别和语音合成示例](http://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 






<!--HONumber=Mar16_HO4-->


