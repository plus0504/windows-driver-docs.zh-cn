---
title: 位置模拟器的指南
description: 本部分包含实现位置模拟器驱动程序的指导。
ms.assetid: 4AA6C3EE-0150-45A8-ACC2-D0267591D33D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 625294038d7a74faca4a05cb41e236cbf1e64bc3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363670"
---
# <a name="guidance-for-location-simulators"></a>位置模拟器的指南


Microsoft Visual Studio 2012 提供了[定位模拟器](https://docs.microsoft.com/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015#bkmk-set-the-simulated-geo-location-of-the-device)的一起使用，创建一个位置模拟器驱动程序。 本部分包含实现位置模拟器驱动程序的指导。 请注意，从 Visual Studio 2017 开始，位置模拟器功能不再存在，因此不支持模拟的传感器驱动程序。

## <a name="configure-the-simulator"></a>配置模拟器


若要启用模拟器驱动程序，编辑注册表项`HKLM\Software\Microsoft\Location`通过设置名为"SimulatorID"为模拟器驱动程序的传感器 ID 的字符串值。

## <a name="clear-data-on-simulator-exit"></a>模拟器退出时清除数据


模拟器驱动程序模拟器应用程序退出时，应将状态更改为否\_数据和发送状态更改事件。

## <a name="how-simulator-data-is-used"></a>如何使用模拟器数据


-   定位模拟器的模拟器会话仅用于模拟器驱动程序中的数据。 永远不会在正常的应用程序中使用模拟器数据。
-   如果在模拟器中运行时，模拟器驱动程序不具有数据，然后将位置在模拟器中使用来自其他源的数据。

## <a name="related-topics"></a>相关主题
[在模拟器中运行 UWP 应用](https://docs.microsoft.com/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015)  
[设置设备的模拟地理位置](https://docs.microsoft.com/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015#bkmk-set-the-simulated-geo-location-of-the-device)  



