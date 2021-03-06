---
title: 设置 SPCRP_Xxx 属性
description: 设置 SPCRP_Xxx 属性
ms.assetid: efb0d02e-ec4c-4c1b-900b-c81f504d2919
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3927adf778967a958a625ba8c510469d759151cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386884"
---
# <a name="setting-spcrpxxx-properties"></a>设置 SPCRP_Xxx 属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持[设备安装程序类属性](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))它们分别对应于中定义的SPCRP_Xxx标识符*Setupapi.h*。 这些属性描述设备安装程序类的特征。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 还支持大部分设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，这些版本的 Windows 使用 SPCRP_*Xxx*标识符，以表示该设备安装程序类属性。 若要保持与早期版本的 Windows 兼容性，Windows Vista 和更高版本还支持使用 SPCRP_*Xxx*标识符，以访问设备安装程序类属性。 但是，应使用统一的设备属性模型属性键来访问设备安装程序类属性。

系统定义的设备安装程序类属性的列表，请参阅[设备安装程序类属性，对应于 SPCRP_Xxx 标识符](https://docs.microsoft.com/previous-versions/ff542245(v=vs.85))。 属性的密钥标识符用于访问在 Windows Vista 和更高版本中的属性按列出的设备安装程序类属性。 与属性键一起提供的信息还包括相应 SPCRP_*Xxx*可用于访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的属性的标识符。

有关如何使用属性键来访问在 Windows Vista 和更高版本的设备安装程序类属性的信息，请参阅[访问设备类属性 （Windows Vista 和更高版本）](accessing-device-class-properties--windows-vista-and-later-.md)。

若要设置 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备安装程序类属性，请调用[ **SetupDiSetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)并提供以下参数值：

-   设置*ClassGuid*为指向表示要为其设置属性的设备安装程序类的 GUID。

-   设置*属性*为要设置具有前缀"SPCRP_"的属性的标识符。

-   设置*PropertyBuffer*到指向包含的属性值的缓冲区的指针。

-   设置*PropertyBufferSize*到的大小，以字节为单位的正确数据。

-   设置*MachineName*为计算机名称。

-   设置*保留*到**NULL**。

如果此调用[ **SetupDiSetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)成功， **SetupDiSetClassRegistryProperty**设置的设备安装程序类属性，并返回 **，则返回 TRUE**。 如果函数调用失败， **SetupDiSetClassRegistryProperty**将返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

 

 





