---
title: 停止 NIC
description: 停止 NIC
ms.assetid: 033b45bd-fbe9-4a40-84e6-b9447370b17f
keywords:
- Nic WDK 网络，停止
- 网络接口卡 WDK 网络，停止
- 即插即用 WDK NDIS 微型端口，停止 NIC
- 停止 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4639540bad0cb7ed91b4e564983839f3c60ca13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841821"
---
# <a name="stopping-a-nic"></a>停止 NIC





PnP 管理器停止 NIC，使其可以重新配置或重新平衡分配给 NIC 的硬件资源。 以下步骤描述了 NDIS 如何参与 NIC 的停止：

1.  PnP 管理器颁发[**IRP\_MN\_QUERY\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)请求。

2.  当 NDIS 接收到此 IRP 时，它会调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventQueryRemoveDevice**的事件代码。

    **请注意**  NDIS 仅对播发[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数入口点的筛选器驱动程序执行此步骤。 筛选器驱动程序在调用[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数时公布此入口点。

     

3.  在对其[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的调用上下文中，筛选器驱动程序必须调用[**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将**NetEventQueryRemoveDevice**事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用**NetEventQueryRemoveDevice**的事件代码调用该筛选器驱动程序的*FilterNetPnPEvent*函数。

    **请注意**  NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的入口点。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发了**NetEventQueryRemoveDevice**事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventQueryRemoveDevice**的事件代码。

5.  如果协议驱动程序通过从*ProtocolNetPnPEvent*返回失败代码， **NetEventQueryRemoveDevice**事件失败，NDIS 或 PnP 管理器可能会忽略失败，并随后成功\_MN\_查询\_停止\_设备请求。 因此，协议驱动程序必须准备好处理 NIC 的删除操作，即使协议驱动程序无法**NetEventQueryRemoveDevice**事件。

6.  PnP 管理器发出[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)请求，停止设备或[**IRP\_MN\_取消\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)请求取消挂起的停止。

7.  如果 PnP 管理器颁发 IRP\_MN\_CANCEL\_停止\_设备请求，NDIS 将调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventCancelRemoveDevice**的事件代码。

    **请注意**  NDIS 仅对播发[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数入口点的筛选器驱动程序执行此步骤。

     

8.  在对其[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的调用上下文中，筛选器驱动程序必须调用[**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将**NetEventCancelRemoveDevice**事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用**NetEventCancelRemoveDevice**的事件代码调用该筛选器驱动程序的*FilterNetPnPEvent*函数。

    **请注意**  NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的入口点。

     

9.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发了**NetEventCancelRemoveDevice**事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventCancelRemoveDevice**的事件代码。

10. 如果 PnP 管理器颁发 IRP\_MN\_停止\_设备请求，NDIS 会执行以下步骤：

    1.  它暂停绑定到 NIC 的所有协议驱动程序。

    2.  它将暂停附加到 NIC 的所有筛选器驱动程序。

    3.  它暂停 NIC 的微型端口驱动程序。

    4.  它调用绑定到 NIC 的所有协议驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。

    5.  它调用附加到 NIC 的所有筛选器模块的[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)函数。

11. 在所有协议和筛选器驱动程序未绑定并从 NIC 分离后，NDIS 将调用微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。 NDIS 将*MiniportHaltEx*的*HaltAction*参数设置为**NdisHaltDeviceStopped**。

12. 当处理 IRP\_MN\_停止\_设备请求时，NDIS 不会销毁在调用*AddDevice*例程时为 NIC 创建的功能设备对象（FDO）。 仅在收到[**IRP\_MN\_删除 NIC\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求后，NDIS 销毁设备对象。

    如果 PnP 管理器颁发了 IRP\_MN\_启动\_设备重新启动 NIC，NDIS 将重复使用之前为 NIC 创建的 FDO。 然后，NDIS 将重新启动 NIC。 有关此过程的详细信息，请参阅[启动 NIC](starting-a-nic.md)。

 

 





