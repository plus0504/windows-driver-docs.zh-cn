---
title: 报告多头视频内存
description: 报告多头视频内存
ms.assetid: 664b60f5-9e19-4dfc-8bd7-73ceccf6cbea
keywords:
- 多个头硬件 WDK DirectX 9.0 中，内存报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f471c37a405083ce92193f9fb661eacafc6b84c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364375"
---
# <a name="reporting-multiple-head-video-memory"></a>报告多头视频内存


## <span id="ddk_reporting_multiple_head_video_memory_gg"></span><span id="DDK_REPORTING_MULTIPLE_HEAD_VIDEO_MEMORY_GG"></span>


在多个头模式中，master 头必须对驱动程序的调用做出响应[ *DdGetAvailDriverMemory* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory)函数 master 头好像只有头控制多个头卡。 该驱动程序返回的可用内存量必须包括其视频内存已到主头交回任何从属 head 的视频内存 (即，任何从属收到的 head *DdCreateSurface*使用调用DDSCAPS2\_ADDITIONALPRIMARY 位集)。

 

 





