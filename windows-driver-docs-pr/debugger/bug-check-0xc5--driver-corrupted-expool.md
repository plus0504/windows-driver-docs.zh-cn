---
title: Bug 检查 0xC5 DRIVER_CORRUPTED_EXPOOL
description: DRIVER_CORRUPTED_EXPOOL bug 检查的值为0x000000C5。 这表示系统尝试在进程 IRQL 上访问无效内存，但该进程的 IRQL 太高。
ms.assetid: e375e7d3-9cb1-474f-ade2-1bc65dd79864
keywords:
- Bug 检查 0xC5 DRIVER_CORRUPTED_EXPOOL
- DRIVER_CORRUPTED_EXPOOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_EXPOOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08a9d8ed31366747b6f3c4aa76210ad2c7df4ab9
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534790"
---
# <a name="bug-check-0xc5-driver_corrupted_expool"></a>Bug 检查0xC5：驱动程序 \_ 损坏 \_ EXPOOL


驱动程序 \_ 损坏的 \_ EXPOOL bug 检查的值为0x000000C5。 这表示系统尝试在进程 IRQL 上访问无效内存，但该进程的 IRQL 太高。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driver_corrupted_expool-parameters"></a>驱动程序 \_ 损坏的 \_ EXPOOL 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>引用时为 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0：</strong>读取</p>
<p><strong>1：</strong>写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>对引用的内存进行寻址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

当 IRQL 太大时，内核试图访问可分页内存（或可能是完全无效的内存）。 此问题的最终原因几乎肯定是损坏了系统池的驱动程序。

在大多数情况下，如果驱动程序损坏了小型分配（小于页面大小），则会检查此错误 \_ 。 较大的分配导致[**错误检查 0xD0**](bug-check-0xd0--driver-corrupted-mmpool.md) （驱动程序 \_ 损坏 \_ MMPOOL）。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 如果最近安装了任何新软件，请检查是否已正确安装。 查看制造商网站上的已更新驱动程序。

若要调试此错误，请使用驱动程序验证程序的特殊池选项。 如果这无法显示导致错误的驱动程序，请使用全局标志实用工具启用 "按池的特殊池" 标记。

有关特殊池的信息，请参阅 Windows 驱动程序工具包的[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)部分。

 

 




