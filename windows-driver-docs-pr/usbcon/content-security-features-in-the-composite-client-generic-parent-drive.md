---
Description: Digital Rights Management (DRM) systems often make use of device serial numbers to ensure that legitimate customers have access to digitized intellectual property.
title: Usbccgp.sys 中的内容的安全功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 027bba805ecfebe72046357dfab9d2451fa7f51b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554254"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys 中的内容的安全功能


数字版权管理 (DRM) 系统经常做出的设备序列号以确保合法客户有权使用数字化知识产权。 如果 USB 设备已 CSM 1 内容安全接口，客户端驱动程序可以查询其序列号的发送[ **IOCTL\_存储\_获取\_媒体\_序列\_数量**](https://msdn.microsoft.com/library/windows/hardware/ff560557)泛型父驱动程序的请求。

## <a name="related-topics"></a>相关主题
[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  


