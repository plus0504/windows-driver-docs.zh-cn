---
title: 用户模式与内核模式
description: 用户模式与内核模式
ms.assetid: ee506167-6b64-4e50-9988-102416bcb056
keywords:
- 软件合成器 WDK 音频
- 自定义 synths WDK 音频
- DirectMusic WDK 音频，用户模式和内核模式对比
- 用户模式下 synths WDK 音频，对应于内核模式
- 内核模式 synths WDK 音频，对应于用户模式
- 滞后时间 WDK 的音频 DirectMusic
- 硬件合成器 WDK 音频
- 时间戳 WDK 音频
- DirectMusic 内核模式 WDK 音频，对应于用户模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bf38a3b33d390384fac8d84331edce018554269
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354142"
---
# <a name="user-mode-versus-kernel-mode"></a>用户模式与内核模式


## <span id="user_mode_versus_kernel_mode"></span><span id="USER_MODE_VERSUS_KERNEL_MODE"></span>


可以编写自定义的合成器为在用户模式或内核模式下运行。 一般情况下，软件 synths 更轻松地实现在用户模式下，但它们通常可以实现在内核模式下更低的延迟。 可以仅在内核模式下支持硬件组件。 充分的理由存在，但是，对于初级开发在用户模式下，即使最终实现是在内核模式下运行。

构建软件合成器 （和批接收器） 是在用户模式下要简单得多。 用户模式接口是易于使用，并且调试已得到简化。 另一个好处是，生成的组件是 Microsoft Windows 可执行文件。 此可执行文件是一个 COM 对象，因为安装它是只需使用 regsvr32.exe 命令行自注册。 (RegSvr32 系统应用程序调用 DLL 的[ **DllRegisterServer** ](https://docs.microsoft.com/windows/desktop/api/olectl/nf-olectl-dllregisterserver)函数。 有关详细信息，请参阅 Microsoft Windows SDK 文档。）

如果只需要一个用户模式下实现，可交付产品的应用程序而不是一个驱动程序。 用户可以避免复杂的驱动程序安装过程中，并安装后无需重新启动所需。 然后可以为一个可用的端口，具体取决于是否想要能够使用它其他应用程序枚举用户模式组件。 有关详细信息，请参阅[注册你的合成器](registering-your-synthesizer.md)。

内核模式软件实现的优点是较低的延迟。 随着加盖时间戳的消息，但是，这一优点是不一样大，因为使用它来进行。 旧版 MIDI Api 有没有时间戳，因此当播放下，这是它已排入队列以播放的确切时间。 时间戳将能够队列说明播放在指定时间在将来。 使用时间戳意味着除非提前警告系统中固有的延迟小于注意播放在正确的时间。

听起来排队尝试的与很少或没有提前警告时，延迟是仅一个问题。 因此，内核模式下实现时，建议使用仅有支持硬件加速时是不需要限制用户模式下的软件实现或。

如果您决定执行内核模式实现，最好的方法仍是开始开发在用户模式下。 Microsoft 的用户模式下合成器的源代码提供在 Microsoft Windows 驱动程序工具包 (WDK)，因此不需要从头开始编写新的合成器。 您可以使用现有代码来了解分析的可下载声音 (DL) 下载内容的方式。 然后，可以添加任何新功能 （如分析其他消息块） 和调试在用户模式下此逻辑首先，将用作存根出访问硬件的例程。 (无存根例程可以不执行任何操作或模拟软件中的硬件函数。)DLS 有关的详细信息，请参阅 Windows SDK 文档。

在用户模式下工作在实现后，可以将其移到内核模式，并使其正常工作。 在内核模式下工作的软件版本后下, 一步是开始将功能移动到您的硬件。 用户模式和内核模式软件 synths 作为硬件合成器启动并运行的过程中很有用的中间步骤。

若要汇总上面的建议：

-   对于仅限软件的组件，在用户模式下首次实现的组件，（目的是解决设计问题与简单的接口，调试时，安装和删除），然后将转换到内核模式如有必要由于延迟或其他考虑因素。

-   对于硬件组件，首先在用户模式下 （目的是解决设计问题与简单的接口，调试时，安装和删除），实现软件版本，然后将其转换为内核模式软件版本。 最后，将内核模式组件连接到硬件，一项功能时，直到一切按预期运行。

 

 




