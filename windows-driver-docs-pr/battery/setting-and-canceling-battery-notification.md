---
title: 设置和取消电池通知
description: 设置和取消电池通知
ms.assetid: bd0920f0-9f3f-47f7-b1a7-29ec233e93ff
keywords:
- 电池通知 WDK
- 电池 miniclass 驱动程序 WDK，通知
- 通知 WDK 电池
- 电池类驱动程序 WDK，通知
- 正在取消电池通知
- 正在停止电池通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 981e34f9f4f919806cb4ce501be235697f0fc237
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364734"
---
# <a name="setting-and-canceling-battery-notification"></a>设置和取消电池通知


## <span id="ddk_setting_and_canceling_battery_notification_dg"></span><span id="DDK_SETTING_AND_CANCELING_BATTERY_NOTIFICATION_DG"></span>


Miniclass 驱动程序提供了[ *BatteryMiniSetStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)例程，以便在类驱动程序可以请求特定条件的通知。 例程声明，如下所示：

```cpp
typedef
NTSTATUS
(*BCLASS_SET_STATUS_NOTIFY)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    IN PBATTERY_NOTIFY BatteryNotify
    );
```

*上下文*参数是指向 miniclass 驱动程序分配和传递给电池中的类驱动程序的上下文区域\_微型端口\_在设备初始化信息结构。 *BatteryTag*参数是前面返回的值[ *BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)。

*BatteryNotify*参数包含一组标志，指示电池电源条件和值对的 ULONG，用于定义可接受的电池容量的范围。 当电池不再满足指定的电源条件或其容量会高于或低于指定的范围内时，应调用 miniclass 驱动程序[ **BatteryClassStatusNotify**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassstatusnotify)。

*BatteryMiniSetStatusNotify*应返回状态\_不\_支持任何条件或无法确定此电池的触发器值。

类驱动程序调用[ *BatteryMiniDisableStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)例程，以取消以前所请求的 BatteryMiniSetStatusNotify 电池状态更改通知。 此例程声明，如下所示：

```cpp
typedef
NTSTATUS
(*BCLASS_DISABLE_STATUS_NOTIFY)(
    IN PVOID Context
    );
```

*上下文*参数是指向由 miniclass 驱动程序分配，并传递给电池中的类驱动程序的上下文区域\_微型端口\_在设备初始化信息结构。

Miniclass 驱动程序可以省略这两个例程的功能和状态\_不\_受支持。 但是，miniclass 驱动程序提供*BatteryMiniSetStatusNotify*例程必须提供相应*BatteryMiniDisableStatusNotify*例程，反之亦然。

 

 




