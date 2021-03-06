---
title: OID_WDI_SET_PRIVACY_EXEMPTION_LIST
description: 主机使用 OID_WDI_SET_PRIVACY_EXEMPTION_LIST 提供的有关数据包说明的例外列表。 该适配器适用于指定例外的 IEEE EtherType 值匹配的数据包接收这些例外。
ms.assetid: 409ac8c5-0bf7-4ae9-b709-5c2cfa1f8b7f
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_PRIVACY_EXEMPTION_LIST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 468406bddf74869d68464b2993e7479a9ca4626f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359172"
---
# <a name="oidwdisetprivacyexemptionlist"></a>OID\_WDI\_设置\_隐私\_免除\_列表


OID\_WDI\_设置\_隐私\_免除\_列表由主机提供的有关数据包说明的例外列表。 该适配器适用于指定例外的 IEEE EtherType 值匹配的数据包接收这些例外。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                 | 允许多个 TLV 实例 | 可选 | 描述                        |
|-------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------|
| [**WDI\_TLV\_隐私\_免除\_条目**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-privacy-exemption-entry) | X                              | X        | 隐私例外条目的列表。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




