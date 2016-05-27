---
author: dbirtolo
ms.assetid: bfabd3d5-dd56-4917-9572-f3ba0de4f8c0
title: Device Portal 核心 API 参考
description: 了解 Windows Device Portal 核心 REST API，可用于访问数据和以编程方式控制设备。
---

# Device Portal 核心 API 参考

Windows Device Portal 中的所有内容都基于 REST API 生成，该 API 可用于访问数据和以编程方式控制设备。

## 应用部署

---
### 安装应用

**请求**

可以使用以下请求格式安装应用。

方法      | 请求 URI
:------     | :-----
POST | /api/app/packagemanager/package
<br />
**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
package   | （**必需**）要安装的程序包的文件名。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 已接受和正在处理的部署请求
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 获取应用安装状态

**请求**

可以通过使用以下请求格式来获取当前正在进行的应用安装状态。
 
方法      | 请求 URI
:------     | :-----
GET | /api/app/packagemanager/state
<br />
**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 最后一个部署的结果
204 | 安装正在运行
404 | 未找到任何安装操作
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 卸载应用

**请求**

可以通过使用以下请求格式来卸载应用。
 
方法      | 请求 URI
:------     | :-----
DELETE | /api/app/packagemanager/package
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 获取已安装应用

**请求**

可以通过使用以下请求格式来获取系统上已安装应用的列表。
 
方法      | 请求 URI
:------     | :-----
GET | /api/app/packagemanager/packages
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包含已安装程序包列表以及相关详细信息。 此响应的模板如下所示。
```
{"InstalledPackages": [
    {
        "Name": string,
        "PackageFamilyName": string,
        "PackageFullName": string,
        "PackageOrigin": int, (https://msdn.microsoft.com/en-us/library/windows/desktop/dn313167(v=vs.85).aspx)
        "PackageRelativeId": string,
        "Publisher": string,
        "Version": {
            "Build": int,
            "Major": int,
            "Minor": int,
            "Revision": int
     },
     "RegisteredUsers": [
     {
        "UserDisplayName": string,
        "UserSID": string
     },...
     ]
    },...
]}
```
**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
## 设备管理器
---
### 获取计算机上已安装的设备

**请求**

可以通过使用以下请求格式来获取计算机上已安装设备的列表。
 
方法      | 请求 URI
:------     | :-----
GET | /api/devicemanager/devices
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括连接到该设备的设备的 JSON 数组。
``` 
{"DeviceList": [
    {
        "Class": string,
        "Description": string,
        "ID": string,
        "Manufacturer": string,
        "ParentID": string,
        "ProblemCode": int,
        "StatusCode": int
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* IoT

---
## 转储集合
---
### 获取应用的所有故障转储列表

**请求**

可以通过使用以下请求格式来获取所有旁加载应用的所有可用故障转储列表。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/usermode/dumps
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括每个旁加载应用程序的故障转储列表。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 获取应用的故障转储集合设置

**请求**

可以通过使用以下请求格式来获取旁加载应用的故障转储集合设置。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/usermode/crashcontrol
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
packageFullname   | （**必需**）旁加载的应用的程序包的完整名称。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应具有以下格式：
```
{"CrashDumpEnabled": bool}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 删除旁加载应用的故障转储

**请求**

可以通过使用以下请求格式来删除旁加载应用的故障转储。
 
方法      | 请求 URI
:------     | :-----
DELETE | /api/debug/dump/usermode/crashdump
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
packageFullname   | （**必需**）旁加载的应用的程序包的完整名称。
fileName   | （**必需**）应该删除的转储文件的名称。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 禁用旁加载应用的故障转储

**请求**

可以通过使用以下请求格式来禁用旁加载应用的故障转储。
 
方法      | 请求 URI
:------     | :-----
DELETE | /api/debug/dump/usermode/crashcontrol

<br />
**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
packageFullname   | （**必需**）旁加载的应用的程序包的完整名称。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 下载旁加载应用的故障转储

**请求**

可以通过使用以下请求格式来下载旁加载应用的故障转储。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/usermode/crashdump
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
packageFullname   | （**必需**）旁加载的应用的程序包的完整名称。
fileName   | （**必需**）要下载的转储文件的名称。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括转储文件。 可以使用 WinDbg 或 Visual Studio 来检查转储文件。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 启用旁加载应用的故障转储

**请求**

可以通过使用以下请求格式来启用旁加载应用的故障转储。
 
方法      | 请求 URI
:------     | :-----
POST | /api/debug/dump/usermode/crashcontrol
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
packageFullname   | （**必需**）旁加载的应用的程序包的完整名称。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 获取检测错误文件列表

**请求**

可以通过使用以下请求格式来获取检测错误小型转储文件列表。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/kernel/dumplist
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括转储文件名称列表和这些文件的大小。 此列表将采用以下格式。 第二个 *FileName* 参数是文件的大小。 这是一个已知 bug。
```
{"DumpFiles": [
    {
        "FileName": string,
        "FileName": string
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 下载检测错误转储文件

**请求**

可以通过使用以下请求格式来下载检测错误转储文件。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/kernel/dump
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
filename   | （**必需**）转储文件的文件名。 通过使用该 API 获取转储列表，可以找到此文件名。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括转储文件。 可以使用 WinDbg 检查此文件。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 获取检测错误故障控制设置

**请求**

可以通过使用以下请求格式来获取检测错误故障控制设置。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/kernel/crashcontrol

<br />
**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括故障控制设置。 有关 CrashControl 的详细信息，请参阅 [CrashControl](https://technet.microsoft.com/library/cc951703.aspx) 文章。 该响应的模板如下所示。
```
{
    "autoreboot": int,
    "dumptype": int,
    "maxdumpcount": int,
    "overwrite": int
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 获取实时内核转储

**请求**

可以通过使用以下请求格式来获取实时内核转储。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/livekernel
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括完整内核模式转储。 可以使用 WinDbg 检查此文件。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 从实时用户进程中获取转储

**请求**

可以通过使用以下请求格式来获取实时用户进程的转储。
 
方法      | 请求 URI
:------     | :-----
GET | /api/debug/dump/usermode/live
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
pid   | （**必需**）关注的进程的唯一进程 ID。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括进程转储。 可以使用 WinDbg 或 Visual Studio 检查此文件。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 设置检测错误故障控制设置

**请求**

可以通过使用以下请求格式来设置收集检测错误数据的设置。
 
方法      | 请求 URI
:------     | :-----
POST | /api/debug/dump/kernel/crashcontrol
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
autoreboot   | （**可选**）True 或 False。 这指示系统在出现故障或锁定后是否自动重新启动。
dumptype   | （**可选**）转储类型。 有关支持的值，请参阅 [CrashDumpType 枚举](https://msdn.microsoft.com/library/azure/microsoft.azure.management.insights.models.crashdumptype.aspx)。
maxdumpcount   | （**可选**）要保存的最大转储数。
overwrite   | （**可选**）True 或 False。 这指示在达到 *maxdumpcount* 指定的转储计数器限制时是否覆盖旧转储。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
## ETW
---
### 通过 WebSocket 创建实时 ETW 会话

**请求**

可以通过使用以下请求格式来创建实时 ETW 会话。 这将通过 WebSocket 进行管理。  ETW 事件会在服务器上进行批处理，并以每秒一次的速度发送到客户端。 
 
方法      | 请求 URI
:------     | :-----
GET/WebSocket | /api/etw/session/realtime
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括已启用提供程序中的 ETW 事件。  请参阅下面的 ETW WebSocket 命令。 

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

### ETW WebSocket 命令
这些命令将从客户端发送到服务器。

命令 | 描述
:----- | :-----
提供程序 *{guid}* 启用 *{level}* | 在指定的级别上启用由 *{guid}*（不带括号）标记的提供程序。 *{level}* 是从 1（最少细节）到 5（详细）的 **int**。
提供程序 *{guid}* 禁用 | 禁用由 *{guid}* 标记（不带括号）的提供程序。

此响应将从服务器发送到客户端。 此响应以文本形式发送，并且你通过解析 JSON 来获取以下格式。
```
{
    "Events":[
        {
            "Timestamp": int,
            "Provider": string,
            "ID": int, 
            "TaskName": string,
            "Keyword": int,
            "Level": int,
            payload objects...
        },...
    ],
    "Frequency": int
}
```

负载对象是在原始 ETW 事件中提供的额外键值对 (string:string)。

示例：
```
{
    "ID" : 42, 
    "Keyword" : 9223372036854775824, 
    "Level" : 4, 
    "Message" : "UDPv4: 412 bytes transmitted from 10.81.128.148:510 to 132.215.243.34:510. ",
    "PID" : "1218", 
    "ProviderName" : "Microsoft-Windows-Kernel-Network", 
    "TaskName" : "KERNEL_NETWORK_TASK_UDPIP", 
    "Timestamp" : 131039401761757686, 
    "connid" : "0", 
    "daddr" : "132.245.243.34", 
    "dport" : "500", 
    "saddr" : "10.82.128.118", 
    "seqnum" : "0", 
    "size" : "412", 
    "sport" : "500"
}
```

---
### 枚举已注册的 ETW 提供程序

**请求**

可以通过使用以下请求格式来枚举已注册的提供程序。
 
方法      | 请求 URI
:------     | :-----
GET | /api/etw/providers
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括 ETW 提供程序列表。 该列表将包含采用以下格式的每个提供程序的友好名称和 GUID。
```
{"Providers": [
    {
        "GUID": string, (GUID)
        "Name": string
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 枚举由平台公开的自定义 ETW 提供程序。

**请求**

可以通过使用以下请求格式来枚举已注册的提供程序。
 
方法      | 请求 URI
:------     | :-----
GET | /api/etw/customproviders
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

200 正常。 该响应包括 ETW 提供程序列表。 该列表将包含每个提供程序的友好名称和 GUID。

```
{"Providers": [
    {
        "GUID": string, (GUID)
        "Name": string
    },...
]}
```

**状态代码**

- 标准状态代码。
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
## 操作系统信息
---
### 获取计算机名称

**请求**

可以通过使用以下请求格式来获取计算机的名称。
 
方法      | 请求 URI
:------     | :-----
GET | /api/os/machinename
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包含采用以下格式的计算机名称。 

```
{"ComputerName": string}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 获取操作系统信息

**请求**

可以通过使用以下请求格式来获取计算机的操作系统信息。
 
方法      | 请求 URI
:------     | :-----
GET | /api/os/info
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包含采用以下格式的操作系统信息。

```
{
    "ComputerName": string,
    "OsEdition": string,
    "OsEditionId": int,
    "OsVersion": string,
    "Platform": string
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 设置计算机名称

**请求**

可以通过使用以下请求格式来设置计算机的名称。
 
方法      | 请求 URI
:------     | :-----
POST | /api/os/machinename
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
name | （**必需**）计算机的新名称。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
## 性能数据
---
### 获取正在运行的进程列表

**请求**

可以通过使用以下请求格式来获取当前正在运行的进程列表。  这也可以升级到 WebSocket 连接，其中相同的 WebSocket 数据将以每秒一次的速度推送到客户端。 
 
方法      | 请求 URI
:------     | :-----
GET | /api/resourcemanager/processes
GET/WebSocket | /api/resourcemanager/processes
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括进程列表以及每个进程的详细信息。 该信息采用 JSON 格式，并且具有以下模板。
```
{"Processes": [
    {
        "CPUUsage": int,
        "ImageName": string,
        "PageFileUsage": int,
        "PrivateWorkingSet": int,
        "ProcessId": int,
        "SessionId": int,
        "UserName": string,
        "VirtualSize": int,
        "WorkingSetSize": int
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 获取系统性能统计信息

**请求**

可以通过使用以下请求格式来获取系统性能统计信息。 这包括诸如读写周期和已使用的内存等信息。
 
方法      | 请求 URI
:------     | :-----
GET | /api/resourcemanager/systemperf
GET/WebSocket | /api/resourcemanager/systemperf
<br />
这还可以升级到 WebSocket 连接。  它以每秒一次的速度提供以下相同的 JSON 数据。 

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包括 CPU 和 GPU 使用率、内存访问以及网络访问之类的系统性能统计信息。 此信息采用 JSON 格式，并且具有以下模板。
```
{
    "AvailablePages": int,
    "CommitLimit": int,
    "CommittedPages": int,
    "CpuLoad": int,
    "IOOtherSpeed": int,
    "IOReadSpeed": int,
    "IOWriteSpeed": int,
    "NonPagedPoolPages": int,
    "PageSize": int,
    "PagedPoolPages": int,
    "TotalInstalledInKb": int,
    "TotalPages": int,
    "GPUData": 
    {
        "AvailableAdapters": [{ (One per detected adapter)
            "DedicatedMemory": int,
            "DedicatedMemoryUsed": int,
            "Description": string,
            "SystemMemory": int,
            "SystemMemoryUsed": int,
            "EnginesUtilization": [ float,... (One per detected engine)]
        },...
    ]},
    "NetworkingData": {
        "NetworkInBytes": int,
        "NetworkOutBytes": int
    }
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
## 电源
---
### 获取当前的电池状态

**请求**

可以通过使用以下请求格式来获取电池的当前状态。
 
方法      | 请求 URI
:------     | :-----
GET | /api/power/battery
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

使用以下格式返回当前电池状态信息。
```
{
    "AcOnline": int (0 | 1),
    "BatteryPresent": int (0 | 1),
    "Charging": int (0 | 1),
    "DefaultAlert1": int,
    "DefaultAlert2": int,
    "EstimatedTime": int,
    "MaximumCapacity": int,
    "RemainingCapacity": int
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT
* 移动设备

---
### 获取活动的电源方案

**请求**

可以通过使用以下请求格式来获取活动的电源方案。
 
方法      | 请求 URI
:------     | :-----
GET | /api/power/activecfg
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

活动的电源方案具有以下格式。
```
{"ActivePowerScheme": string (guid of scheme)}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 获取电源方案的子值

**请求**

可以通过使用以下请求格式来获取电源方案的子值。
 
方法      | 请求 URI
:------     | :-----
GET | /api/power/cfg/*<power scheme path>*
<br />
选项：
- SCHEME_CURRENT

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

可用电源状态的完整列表以应用程序和标志各种电源状态的设置（如电量低和电量严重不足）为基准。 

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 获取系统的电源状态

**请求**

可以通过使用以下请求格式来检查系统的电源状态。 这可让你查看它是否处于低功耗状态。
 
方法      | 请求 URI
:------     | :-----
GET | /api/power/state
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

电源状态信息具有以下模板。
```
{"LowPowerStateAvailable": bool}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 设置活动的电源方案

**请求**

可以通过使用以下请求格式来设置活动的电源方案。
 
方法      | 请求 URI
:------     | :-----
POST | /api/power/activecfg
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
scheme | （**必需**）要设置为系统的活动电源方案的方案 GUID。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 设置电源方案的子值

**请求**

可以通过使用以下请求格式来设置电源方案的子值。
 
方法      | 请求 URI
:------     | :-----
POST | /api/power/cfg/*<power scheme path>*
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
valueAC | （**必需**）用于交流电源的值。
valueDC | （**必需**）用于电池电源的值。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 获取睡眠分析报告

**请求**

方法      | 请求 URI
:------     | :-----
GET | /api/power/sleepstudy/report
<br />
可以通过使用以下请求格式来获取睡眠分析报告。

**URI 参数**
URI 参数 | 说明
:---          | :---
FileName | （**必需**）要下载的文件的完整名称。 此值应采用 hex64 编码。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应是包含睡眠分析的文件。 

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 枚举可用的睡眠分析报告

**请求**

可以通过使用以下请求格式来枚举可用的睡眠分析报告。
 
方法      | 请求 URI
:------     | :-----
GET | /api/power/sleepstudy/reports
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

可用报告的列表具有以下模板。

```
{"Reports": [
    {
        "FileName": string
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
### 获取睡眠分析转换

**请求**

可以通过使用以下请求格式来获取睡眠分析转换。 此转换为 XSLT，可将睡眠分析报告转换为用户可以读取的 XML 格式。
 
方法      | 请求 URI
:------     | :-----
GET | /api/power/sleepstudy/transform
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包含睡眠研究转换。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* IoT

---
## 远程控制
---
### 重新启动目标计算机

**请求**

可以通过使用以下请求格式来重新启动目标计算机。
 
方法      | 请求 URI
:------     | :-----
POST | /api/control/restart
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 关闭目标计算机

**请求**

可以通过使用以下请求格式来关闭目标计算机。
 
方法      | 请求 URI
:------     | :-----
POST | /api/control/shutdown
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
## 任务管理器
---
### 启动现代应用

**请求**

可以通过使用以下请求格式来启动现代应用。
 
方法      | 请求 URI
:------     | :-----
POST | /api/taskmanager/app
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
appid   | （**必需**）要启动的应用的 PRAID。 此值应采用 hex64 编码。
package   | （**必需**）要启动的应用包的完整名称。 此值应采用 hex64 编码。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 停止现代应用

**请求**

可以通过使用以下请求格式来停止现代应用。
 
方法      | 请求 URI
:------     | :-----
DELETE | /api/taskmanager/app
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
package   | （**必需**）要停止的应用包的完整名称。 此值应采用 hex64 编码。
forcestop   | （**可选**）值为 **yes** 指示系统应强制停止所有进程。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
## 网络
---
### 获取当前的 IP 配置

**请求**

可以通过使用以下请求格式来获取当前的 IP 配置。
 
方法      | 请求 URI
:------     | :-----
GET | /api/networking/ipconfig
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

该响应包含采用以下模板的 IP 配置。

```
{"Adapters": [
    {
        "Description": string,
        "HardwareAddress": string,
        "Index": int,
        "Name": string,
        "Type": string,
        "DHCP": {
            "LeaseExpires": int, (timestamp)
            "LeaseObtained": int, (timestamp)
            "Address": {
                "IpAddress": string,
                "Mask": string
            }
        },
        "WINS": {(WINS is optional)
            "Primary": {
                "IpAddress": string,
                "Mask": string
            },
            "Secondary": {
                "IpAddress": string,
                "Mask": string
            }
        },
        "Gateways": [{ (always 1+)
            "IpAddress": "10.82.128.1",
            "Mask": "255.255.255.255"
            },...
        ],
        "IpAddresses": [{ (always 1+)
            "IpAddress": "10.82.128.148",
            "Mask": "255.255.255.0"
            },...
        ]
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

--
### 枚举无线网络接口

**请求**

可以通过使用以下请求格式来枚举可用的无线网络接口。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wifi/interfaces
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

采用以下格式的可用无线接口列表以及详细信息。

``` 
{"Interfaces": [{
    "Description": string,
    "GUID": string (guid with curly brackets),
    "Index": int,
    "ProfilesList": [
        {
            "GroupPolicyProfile": bool,
            "Name": string, (Network currently connected to)
            "PerUserProfile": bool
        },...
    ]
    }
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 枚举无线网络

**请求**

可以通过使用以下请求格式来枚举指定接口上的无线网络列表。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wifi/networks
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
接口   | （**必需**）用于搜索无线网络的网络接口的 GUID，不带括号。 
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

在提供的*接口*上找到的无线网络列表。 这包括采用以下格式的网络详细信息。

```
{"AvailableNetworks": [
    {
        "AlreadyConnected": bool,
        "AuthenticationAlgorithm": string, (WPA2, etc)
        "Channel": int,
        "CipherAlgorithm": string, (e.g. AES)
        "Connectable": int, (0 | 1)
        "InfrastructureType": string,
        "ProfileAvailable": bool,
        "ProfileName": string,
        "SSID": string,
        "SecurityEnabled": int, (0 | 1)
        "SignalQuality": int,
        "BSSID": [int,...],
        "PhysicalTypes": [string,...]
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 建立和断开与 WLAN 网络的连接。

**请求**

可以通过使用以下请求格式来建立或断开与 WLAN 网络的连接。
 
方法      | 请求 URI
:------     | :-----
POST | /api/wifi/network
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
interface   | （**必需**）用于连接到网络的网络接口的 GUID。
op   | （**必需**）指示要执行的操作。 可能的值为 connect 或 disconnect。
ssid   | （**如果 *op* == connect，则为必需**）要连接到的 SSID。
key   | （**如果 *op* == connect 并且网络需要身份验证，则为必需**）共享的密钥。
createprofile | （**必需**）在设备上为网络创建配置文件。  这将导致设备在将来自动连接到该网络。 这可以是**是**或**否**。 

**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
### 删除 WLAN 配置文件

**请求**

可以通过使用以下请求格式来删除与特定接口上的网络关联的配置文件。
 
方法      | 请求 URI
:------     | :-----
DELETE | /api/wifi/network
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
interface   | （**必需**）与要删除的配置文件关联的网络接口的 GUID。
profile   | （**必需**）要删除的配置文件名称。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* Xbox
* HoloLens
* IoT

---
## Windows 错误报告 (WER)
---
### 下载 Windows 错误报告 (WER) 文件

**请求**

可以通过使用以下请求格式来下载 WER 相关的文件。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wer/report/file
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
user   | （**必需**）与报告关联的用户名。
type   | （**必需**）报告的类型。 这可以是 **queried**，也可以是 **archived**。
name   | （**必需**）报告的名称。 这应采用 base64 编码。 
文件   | （**必需**）要从报告下载的文件名称。 这应采用 base64 编码。 
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

- 响应包含所请求的文件。 

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 枚举 Windows 错误报告 (WER) 报告中的文件

**请求**

可以通过使用以下请求格式来枚举 WER 报告中的文件。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wer/report/files
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
user   | （**必需**）与报告关联的用户。
type   | （**必需**）报告的类型。 这可以是 **queried**，也可以是 **archived**。
name   | （**必需**）报告的名称。 这应采用 base64 编码。 
<br />
**请求标头**

- 无

**请求正文**

```
{"Files": [
    {
        "Name": string, (Filename, not base64 encoded)
        "Size": int (bytes)
    },...
]}
```

**响应**

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
### 列出 Windows 错误报告 (WER) 报告

**请求**

可以通过使用以下请求格式来获取 WER 报告。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wer/reports
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

采用以下格式的 WER 报告。

```
{"WerReports": [
    {
        "User": string,
        "Reports": [
            {
                "CreationTime": int,
                "Name": string, (not base64 encoded)
                "Type": string ("Queue" or "Archive")
            },
    },...
]}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 桌面版
* HoloLens
* IoT

---
## Windows Performance Recorder (WPR) 
---
### 使用自定义配置文件开始跟踪

**请求**

可以通过使用以下请求格式来上载 WPR 配置文件，并使用该配置文件开始跟踪。  一次只能运行一个跟踪。 配置文件将不保留在设备上。 
 
方法      | 请求 URI
:------     | :-----
POST | /api/wpr/customtrace
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 包含自定义的 WPR 配置文件的多部分一致 http 正文。

**响应**

采用以下格式的 WPR 会话状态。

```
{
    "SessionType": string, (Running or Idle) 
    "State": string (normal or boot)
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 开始启动性能跟踪会话

**请求**

可以通过使用以下请求格式来开始启动 WPR 跟踪会话。 这也称为性能跟踪会话。
 
方法      | 请求 URI
:------     | :-----
POST | /api/wpr/boottrace
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
profile   | （**必需**）开始时必须使用此参数。 开始性能跟踪会话应使用的配置文件的名称。 可能的配置文件存储在 perfprofiles/profiles.json 中。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

开始时，此 API 会返回采用以下格式的 WPR 会话状态。

```
{
    "SessionType": string, (Running or Idle) 
    "State": string (boot)
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 停止启动性能跟踪会话

**请求**

可以通过使用以下请求格式来停止启动 WPR 跟踪会话。 这也称为性能跟踪会话。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wpr/boottrace
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

- 返回跟踪 ETL 文件。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 开始性能跟踪会话

**请求**

可以通过使用以下请求格式来开始 WPR 跟踪会话。 这也称为性能跟踪会话。  一次只能运行一个跟踪。 
 
方法      | 请求 URI
:------     | :-----
POST | /api/wpr/trace
<br />

**URI 参数**

可以在请求 URI 上指定以下附加参数：

URI 参数 | 说明
:---          | :---
profile   | （**必需**）开始性能跟踪会话应使用的配置文件的名称。 可能的配置文件存储在 perfprofiles/profiles.json 中。
<br />
**请求标头**

- 无

**请求正文**

- 无

**响应**

开始时，此 API 会返回采用以下格式的 WPR 会话状态。

```
{
    "SessionType": string, (Running or Idle) 
    "State": string (normal)
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 停止性能跟踪会话

**请求**

可以通过使用以下请求格式来停止 WPR 跟踪会话。 这也称为性能跟踪会话。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wpr/trace
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

- 返回跟踪 ETL 文件。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT

---
### 检索跟踪会话的状态

**请求**

可以通过使用以下请求格式来检索当前 WPR 会话的状态。
 
方法      | 请求 URI
:------     | :-----
GET | /api/wpr/status
<br />

**URI 参数**

- 无

**请求标头**

- 无

**请求正文**

- 无

**响应**

采用以下格式的 WPR 跟踪会话的状态。

```
{
    "SessionType": string, (Running or Idle) 
    "State": string (normal or boot)
}
```

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 正常
4XX | 错误代码
5XX | 错误代码
<br />
**可用设备系列**

* Windows 移动版
* Windows 桌面版
* HoloLens
* IoT


<!--HONumber=May16_HO2-->


