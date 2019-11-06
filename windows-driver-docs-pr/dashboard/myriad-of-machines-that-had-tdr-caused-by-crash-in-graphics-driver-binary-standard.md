---
title: 由于显卡驱动程序二进制文件中的崩溃导致发生了 TDR 的计算机的巨大数量
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为大量不同的计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了 TDR
ms.topic: article
ms.date: 10/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: af818c5d6a1ec5dacbe887cc499531fc16373e0b
ms.sourcegitcommit: 6e839d8f12eafd93d357b6896e0671cb69f7ecfa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2019
ms.locfileid: "72962173"
---
# <a name="myriad-of-machines-that-had-a-tdr-caused-by-a-crash-in-the-graphics-driver-binary"></a>由于显卡驱动程序二进制文件中的崩溃导致发生了 TDR 的计算机的巨大数量

## <a name="description"></a>描述

在用户会话期间，显卡驱动程序二进制文件中的崩溃会导致计算机的屏幕挂起或完全冻结。 超时检测和恢复 (TDR) 事件会尝试检测这些挂起，并动态恢复以取消冻结显示器。 遇到 TDR 的用户在 TDR 成功之前将无法使用计算机，这会导致屏幕闪烁。 

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天滑动窗口|
|度量标准 |计算机的聚合|
|最小总体数量 |10,000 台计算机|
|通过标准 |<= 130/10,000 台计算机遇到 TDR|
|度量 ID |20574707|

## <a name="calculation"></a>计算

该度量将来自 7 天滑动窗口的遥测数据聚合为**大量**的**不同计算机，这些计算机由于显卡驱动程序二进制文件中的崩溃而发生了 TDR**。
1. 出现 TDR 的计算机数 = 计数（使用该驱动程序的计算机中出现 TDR 的计算机数） 
2. 计算机总数 = 计数（使用该驱动程序的计算机数） 
3. 发生 TDR 的计算机的比率 = 发生 TDR 的计算机数/计算机总数 

### <a name="final-calculation"></a>最终计算

相对于总体的不同设备命中数 (DHoP) = 出现 TDR 的计算机的比率 * 10,000 

在上面的计算中，结果规范化为 10,000 台计算机，最终结果为：  
[相对于总体的不同设备命中数 (DHoP)] 10,000 台计算机中由于显卡驱动程序二进制文件中的崩溃而发生 TDR 的不同计算机数