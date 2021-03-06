---
title: 对 ACPI 服务使用 PEP
description: 本主题提供有关使用 ACPI 服务的平台扩展插件（PEPs）的信息。
ms.assetid: 80ED3B80-A1FF-4A41-BA88-EC1C832C4639
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5a42590abc050b137b6db68e2516e0061e45e0b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835881"
---
# <a name="using-peps-for-acpi-services"></a>对 ACPI 服务使用 PEP


本主题提供有关使用 ACPI 服务的平台扩展插件（PEPs）的信息。

PEPs 提供动态的运行时 ACPI 方法。 必须在 ACPI 固件中实现静态表（FADT、MADT、DBG2 等），以及 DSDT/SSDT 设备层次结构。

PEPs 旨在用于脱离 SoC 电源管理方法。 由于它们是可安装的二进制文件，因此它们可以动态更新，而不是要求固件刷新的 ACPI 固件。 这意味着你可以通过在 Windows 更新上发布更新的驱动程序，在已发布的平台上改善电源管理代码。 电源管理是 PEPs 的原始用途，但可用于提供或重写任何任意 ACPI 运行时方法。

PEPs 在 ACPI 命名空间层次结构的构造中不起作用，因为必须在固件 DSDT 中提供命名空间层次结构。 当 ACPI 驱动程序在运行时评估方法时，它将针对相关设备检查 PEP 的已实现方法，如果存在，它将执行 PEP 并忽略固件版本。 但是，必须在固件中定义设备本身。

使用 PEPs 进行电源管理比使用为 ACPI 固件编写的代码更容易调试，因为提供了相应的工具。 大多数和工具选项都不熟悉用于调试 ACPI 固件的工具。 与此相反，PEPs 是作为 Windows 驱动程序开发的，因此开发人员可以使用他们最熟悉的任何开发和调试工具。

使用 PEP 代替 ACPI 服务时，无需执行任何特殊操作或操作即可声明服务的角色。 当在 PEP 中实现方法时，Windows 将自动使用该方法。 如果在同一设备上提供相同方法的固件版本，则会将其忽略。

PEPs 会非常提前加载，以便其服务可用于设备驱动程序。 此外，通过 Windows 的抽象层被设计为对设备驱动程序透明。 驱动程序应能够与 ACPI 方法交互，就像没有使用 PEP 一样。

将 PEP 用于设备电源管理（DPM）和 ACPI 服务时，建议使用单独的 PEP 句柄，但这只是优先考虑。 共享句柄时，可以轻松地为设备跟踪 DPM 和 ACPI 状态，因为句柄是相同的。 不过，处理生存期管理稍微复杂一些。 此 PEP 需要提供句柄的引用计数，以确保仅在为该句柄断开 DPM 和 ACPI 服务（即，这两个[**PEP\_dpm\_注销\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[**PEP\_通知\_ACPI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)在该句柄上收到\_设备注册）。 当使用不同的句柄时，将单独跟踪 DPM 和 ACPI 状态，但处理生存期管理更为简单。 在这种情况下，可以在发送相应的取消注册通知时销毁句柄。

为了简化使用 ACPI 资源的过程，电源管理框架（PoFx）提供了 PEP\_请求\_常见\_ACPI\_将\_转换为\_BIOS\_资源帮助程序例程来转换 ACPI与 BIOS 资源的资源。

PEPs 负责计划无法同步执行的工作，以响应来自 PoFx 的 ACPI 通知，但使用的方法由 PEP 开发人员确定。 通常，PEP 会将工作排队，并在需要时启动工作线程。 还可能是因为工作需要等待某个外部事件（例如设备中断），并且将在该事件的上下文中处理。 完成工作后，PEP 可以通过\_[ **\_内核信息\_结构\_V3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_kernel_information_struct_v3)-&gt;[*RequestWorker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pofxcallbackrequestworker)（）来请求 PoFx 查询工作。 在响应中，PoFx 将为实现 DPM 通知处理程序（[*AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifydpm)）的 PEPS [ **\_dpm\_工作通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)， [ **\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)或在实现仅 ACPI 通知处理程序（[*AcceptAcpiNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifyacpi)）的 PEPs。

## <a name="related-topics"></a>相关主题
[ACPI 系统说明表](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)  
[**PEP\_DPM\_注销\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[**PEP\_通知\_ACPI\_注销\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[**PEP\_内核\_信息\_结构\_V3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_kernel_information_struct_v3)  
[**PEP\_DPM\_工作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[**PEP\_通知\_ACPI\_工作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[*RequestWorker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pofxcallbackrequestworker)  
[*AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifydpm)  
[ACPI 通知](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  



