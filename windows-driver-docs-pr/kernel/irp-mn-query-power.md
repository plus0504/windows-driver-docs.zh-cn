---
title: IRP_MN_QUERY_POWER
description: 此 IRP 将查询设备，以确定是否可以更改系统电源状态或设备电源状态。
ms.date: 08/12/2017
ms.assetid: fc4c5364-2160-4525-889a-96785a3c7a07
keywords:
- IRP_MN_QUERY_POWER 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: fac293187ca2abfaa7ab07fb2e8054c77d8601bf
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922530"
---
# <a name="irp_mn_query_power"></a>IRP\_MN\_查询\_能力


此 IRP 将查询设备，以确定是否可以更改系统电源状态或设备电源状态。

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_POWER**](irp-mj-power.md)

<a name="when-sent"></a>发送时间
---------

电源管理器或设备电源策略所有者发送此 IRP，以确定它是否可以更改系统或设备电源状态，通常为 "休眠"。 驱动程序必须调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)来分配并发送此 IRP。

对于在 PDO 中设置 DO\_\_power\_PAGABLE 标志的设备堆栈，电源管理器以 IRQL = 被动级别发送此 IRP。

如果设置了 "DO\_\_power\_浪涌" 标志，则电源管理器可以以 IRQL 为间隔发送 IRP。 此类驱动程序不能直接或间接访问任何分页的代码或数据。

## <a name="input-parameters"></a>输入参数


**Power. Type**指定所设置的电源状态的类型（ **SystemPowerState**或**DevicePowerState**）。

**参数。 power. state**指定电源状态，如下所示：

-   如果**SystemPowerState**，则值为[**系统\_\_电源状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)类型的枚举**器。**

-   如果**DevicePowerState**，则值为[**设备\_\_电源状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)类型的枚举**器。**

**ShutdownType**指定有关所请求转换的其他信息。 可能的值是**电源\_操作**类型的枚举器。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将**Irp-&gt;IOSTATUS**设置为状态\_"成功" 以指示设备可以进入请求的状态。 驱动程序将设置任何适当的故障状态，以指示它无法进入请求的状态。

<a name="operation"></a>操作
---------

**Irp\_MN\_查询\_功能**的参数与[**irp\_MN\_设置\_的电源**](irp-mn-set-power.md)参数相同。 但不是向驱动程序通知电源状态的不可撤消的更改，**而\_使用\_IRP\_MN QUERY power**查询系统或设备是否可以进入特定电源状态。

驱动程序不得更改其设备的电源状态以响应**IRP\_\_MN QUERY\_power** request。

驱动程序在 Windows Server 2003、Windows XP 和 Windows 2000 上收到**IRP\_MN\_QUERY\_POWER** request 之后，驱动程序必须调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，如[调用**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/calling-postartnextpowerirp)中所述。 从 Windows Vista 开始，不需要调用**PoStartNextPowerIrp** ，此类调用不执行任何电源管理操作。

**IRP\_MN\_系统\_电源状态的查询能力**

电源管理器发送此 IRP，以确保它可以更改系统电源状态，而不会中断工作，如丢弃网络连接。

如果可能，在发送**IRP\_\_MN 设置\_电源**之前，电源管理器会查询以请求系统睡眠状态或正常系统关闭。 但是，在某些关键条件下（例如，用户按下 "**关闭电源**" 按钮或电池过期），在未首先发送查询电源请求的情况下，电源管理器可能会发送**IRP\_\_MN 设置\_电源**请求。 仅限睡眠状态的电源管理器查询;它永远不会在返回到工作状态之前进行查询。

当驱动程序收到系统 power query IRP 时，如果该驱动程序无法支持对查询的系统状态有效的任何设备状态，则它应失败 IRP。 有关详细信息，请参阅[**DeviceState**](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)。 否则，驱动程序应将 IRP 传递到下一个较低版本的驱动程序。 总线驱动程序完成 IRP。

从 Windows Vista 开始，转换到系统睡眠状态被视为一种关键操作。 尽管驱动程序可能无法通过系统查询-power IRP，电源管理器可能仍会将系统电源状态更改为睡眠状态。 驱动程序收到系统查询-power IRP 后，应该始终准备好驱动程序，以便在系统电源状态下进行后续更改。

当设备电源策略所有者收到系统 power query IRP 时，它应在 IRP 中设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，然后将其向下传递。 在*IoCompletion*例程中，它应为对查询的系统状态有效的设备状态发送**IRP\_\_MN 查询\_能力**。 有关详细信息，请参阅[在设备电源策略所有者中处理系统查询-POWER IRP](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-a-system-query-power-irp-in-a-device-power-policy-owner)。

当 IRP 指定**PowerSystemShutdown** （S5）时， **ShutdownType**中的值将提供关闭的原因。 **ShutdownType**告知驱动程序系统是重置（**PowerActionShutdownReset**）还是无限期关机以稍后重新启动（**PowerActionShutdownOff**）。 对于大多数设备的驱动程序，差别是无关紧要。 但是，对于某些设备，如执行 DMA 的视频流式处理设备，驱动程序可能会选择在重置系统时关闭设备的电源，从而停止任何正在进行的 i/o。

在 Microsoft Windows 2000 及更高版本的系统上， **ShutdownType**的值也可以是**PowerActionShutdown**。 在这种情况下，驱动程序无法判断请求哪种类型的关闭，因此应继续进行重置。

如果驱动程序对系统电源状态的**\_irp\_MN QUERY\_POWER**请求失败，则电源管理器通常会通过发出**IRP\_MN\_\_电源**irp 来做出响应。 通常，此 IRP 将重申当前系统状态。 但是，驱动程序可能会接收到所查询状态或其他中间状态的**IRP\_\_MN 设置\_的电源**。 驱动程序应准备好处理这些情况。

**IRP\_MN\_查询\_电源状态**

设备电源策略所有者将此 IRP 发送到其堆栈，以响应系统**IRP\_\_MN QUERY\_power** request。

如果驱动程序可以将其设备置于请求的设备状态，它会将**IoStatus**设置为状态\_SUCCESS，并将 irp 向下传递到下一个较低的驱动程序，依此类推，直到 IRP 达到总线驱动程序。 如果堆栈中的任何驱动程序必须使 IRP 失败，则该驱动程序应立即通过调用**IoCompleteRequest**并返回失败状态来完成 irp。 IRP 失败的驱动程序不会沿堆栈进一步向下传递。

通过返回状态\_SUCCESS，驱动程序可保证它不会启动任何会更改其设置请求电源状态的功能的操作。 驱动程序应该将需要此类操作的任何 Irp 排队，直到它完成将设备恢复到可接受电源状态的集电源 IRP。

在 Windows 2000 和更高版本的系统上，当 IRP 指定**PowerDeviceD1**、 **PowerDeviceD2**或**PowerDeviceD3**时，**参数. ShutdownType**中的值提供有关当前系统电源 irp 的信息（如果系统电源 irp 处于活动状态）。 在这种情况下， **ShutdownType**处的值表示当前请求的系统电源状态，或者，如果系统请求未完成，则为**PowerActionNone** 。 在 Windows 98/Me 上，当 IRP 请求设备电源状态时，此字段始终包含**PowerActionNone** 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IRP\_MN\_查询\_能力**](irp-mn-query-power.md)

[**IRP\_MN\_设置\_电源**](irp-mn-set-power.md)

[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)

 

 




