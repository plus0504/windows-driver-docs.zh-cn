---
title: 智能卡驱动程序调试
description: 智能卡驱动程序调试
ms.assetid: 701528f6-d8ba-4a73-ad68-cb35497a3474
keywords:
- 智能卡驱动程序 WDK，调试
- 调试驱动程序 WDK 智能卡
- DebugLevel
- 供应商提供的驱动程序 WDK 智能卡，调试
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5512a2a8bb632abe73d3763dc75634a7a083834c
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428324"
---
# <a name="smart-card-driver-debugging"></a>智能卡驱动程序调试

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

智能卡驱动程序库支持多种调试功能。 每个调试功能由以下常量之一表示，这些常量是在*Smclib*头文件中定义的：

```cpp
DEBUG_IOCTL
DEBUG_ATR
DEBUG_PROTOCOL
DEBUG_DRIVER
DEBUG_TRACE
DEBUG_ERROR
DEBUG_BREAK
DEBUG_ALL
```

启用的调试功能的组合集由一个称为*调试级别*的值表示。 您可以通过采用与要启用的功能对应的常量的按位 OR 来计算此值。

可以通过两种方式设置调试级别。 首先，可以使用 Windows 驱动程序工具包（WDK）随附的智能卡驱动程序测试程序*Scdrvtst*。 第二种是使用[**SmartcardSetDebugLevel**](https://docs.microsoft.com/previous-versions/ff548960(v=vs.85))智能卡驱动程序库例程。

在这两种情况下，必须将所需的调试级别的值传递到设置调试级别的程序或例程。 例如，若要使用智能卡库例程从驱动程序设置调试级别，请执行以下调用：

```cpp
SmartcardSetDebugLevel(DebugLevel);
```

若要从读取器驱动程序写入调试消息，驱动程序必须调用以下例程：

```cpp
SmartcardDebug(
 ULONG DebugLevel,
 PCHAR Message
);
```

> [!IMPORTANT]
> 您必须安装所选版本的操作系统和该驱动程序的已检查版本，才能获取调试消息。

此例程还可用于通过以下方式将消息写入远程调试器。

- 若要编写错误消息，请使用 \_ *DEBUGLEVEL*的调试错误常量。

- 若要写入标准驱动程序消息，请使用调试 \_ 驱动程序常量。

- 若要编写指示读取器驱动程序何时进入或退出例程的跟踪消息，请使用调试 \_ 跟踪作为*DebugLevel*。

开发驱动程序时，请使用所选的智能卡驱动程序库版本，并使用**SmartcardSetDebugLevel** \_ *DriverEntry*例程中的 SmartcardSetDebugLevel （调试全部）将调试级别设置为最大值。

有关设置远程调试会话的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。
