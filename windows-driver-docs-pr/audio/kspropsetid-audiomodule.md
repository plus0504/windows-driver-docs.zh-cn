---
title: KSPROPSETID\_AudioModule
description: KSPROPSETID\_音频驱动程序用 AudioModule 属性集来检索音频模块的列表。
ms.assetid: 6F167E5E-CA11-45F3-BF21-6B9A3F90DB9F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c0b7568a52d88a8d49a99e84a7722b567eae2fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360493"
---
# <a name="kspropsetidaudiomodule"></a>KSPROPSETID\_AudioModule


**KSPROPSETID\_AudioModule**音频驱动程序使用属性集来检索音频模块的列表。

*Ksmedia.h*标头文件定义**KSPROPSETID\_AudioModule**属性设置，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioModule \
    0xc034fdb0, 0xff75, 0x47c8, 0xaa, 0x3c, 0xee, 0x46, 0x71, 0x6b, 0x50, 0xc6
DEFINE_GUIDSTRUCT("C034FDB0-FF75-47C8-AA3C-EE46716B50C6", KSPROPSETID_AudioModule);
#define KSPROPSETID_AudioModule DEFINE_GUIDNAMED(KSPROPSETID_AudioModule)
```

**KSPROPSETID\_AudioModule**属性集包含以下 KS 属性。

[**KSPROPERTY\_AUDIOMODULE\_描述符**](ksproperty-audiomodule-descriptors.md)

[**KSPROPERTY\_AUDIOMODULE\_命令**](ksproperty-audiomodule-command.md)

[**KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID**](ksproperty-audiomodule-notification-device-id.md)

此属性的名称中定义[ **KSPROPERTY\_AUDIOMODULE** ](ksproperty-audiomodule.md)枚举。

有关音频模块的详细信息，请参阅[实现音频模块发现](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)。

 

 





