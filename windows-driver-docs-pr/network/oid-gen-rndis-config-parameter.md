---
title: OID_GEN_RNDIS_CONFIG_PARAMETER
description: 作为一组 OID_GEN_RNDIS_CONFIG_PARAMETER 用于设置特定于设备的参数。
ms.assetid: 79e74e8b-7811-46a5-8ede-f6cca92967b0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RNDIS_CONFIG_PARAMETER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71c28e88e08d7f937cf675a8f1dbc176372eb549
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355120"
---
# <a name="oidgenrndisconfigparameter"></a>OID\_GEN\_RNDIS\_CONFIG\_参数


作为一组 OID\_GEN\_RNDIS\_CONFIG\_参数用于设置特定于设备的参数。 主机将使用它与仅限 RNDIS 设备。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 RNDIS 设备。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a name="remarks"></a>备注
-------

OID\_GEN\_RNDIS\_CONFIG\_的 RNDIS 设备上使用参数。 主机使用它来设置特定于设备的参数。 微型端口驱动程序不使用它。 有关此 OID 的详细信息，请参阅[设置特定于设备的参数](https://docs.microsoft.com/windows-hardware/drivers/network/setting-device-specific-parameters)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




