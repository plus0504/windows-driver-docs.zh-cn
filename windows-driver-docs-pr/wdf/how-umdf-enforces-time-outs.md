---
title: UMDF 中的主机进程超时
description: UMDF 中的主机进程超时
ms.assetid: b8a0a4cc-9c6d-40e2-a3f1-9807dbcf15d9
keywords:
- 用户模式驱动程序框架 WDK，超时值
- UMDF WDK，超时值
- 用户模式驱动程序 WDK UMDF，超时值
- 超时 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92b6248f82c08b9d2f85b3a85d92dcd26377006f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382838"
---
# <a name="host-process-timeouts-in-umdf"></a>UMDF 中的主机进程超时


当该发送程序发送到驱动程序主机进程的关键请求时，主机将启动内部计时器。 默认超时间隔为 60 秒。 关键的请求包括插、 电源和 I/O 取消。

只要用户模式驱动程序框架 (UMDF) 驱动程序执行定期向完成请求的操作，该发送程序扩展了超时期限。 例如，对于删除请求，该驱动程序需要按固定间隔从删除回调返回。

如果超时时间到期时，该发送程序生成 WER 错误报告、 终止主机进程，并尝试重新启动设备。 有关自动重启的信息，请参阅[UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。

有关此报表中字段的信息，请参阅[WER 报表中访问 UMDF 元数据](accessing-umdf-metadata-in-wer-reports.md)。

超时时间是反射器终止主机进程的最常见原因。

您可以通过使用扩展的超时期限[WDF 验证程序控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)。

 

 





