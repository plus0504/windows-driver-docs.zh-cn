---
title: 设计微型端口回调例程来处理 WMI 类
description: 设计处理 WMI 类的数据字段的微型端口驱动程序回调例程
ms.assetid: 6e08f9c1-e541-4e5f-8c99-f81d5793cc21
keywords:
- WMI Srb WDK 存储，设计回调例程
- 回调例程 WDK WMI Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5498f1a765e6cfff252c7a3afa2e36d2ffdb3ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520990"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-data-fields"></a>设计处理 WMI 类的数据字段的微型端口驱动程序回调例程


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


本部分介绍如何回调例程必须处理与数据字段为 WMI 类的输入和输出数据...

如果 WMI 类包含数据字段，WMI 工具套件将生成的数据在结构声明。 结构声明是除了任何生成来保留输入和输出属于类的 WMI 方法的参数的结构。 有关 WMI 工具套件生成来处理 WMI 方法的结构的详细信息，请参阅设计例程微型端口驱动程序回调该处理的 WMI 类的方法。

例如，假设我们编译以下 WMI 类定义与**mofcomp**并生成与.h 文件**wmimofck**。

```cpp
class HBAFCPBindingEntry
{
  [HBAType("HBA_FCPBINDINGTYPE"),
   Values{"TO_D_ID", "TO_WWN", "TO_OTHER"},
   ValueMap{"0", "1", "2"},
   WmiDataId(1)
  ]
  uint32  Type;
  [HBAType("HBA_FCID"),
   WmiDataId(2)
  ]
  HBAFCPID  FCPId;
  [HBAType("HBA_FCPSCSIENTRY"),
   WmiDataId(3)
  ]
  HBAScsiID  ScsiId;
};
```

生成的.h 文件将包含以下结构声明。

```cpp
typedef struct _HBAFCPBindingEntry
{
  ULONG  Type;
  HBAFCPID  FCPId;
  HBAScsiID  ScsiId;
} HBAFCPBindingEntry, *PHBAFCPBindingEntry;
```

管理输入和输出数据时，可以强制转换为输入和输出缓冲区的 SRB 此结构声明。

返回前，应调用回调例程[ **ScsiPortWmiPostProcess**](https://msdn.microsoft.com/library/windows/hardware/ff564796)。 此 SCSI 端口 WMI 库例程的信息，例如请求的状态和返回数据的大小更新请求上下文。 请求上下文中存储的数据有关的详细信息，请参阅[ **SCSIWMI\_请求\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff564946)。

 

 



