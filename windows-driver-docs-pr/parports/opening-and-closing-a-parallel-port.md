---
title: 打开和关闭并行端口
description: 打开和关闭并行端口
ms.assetid: 2183ffd9-8265-4848-b5d1-703643e0d0e6
keywords:
- 并行端口 WDK，打开
- 并行端口 WDK，关闭
- 并行端口 WDK，共享
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64fb36c198e9e1777f48ed9b8bbbe11899f08e39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844496"
---
# <a name="opening-and-closing-a-parallel-port"></a>打开和关闭并行端口





客户端可以共享并行端口。 客户端必须先在并行端口上打开文件，然后客户端才能使用其他 i/o 请求或使用[并行端口回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 客户端在端口上关闭其文件后，不能尝试与并行端口进行通信。

请注意，在即插即用环境中，每当设备上没有打开的文件时，可以删除或添加设备。 通常，每次添加并行端口时，即插即用会分配不同的位置和资源。

 

 




