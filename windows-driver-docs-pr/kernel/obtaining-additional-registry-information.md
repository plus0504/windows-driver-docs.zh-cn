---
title: 获取其他注册表信息
description: 获取其他注册表信息
ms.assetid: 989acf63-3bb1-4d9a-a7a8-3eea1e2bc68a
keywords:
- 筛选注册表调用 WDK 内核，获取其他信息
- 注册表筛选驱动程序 WDK 内核，要获取的其他信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c09a7547bb37ccb81948d6f0de13c8c00d8333e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838528"
---
# <a name="obtaining-additional-registry-information"></a>获取其他注册表信息


在 Windows Vista 及更高版本的操作系统上运行的注册表筛选驱动程序可以获取以下有关注册表操作的其他信息：

-   对象标识符和名称

    [**CmCallbackGetKeyObjectIDEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmcallbackgetkeyobjectidex)例程检索与指定的注册表项对象相关联的注册表项标识符和对象名。

-   事务对象

    [**CmGetBoundTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetboundtransaction)例程返回指向 transaction 对象的指针，该对象表示与某个注册表项对象关联的[事务](using-kernel-transaction-manager.md)（如果有）。

-   版本信息

    [**CmGetCallbackVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetcallbackversion)例程检索当前版本的 configuration manager 的注册表回调功能的主要版本号和次版本号。

 

 




