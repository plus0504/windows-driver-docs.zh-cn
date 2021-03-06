---
title: 管理上下文
description: 管理上下文
ms.assetid: 1ad33c6c-a5dd-4b65-bfcc-a40453d3a6b5
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，上下文
- 文件系统微筛选器驱动程序 WDK，上下文
- 微筛选器驱动程序 WDK，上下文
- 上下文 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdeff72eaa35daca18476289f3e92735c99829ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841130"
---
# <a name="managing-contexts"></a>管理上下文


筛选器管理器使微筛选器驱动程序可以将上下文与对象相关联，以便在 i/o 操作之间保持状态。 可以具有上下文的对象包括卷、实例、流和流句柄。

第三方文件系统必须使用[**FSRTL\_ADVANCED\_FCB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)结构（而不是[**FSRTL\_常见\_FCB\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_common_fcb_header)结构），才能正常使用 stream 和流句柄上下文.

上下文可以从分页或非分页池分配，但必须从非分页池分配的卷上下文除外。

释放所有未完成的引用后，上下文会自动释放。 如果微筛选器驱动程序定义上下文清理回调例程，筛选器管理器将在释放上下文之前调用例程。

筛选器管理器负责在删除关联的对象、分离实例以及卸载微筛选器驱动程序时删除上下文。

如果微筛选器驱动程序仅支持每个卷一个实例，请使用实例上下文而不是卷上下文来提高性能。 你还可以通过将指向微筛选器驱动程序实例上下文的指针存储在流或流句柄上下文中来提高性能。

页面文件或以下操作中不支持上下文：

-   创建请求的 Preoperation 处理

-   关闭请求的 Postoperation 处理

-   处理 IRP\_MJ\_网络\_查询\_打开请求

有关使用上下文的微筛选器驱动程序的示例，请参阅 CTX 示例。

### <a name="span-idfilter_manager_routines_for_context_managementspanspan-idfilter_manager_routines_for_context_managementspanspan-idfilter_manager_routines_for_context_managementspanfilter-manager-routines-for-context-management"></a><span id="Filter_Manager_Routines_for_Context_Management"></span><span id="filter_manager_routines_for_context_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>用于上下文管理的筛选器管理器例程

筛选器管理器提供以下用于创建、注册和设置上下文的支持例程：

[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)

[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)

[**FltSetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)

[**FltSetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamcontext)

[**FltSetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamhandlecontext)

[**FltSetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetvolumecontext)

提供以下例程用于查询上下文支持：

[**FltSupportsStreamContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)

[**FltSupportsStreamHandleContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)

提供以下例程用于获取和引用上下文：

[**FltGetContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetcontexts)

[**FltGetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetinstancecontext)

[**FltGetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamcontext)

[**FltGetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)

[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)

[**FltReferenceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext)

提供以下例程用于发布和删除上下文：

[**FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)

[**FltDeleteInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeleteinstancecontext)

[**FltDeleteStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamcontext)

[**FltDeleteStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamhandlecontext)

[**FltDeleteVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletevolumecontext)

[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)

[**FltReleaseContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontexts)

### <a name="span-idminifilter_driver_callback_routines_for_context_managementspanspan-idminifilter_driver_callback_routines_for_context_managementspanspan-idminifilter_driver_callback_routines_for_context_managementspanminifilter-driver-callback-routines-for-context-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Context_Management"></span><span id="minifilter_driver_callback_routines_for_context_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>上下文管理的微筛选器驱动程序回调例程

以下回调例程存储在[**FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构中，该结构作为参数传递给用于管理上下文的微微筛选器驱动程序的[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) ：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调例程名称</th>
<th align="left">回调例程类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ContextAllocateCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_allocate_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_ALLOCATE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_allocate_callback)"><strong>PFLT_CONTEXT_ALLOCATE_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_CLEANUP_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)"><strong>PFLT_CONTEXT_CLEANUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ContextFreeCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_free_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_FREE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_free_callback)"><strong>PFLT_CONTEXT_FREE_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




