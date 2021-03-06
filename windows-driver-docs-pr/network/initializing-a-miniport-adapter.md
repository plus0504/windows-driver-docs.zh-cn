---
title: 初始化微型端口适配器
description: 初始化微型端口适配器
ms.assetid: 6d7a23dc-cc09-46d3-89d3-34e8e8f17a51
keywords:
- 微型端口适配器 WDK 网络，初始化
- 适配器 WDK 网络，初始化
- 初始化微型端口适配器
- 正在初始化状态 WDK 网络
- MiniportInitializeEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d605fee54fccb3faf35249c39ca5275f2e0fe995
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824596"
---
# <a name="initializing-a-miniport-adapter"></a>初始化微型端口适配器





当网络设备可用时，系统会加载所需的 NDIS 微型端口驱动程序（如果尚未加载）。 然后，即插即用（PnP）管理器将 NDIS a 即插即用 IRP 发送到该设备。 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数为网络 i/o 操作初始化适配器。 初始化驱动程序后，可以随时调用*MiniportInitializeEx* 。 有关微型端口驱动程序初始化的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)返回之前，NDIS 不会提交正在初始化的适配器的请求。 适配器处于 "正在初始化" 状态。

小型小型驱动程序通常在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)中执行以下任务：

1.  获取适配器的配置信息。

2.  获取有关适配器的硬件资源的信息。

3.  调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)并提供与适配器关联的以下属性：
    -   指向驱动程序分配的上下文区域的指针。
    -   适当的属性标志。
    -   调用其[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)函数的超时间隔。
    -   接口类型。

4.  初始化特定于适配器的资源。

微型端口驱动程序在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)中指定适配器属性\_特性结构， [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)将其传递到[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)。

通常， [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)按以下顺序分配适配器特定的资源：

1.  非分页池内存。

2.  [**Net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)和[**net\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)池（请参阅[微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md)）。

3.  旋转锁。

4.  后续.

5.  IO 端口。

6.  DMA （请参阅[散点/聚集 DMA](scatter-gather-dma2.md)）。

7.  共享内存。

8.  中断（请参阅[管理中断](managing-interrupts.md)）。

在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)成功返回后，适配器将处于暂停状态。 NDIS 可以调用[**MiniportRestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)函数将适配器转换为正在运行状态。 有关详细信息，请参阅[启动微型端口适配器](starting-an-adapter.md)。

如果[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)返回 NDIS\_状态\_SUCCESS，则驱动程序应释放[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数中适配器的所有资源。 有关详细信息，请参阅[停止微型端口适配器](halting-a-miniport-adapter.md)。

如果[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)失败，则*MiniportInitializeEx*必须释放它在返回前分配的所有资源，并将适配器恢复到停止状态。

## <a name="related-topics"></a>相关主题


[停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md)

[散点/集合 DMA](scatter-gather-dma2.md)

[启动微型端口适配器](starting-an-adapter.md)

 

 






