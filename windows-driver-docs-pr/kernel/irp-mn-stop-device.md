---
title: IRP_MN_STOP_DEVICE
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: a5c81db0-e753-4d91-97e4-c58ea05f5ce8
keywords:
- IRP_MN_STOP_DEVICE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: d51e1856e9bb4b97d93a56cb59cba07c3fe58577
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533926"
---
# <a name="irpmnstopdevice"></a>IRP\_MN\_STOP\_DEVICE


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，若要停用设备，因此它可以重新配置设备的硬件资源。

在 Windows 2000 和更高版本的系统，即插即用管理器发送 IRP 才前面[ **IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)完成已成功。

在 Windows 98 上 / 我，PnP 管理器还会发送此 IRP 时设备正在停用状态，当失败设备堆栈**IRP\_MN\_启动\_设备**请求。 在失败的启动的情况下，即插即用管理器将此 IRP 发送前面不带[ **IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)请求。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序必须设置**Irp-&gt;IoStatus.Status**于状态\_成功。

<a name="operation"></a>操作
---------

此 IRP 是首先处理设备堆栈顶部驱动程序，然后向下传递到堆栈中每个较低的驱动程序。

为此 IRP、 Windows 2000 和更高版本的驱动程序的响应中停用设备并释放正在使用的设备，例如 I/O 端口并中断任何硬件资源。

在 Windows 2000 及更高版本，停止 IRP 只用来释放设备的硬件资源，以便可以重新配置。 一旦重新配置资源，是重启设备。 停止 IRP 不是删除 IRP 的前提。 请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)有关中的 PnP Irp 的订单详细信息发送到设备。

在 Windows 98 上 / 我停止 IRP 也使用失败的启动后，设备将被禁用。 在这些操作系统运行的 WDM 驱动程序应停用设备、 故障任何传入的 I/O，并禁用和取消注册任何用户模式接口。

驱动程序不得失败此 IRP。 如果驱动程序无法释放设备的硬件资源，则必须失败前面的查询停止 IRP。

请参阅[停止设备](https://msdn.microsoft.com/library/windows/hardware/ff563868)有关处理的详细信息停止 Irp。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

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
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)

[**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)

[**IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)

[**IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)

 

 



