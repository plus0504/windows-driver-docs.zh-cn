---
title: MOUNTDEV_MOUNTED_DEVICE_GUID
description: MOUNTDEV_MOUNTED_DEVICE_GUID
ms.assetid: 48d127ed-414b-40bb-8a35-6472c8783b81
keywords:
- MOUNTDEV_MOUNTED_DEVICE_GUID 设备和驱动程序安装
topic_type:
- apiref
api_name:
- MOUNTDEV_MOUNTED_DEVICE_GUID
api_location:
- Mountmgr.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3da28329f4f87fbc77df61ee812183d64ffd7cee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371923"
---
# <a name="mountdevmounteddeviceguid"></a>MOUNTDEV_MOUNTED_DEVICE_GUID


MOUNTDEV_MOUNTED_DEVICE_GUID[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为卷设备定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>MOUNTDEV_MOUNTED_DEVICE_GUID</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F5630D-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此设备接口类的 MOUNTDEV_MOUNTED_DEVICE_GUID 标识符是其别名[ **GUID_DEVINTERFACE_VOLUME** ](guid-devinterface-volume.md)设备接口类。

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[classpnp 会存储类驱动程序库](https://go.microsoft.com/fwlink/p/?linkid=256095)，它使用 MOUNTDEV_MOUNTED_DEVICE_GUID 注册 GUID_DEVINTERFACE_VOLUME 设备接口的实例类。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Mountmgr.h （包括 Mountmgr.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

 

 






