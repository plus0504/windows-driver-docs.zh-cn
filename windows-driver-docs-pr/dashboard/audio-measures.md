---
title: 音频度量
description: 音频度量在音频驱动程序外部测试过程中筛选出良性初始化错误
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 50de16eb2608b21c923671413f0e5ca335698a39
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70224057"
---
# <a name="audio-measures"></a>音频度量

## <a name="description"></a>描述

Windows 核心音频 API 引入了流的概念，作为应用程序和用于播放或捕获音频的音频设备之间的连接，其中单个应用程序可以有多个音频流  。 应用程序初始化的每个流都分配给一个会话，用于管理每个已分配的流的输入和输出  。 应用程序可以调用 Windows 核心音频 API，该 API 返回用于指示初始化是否成功的成功或失败代码。 这些失败代码可能微不足道，如终结点不再存在，也可能是在遇到 bug 后导致初始化失败的严重错误。

音频度量筛选出良性初始化错误；[附录](/measure-appendix.md)中提供这些错误的列表。