---
title: 将虚拟地址映射到内存段
description: 将虚拟地址映射到内存段
ms.assetid: 3ff64e33-eceb-4603-a3d9-11cb2f7dac85
keywords:
- 内存段 WDK 显示，映射虚拟地址
- 映射虚拟地址
- 虚拟地址映射 WDK 显示
- CPU 虚拟地址映射 WDK 显示
- 线性口径-空间段 WDK 显示
- 口径空间段 WDK 显示
- 线性内存空间段 WDK 显示
- 内存空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 831f2687c6c2bae43c9b2c7ac33b3aff80a8d35b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840581"
---
# <a name="mapping-virtual-addresses-to-a-memory-segment"></a>将虚拟地址映射到内存段


## <span id="ddk_mapping_virtual_addresses_to_a_memory_segment_gg"></span><span id="DDK_MAPPING_VIRTUAL_ADDRESSES_TO_A_MEMORY_SEGMENT_GG"></span>


显示微型端口驱动程序可以指定它定义的每个内存空间或口径区段，无论 CPU 虚拟地址是否可通过设置标志中的**CpuVisible**位域标志直接映射到位于该段中的分配段的[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)结构的成员。

若要将 CPU 虚拟地址映射到段，段应具有通过 PCI 口径的线性访问。 换句话说，段内任何分配的偏移量应与 PCI 口径中的偏移量相同。 因此，视频内存管理器可以根据分配在给定段内的偏移量来计算任何分配的与总线相关的物理地址。

下图说明了如何将虚拟地址映射到线性内存空间段。

![说明映射到线性内存空间段的虚拟地址的关系图](images/vrtlmap.png)

下图说明了如何将虚拟地址映射到线性口径段的基础页。

![说明映射到线性口径区基础页的虚拟地址的关系图](images/vrtlmap2.png)

在将虚拟地址映射到部分段之前，视频内存管理器会调用显示微型端口驱动程序的[**DxgkDdiAcquireSwizzlingRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)函数，以便驱动程序可以设置用于访问分配的位的口径这可能是 swizzled 的。 驱动程序可以将偏移量更改为在其中访问分配的 PCI 口径，也不会更改为在口径中占用的空间量。 如果该驱动程序不能使分配 CPU 可访问（例如，硬件可能用尽了 unswizzling 口径），视频内存管理器将逐出分配到系统内存，并使应用程序可以访问其中的位。

如果在用户模式显示驱动程序调用[**pfnLockCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数来请求直接访问内存时，先前创建的分配的内容在系统内存中，则视频内存管理器会将系统内存缓冲区返回给用户模式显示驱动程序和显示微型端口驱动程序不涉及访问分配。 因此，该分配的内容不会被显示微型端口驱动程序修改，并且仍采用 unswizzled 格式。 这意味着，从视频内存中收回 CPU 可访问的分配时，显示微型端口驱动程序必须 unswizzle 分配，以便应用程序可以直接访问生成的系统内存位。

如果逐出了与当前为直接应用程序访问映射的分配关联的 GPU 资源，则分配的内容将传输到系统内存中，以便应用程序可以继续访问同一虚拟上的内容。地址但不同的物理介质。 若要设置传输，视频内存管理器会调用显示微型端口驱动程序的[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数来创建分页缓冲区，并且 GPU 计划程序将调用驱动程序的[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数来对分页进行排队向 GPU 执行单元缓冲。 特定于硬件的传输命令在分页缓冲区中。 有关详细信息，请参阅[提交命令缓冲区](submitting-a-command-buffer.md)。 视频内存管理器可确保视频到系统内存的转换对应用程序不可见。 但是，驱动程序必须确保在逐出分配时，通过 PCI 口径的分配的字节顺序与分配的字节顺序完全匹配。

对于口径区，分配的基础位已经在系统内存中，因此不需要在逐出过程中进行数据传输（unswizzling）。 因此，如果可由应用程序直接访问，则位于口径区内的 CPU 可访问的分配不能 swizzled。

如果某个图面可以由应用程序通过 CPU 直接访问，但会在 swizzled 段中被视为，则显示驱动程序应将曲面实现为两个不同的分配。 当用户模式显示驱动程序创建这样的图面时，它可以调用[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数，并可以将 D3DDDICB 的**NumAllocations**成员设置为2，将[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)的**pPrivateDriverData**成员设置为D3DDDICB 的**pAllocationInfo**数组中的[**D3DDDI\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)结构\_分配，以指向有关分配的专用数据（如其 swizzled 和 unswizzled 格式）。 GPU 将使用的分配包含 swizzled 格式的位，并且应用程序将访问的分配包含 unswizzled 格式的位。 视频内存管理器调用显示微型端口驱动程序的[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数来创建分配。 显示微型端口驱动程序会在从用户模式显示驱动程序传递的每个分配的[**DXGK\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的**pPrivateDriverData**成员中解释专用数据。 视频内存管理器不识别分配的格式;它只为分配分配特定大小和对齐的内存块。 调用用户模式显示驱动程序的*锁*函数以锁定图面以进行处理会导致以下操作：

1.  用户模式显示驱动程序调用[**pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)函数，将命令缓冲区中的 unswizzle 操作提交到 Direct3D 运行时，并将其提交到显示微型端口驱动程序。

2.  用户模式显示驱动程序调用[**pfnLockCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数来锁定 unswizzled 分配。 请注意，用户模式显示驱动程序不得在 D3DDDICB\_锁定结构的**Flags**成员中设置 D3DDDILOCKCB\_DONOTWAIT 标志。

3.  **PfnLockCb**函数将等待，直到执行分配之间的传输（unswizzling）。

4.  **PfnLockCb**函数请求显示微型端口驱动程序为 unswizzled 分配获取虚拟地址，并将虚拟地址返回到[**D3DDDICB\_锁定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_lock)的**pData**成员中的用户模式显示驱动程序。

5.  用户模式显示驱动程序将 unswizzled 分配的虚拟地址返回到 D3DDDIARG\_锁定的**pSurfData**成员中的应用程序。

 

 





