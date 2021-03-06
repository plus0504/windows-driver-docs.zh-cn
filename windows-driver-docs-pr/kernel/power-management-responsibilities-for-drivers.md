---
title: 驱动程序的电源管理责任
description: 驱动程序的电源管理责任
ms.assetid: c42a5b95-76f3-4975-b452-4858bbbe532e
keywords:
- 电源管理 WDK 内核，驱动程序的职责
- 驱动程序 power 职责 WDk 内核
- 节省电源 WDK 内核
- 电源管理 WDK 内核，电源状态
- 电源状态 WDK 内核
- 指出 WDK 电源管理
- 系统电源状态 WDK 内核，电源管理
- 设备电源状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c97fe28aec37109a93bf68e5d98c79cefd44074
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374198"
---
# <a name="power-management-responsibilities-for-drivers"></a>驱动程序的电源管理责任





支持电源管理的驱动程序负责：

[报告设备电源功能](reporting-device-power-capabilities.md)期间枚举即插即用。

[设置电源管理的设备对象标志](setting-device-object-flags-for-power-management.md)。

[处理 power Irp](handling-power-irps.md)发送的电源管理器或驱动程序。

[打开设备电源](powering-up-a-device.md)立即在系统启动时或空闲时关闭后仍需要。

[关闭设备](powering-down-a-device.md)在系统空闲关闭时间或使其进入睡眠状态时。

[启用设备唤醒](enabling-device-wake-up.md)，如果设备支持唤醒功能。

[管理设备性能状态](managing-device-performance-states.md)，如果设备支持不断降低性能或功能以降低能耗。

每个设备堆栈中的不是每个驱动程序执行所有这些任务。 通常情况下，总线驱动程序报告功能、 设置标志，和操作的物理设备和设备电源策略管理器 （通常是功能驱动程序） 发出请求以将设备进入睡眠状态并启用唤醒。

几个例外情况之外，驱动程序电源上和他们的设备，打开和关闭电源，然后它们启用设备进行电源 Irp，即，使用的主要代码 Irp 响应唤醒[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power). Power Irp 可以由驱动程序通过电源管理器，然后在某些情况下，发送。

 

 




