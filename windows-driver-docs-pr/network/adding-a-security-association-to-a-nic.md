---
title: 将安全关联添加到 NIC
description: 将安全关联添加到 NIC
ms.assetid: 524cc9f8-fe02-4192-85af-83813ae83d08
keywords:
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
- ESP 保护数据包 WDK IPsec 卸载、 安全关联
- AH 保护数据包 WDK IPsec 卸载、 安全关联
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdc4c279bdd78dafe37a7528cc35fa77f921279c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384732"
---
# <a name="adding-a-security-association-to-a-nic"></a>将安全关联添加到 NIC

\[IPsec 任务卸载功能已弃用，不应使用。\]




后 TCP/IP 传输确定 NIC 可以执行 Internet 协议安全 (IPsec) 操作 (请参阅[报告 NIC 的 IPsec 功能](reporting-a-nic-s-ipsec-capabilities.md))，传输必须请求 NIC 的微型端口驱动程序以添加一个或多个入站和之前传输的 nic 的出站安全关联 (Sa) 可将 nic 的 IPsec 任务卸载 以请求微型端口驱动程序到 NIC，TCP/IP 传输集添加一个或多个 SAs [OID\_TCP\_任务\_IPSEC\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-add-sa)。

 

 





