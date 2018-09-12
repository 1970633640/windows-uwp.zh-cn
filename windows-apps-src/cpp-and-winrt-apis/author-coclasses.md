---
author: stevewhims
description: C + + WinRT 只是因为它可以帮助你创作 Windows 运行时类可以帮助你创作传统的 COM 组件。
title: 创作 COM 组件使用 C + + WinRT
ms.author: stwhi
ms.date: 09/06/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp，标准，c + +，cpp，winrt，投影，作者，COM，组件
ms.localizationpriority: medium
ms.openlocfilehash: 729cfae39f302ae6b5bae275d9e28a39f3d9503b
ms.sourcegitcommit: 2a63ee6770413bc35ace09b14f56b60007be7433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "3935687"
---
# <a name="author-com-components-with-cwinrtwindowsuwpcpp-and-winrt-apisintro-to-using-cpp-with-winrt"></a>使用 COM 组件中创作[C + + WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)

C + + WinRT 可以帮助你创作经典组件对象模型 (COM) 组件 （或组件类），就像它有助于你创作 Windows 运行时类。 下面是非常简单的图示，如果你将其粘贴到可以测试`main.cpp`新**Windows 控制台应用程序 (C + + WinRT)** 项目。

```cppwinrt
// main.cpp : Defines the entry point for the console application.
#include "pch.h"

using namespace winrt;

int main()
{
    init_apartment();

    struct MyCoclass : winrt::implements<MyCoclass, IPersist>
    {
        HRESULT STDMETHODCALLTYPE GetClassID(CLSID* id) noexcept override
        {
            *id = IID_IPersist; // Doesn't matter what we return, for this example.
            return S_OK;
        }
    };

    auto mycoclass_instance{ winrt::make<MyCoclass>() };
    CLSID id{};
    winrt::check_hresult(mycoclass_instance->GetClassID(&id));
}
```

另请参阅[使用 COM 组件与 C + + WinRT](consume-com.md)。

## <a name="a-more-realistic-and-interesting-example"></a>更逼真更具有趣的示例

本主题的其余部分演示了如何创建的最小控制台应用程序项目中使用 C + + WinRT 以实现基本 coclass 和类工厂。 示例应用程序显示了如何，传递 toast 通知回调按钮和 coclass （可实现**INotificationActivationCallback** COM 接口） 允许应用程序启动和名为后退时用户单击 toast 上的按钮。

有关 toast 通知功能区域的更多背景可以位于[发送本地 toast 通知](/windows/uwp/design/shell/tiles-and-notifications/send-local-toast)。 没有任何文档的此部分中的代码示例使用 C + + WinRT，但是，因此我们建议你想在本主题中所示的代码。

## <a name="create-a-windows-console-application-project-toastandcallback"></a>创建 Windows 控制台应用程序项目 (ToastAndCallback)

首先在 Microsoft Visual Studio 中创建新项目。 创建**Visual c + +** > **Windows 桌面版** > **Windows 控制台应用程序 (C + + WinRT)** 项目，然后将其命名为*ToastAndCallback*。

打开`main.cpp`，并删除 using 指令的项目模板生成。 在自己的位置，粘贴下面的代码 （其中的库，标头和所需的类型名称为我们提供）。

```cppwinrt
#pragma comment(lib, "shell32")

#include <iomanip>
#include <iostream>
#include <notificationactivationcallback.h>
#include <propkey.h>
#include <propvarutil.h>
#include <shlobj.h>
#include <winrt/Windows.UI.Notifications.h>
#include <winrt/Windows.Data.Xml.Dom.h>

using namespace winrt;
using namespace Windows::Data::Xml::Dom;
using namespace Windows::UI::Notifications;
```

## <a name="implement-the-coclass-and-class-factory"></a>实现 coclass 和类工厂

在 C + + WinRT，可通过从[**winrt:: implements**](/uwp/cpp-ref-for-winrt/implements)基结构派生实现 coclass 和类工厂。 三个 using 指令如上所示后立即 (之前`main`)，将此代码来实现 toast 通知 COM 激活器组件粘贴。

```cppwinrt
static constexpr GUID callback_guid // BAF2FA85-E121-4CC9-A942-CE335B6F917F
{
    0xBAF2FA85, 0xE121, 0x4CC9, {0xA9, 0x42, 0xCE, 0x33, 0x5B, 0x6F, 0x91, 0x7F}
};

std::wstring const this_app_name{ L"ToastAndCallback" };

struct callback : winrt::implements<callback, INotificationActivationCallback>
{
    HRESULT __stdcall Activate(
        LPCWSTR app,
        LPCWSTR args,
        [[maybe_unused]] NOTIFICATION_USER_INPUT_DATA const* data,
        [[maybe_unused]] ULONG count) noexcept final
    {
        try
        {
            std::wcout << this_app_name << L" has been called back from a notification." << std::endl;
            std::wcout << L"Value of the 'app' parameter is '" << app << L"'." << std::endl;
            std::wcout << L"Value of the 'args' parameter is '" << args << L"'." << std::endl;
            return S_OK;
        }
        catch (...)
        {
            return winrt::to_hresult();
        }
    }
};

struct callback_factory : implements<callback_factory, IClassFactory>
{
    HRESULT __stdcall CreateInstance(
        IUnknown* outer,
        GUID const& iid,
        void** result) noexcept final
    {
        *result = nullptr;

        if (outer)
        {
            return CLASS_E_NOAGGREGATION;
        }

        return make<callback>()->QueryInterface(iid, result);
    }

    HRESULT __stdcall LockServer(BOOL) noexcept final
    {
        return S_OK;
    }
};
```

实现上述 coclass 遵循相同的模式中演示[创作 Api 通过 C + + WinRT](/windows/uwp/cpp-and-winrt-apis/author-apis#if-youre-not-authoring-a-runtime-class)。 请注意，你可以使用此技术不仅用于 Windows 运行时接口 （最终派生自[**IInspectable**](https://msdn.microsoft.com/library/br205821)任何界面），而且要实现 COM 接口 （最终派生自[**IUnknown**](https://msdn.microsoft.com/library/windows/desktop/ms680509)任何接口）。

在上面的代码中 coclass，我们实现**INotificationActivationCallback::Activate**方法，即用户单击 toast 通知上的回调按钮时调用的函数。 但在调用该函数之前，组件类的一个实例需要创建，并且这是**IClassFactory::CreateInstance**函数的工作。

我们只需实现 coclass 称为通知， *COM 激活器*，它具有其类 id (CLSID) 的形式`callback_guid`标识符 （ **GUID**类型），请参阅上述内容。 我们将使用该标识符更高版本，在开始菜单快捷方式和 Windows 注册表项的形式。 COM 激活器 CLSID，并且其关联的 COM 服务器 （这是我们在此处生成的可执行文件的路径） 的路径是一种的机制的 toast 通知知道哪些类创建其回调按钮时的一个实例 (是否通知，则单击在操作中心与否）。

## <a name="best-practices-for-implementing-com-methods"></a>实现 COM 方法的最佳做法

错误处理和资源管理技术可以转手中手。 它是更加方便和实际使用比错误代码的异常。 并且，如果你使用的资源的购置-即-初始化 (RAII) 用法，然后可以避免显式检查错误代码，然后显式释放资源。 此类显式检查使代码更复杂超出必要，并提供 bug 很多地方来隐藏。 相反，使用 RAII，并引发/catch 异常。 这样一来，资源分配异常安全，并在代码很简单。

但是，不允许异常转义你 COM 方法实现。 你可以确保通过使用`noexcept`COM 方法上的说明符。 只要你处理这些方法退出之前已成功为你的方法的调用图中任意位置引发异常。 如果你使用`noexcept`，但你然后允许异常转义你方法中，则将终止你的应用程序。

## <a name="add-helper-types-and-functions"></a>添加帮助程序类型和函数

在此步骤中，我们将添加代码的其余部分进行一些帮助程序类型和函数使用。 因此之前, `main`，添加以下内容。

```cppwinrt
struct prop_variant : PROPVARIANT
{
    prop_variant() noexcept : PROPVARIANT{}
    {
    }

    ~prop_variant() noexcept
    {
        clear();
    }

    void clear() noexcept
    {
        WINRT_VERIFY_(S_OK, ::PropVariantClear(this));
    }
};

struct registry_traits
{
    using type = HKEY;

    static void close(type value) noexcept
    {
        WINRT_VERIFY_(ERROR_SUCCESS, ::RegCloseKey(value));
    }

    static constexpr type invalid() noexcept
    {
        return nullptr;
    }
};

using registry_key = winrt::handle_type<registry_traits>;

std::wstring get_module_path()
{
    std::wstring path(100, L'?');
    uint32_t path_size{};
    DWORD actual_size{};

    do
    {
        path_size = static_cast<uint32_t>(path.size());
        actual_size = ::GetModuleFileName(nullptr, path.data(), path_size);

        if (actual_size + 1 > path_size)
        {
            path.resize(path_size * 2, L'?');
        }
    } while (actual_size + 1 > path_size);

    path.resize(actual_size);
    return path;
}

std::wstring get_shortcut_path()
{
    std::wstring format{ LR"(%ProgramData%\Microsoft\Windows\Start Menu\Programs\)" };
    format += (this_app_name + L".lnk");

    auto required{ ::ExpandEnvironmentStrings(format.c_str(), nullptr, 0) };
    std::wstring path(required - 1, L'?');
    ::ExpandEnvironmentStrings(format.c_str(), path.data(), required);
    return path;
}
```

## <a name="implement-the-remaining-functions-and-the-wmain-entry-point-function"></a>实现其余的函数和 wmain 入口点函数

项目模板生成`main`为你的函数。 删除`main`函数，并在其位置粘贴此代码列表，其中包括注册你 coclass 的代码，然后提供 toast 能够调用返回你的应用程序。

```cppwinrt
void register_callback()
{
    DWORD registration{};

    winrt::check_hresult(::CoRegisterClassObject(
        callback_guid,
        make<callback_factory>().get(),
        CLSCTX_LOCAL_SERVER,
        REGCLS_SINGLEUSE,
        &registration));
}

void create_shortcut()
{
    auto link{ winrt::create_instance<IShellLink>(CLSID_ShellLink) };
    std::wstring module_path{ get_module_path() };
    winrt::check_hresult(link->SetPath(module_path.c_str()));

    auto store = link.as<IPropertyStore>();
    prop_variant value;
    winrt::check_hresult(::InitPropVariantFromString(this_app_name.c_str(), &value));
    winrt::check_hresult(store->SetValue(PKEY_AppUserModel_ID, value));
    value.clear();
    winrt::check_hresult(::InitPropVariantFromCLSID(callback_guid, &value));
    winrt::check_hresult(store->SetValue(PKEY_AppUserModel_ToastActivatorCLSID, value));

    auto file{ store.as<IPersistFile>() };
    std::wstring shortcut_path{ get_shortcut_path() };
    winrt::check_hresult(file->Save(shortcut_path.c_str(), TRUE));

    std::wcout << L"In " << shortcut_path << L", created a shortcut to " << module_path << std::endl;
}

void update_registry()
{
    std::wstring key_path{ LR"(SOFTWARE\Classes\CLSID\{????????-????-????-????-????????????})" };
    ::StringFromGUID2(callback_guid, key_path.data() + 23, 39);
    key_path += LR"(\LocalServer32)";
    registry_key key;

    winrt::check_win32(::RegCreateKeyEx(
        HKEY_CURRENT_USER,
        key_path.c_str(),
        0,
        nullptr,
        0,
        KEY_WRITE,
        nullptr,
        key.put(),
        nullptr));
    ::RegDeleteValue(key.get(), nullptr);

    std::wstring path{ get_module_path() };

    winrt::check_win32(::RegSetValueEx(
        key.get(),
        nullptr,
        0,
        REG_SZ,
        reinterpret_cast<BYTE const*>(path.c_str()),
        static_cast<uint32_t>((path.size() + 1) * sizeof(wchar_t))));

    std::wcout << L"In " << key_path << L", registered local server at " << path << std::endl;
}

void create_toast()
{
    XmlDocument xml;

    std::wstring toastPayload
    {
        LR"(
<toast>
  <visual>
    <binding template='ToastGeneric'>
      <text>)"
    };
    toastPayload += this_app_name;
    toastPayload += LR"(
      </text>
    </binding>
  </visual>
  <actions>
    <action content='Call back )";
    toastPayload += this_app_name;
    toastPayload += LR"(
' arguments='the_args' activationKind='Foreground' />
  </actions>
</toast>)";
    xml.LoadXml(toastPayload);

    ToastNotification toast{ xml };
    ToastNotifier notifier{ ToastNotificationManager::CreateToastNotifier(this_app_name) };
    notifier.Show(toast);
}

void LaunchedNormally(HANDLE, INPUT_RECORD &, DWORD &);
void LaunchedFromNotification(HANDLE, INPUT_RECORD &, DWORD &);

int wmain(int argc, wchar_t * argv[], wchar_t * /* envp */[])
{
    init_apartment();

    register_callback();

    HANDLE consoleHandle{ ::GetStdHandle(STD_INPUT_HANDLE) };
    INPUT_RECORD buffer{};
    DWORD events{};
    ::FlushConsoleInputBuffer(consoleHandle);

    if (argc == 1)
    {
        LaunchedNormally(consoleHandle, buffer, events);
    }
    else if (argc == 2 && wcscmp(argv[1], L"-Embedding") == 0)
    {
        LaunchedFromNotification(consoleHandle, buffer, events);
    }
}

void LaunchedNormally(HANDLE consoleHandle, INPUT_RECORD & buffer, DWORD & events)
{
    try
    {
        bool runningAsAdmin{ ::IsUserAnAdmin() == TRUE };
        std::wcout << this_app_name << L" is running" << (runningAsAdmin ? L" (Administrator)." : L".") << std::endl;

        if (runningAsAdmin)
        {
            create_shortcut();
            update_registry();
        }

        std::wcout << std::endl << L"Press 'T' to display a toast notification (press any other key to exit)." << std::endl;

        ::ReadConsoleInput(consoleHandle, &buffer, 1, &events);
        if (towupper(buffer.Event.KeyEvent.uChar.UnicodeChar) == L'T')
        {
            create_toast();
        }
    }
    catch (winrt::hresult_error const& e)
    {
        std::wcout << L"Error: " << e.message().c_str() << L" (" << std::hex << std::showbase << std::setw(8) << static_cast<uint32_t>(e.code()) << L")" << std::endl;
    }
}

void LaunchedFromNotification(HANDLE consoleHandle, INPUT_RECORD & buffer, DWORD & events)
{
    ::Sleep(50); // Give the callback chance to display its message.
    std::wcout << std::endl << L"Press any key to exit." << std::endl;
    ::ReadConsoleInput(consoleHandle, &buffer, 1, &events);
}
```

## <a name="how-to-test-the-example-application"></a>如何测试示例应用程序

生成应用程序，然后在以管理员身份会导致在注册时，和其他设置，代码运行至少一次运行它。 指示是否正在运行它作为管理员，然后按 \ 会导致显示 toast。 然后可以单击该**回调 ToastAndCallback**按钮可以直接从 toast 通知，将启动 pop，或从操作中心和你的应用程序、 实例化，coclass 和 INotificationActivationCallback **:: 激活**执行方法。

## <a name="important-apis"></a>重要的 API
* [IInspectable 接口](https://msdn.microsoft.com/library/br205821)
* [IUnknown 接口](https://msdn.microsoft.com/library/windows/desktop/ms680509)
* [winrt::implements 结构模板](/uwp/cpp-ref-for-winrt/implements)

## <a name="related-topics"></a>相关主题
* [使用 C++/WinRT 创作 API](/windows/uwp/cpp-and-winrt-apis/author-apis)
* [使用 COM 组件使用 C + + WinRT](consume-com.md)
* [发送本地 toast 通知](/windows/uwp/design/shell/tiles-and-notifications/send-local-toast)
