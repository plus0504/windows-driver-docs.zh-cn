---
Description: This topic first describes the initial setup that is done by the software to enable U1 and U2 transitions, and then describes how these transitions occur in the hardware.
title: U1 和 U2 转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e8cc5f049fcc6da78c0fb140f81e7bcece05522
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541478"
---
# <a name="u1-and-u2-transitions"></a>U1 和 U2 转换


本主题首先介绍的通过软件来启用 U1 和 U2 转换，并介绍如何在硬件发生这些转换的初始设置。

## <a name="initial-setup-by-software"></a>初始安装程序软件


本主题介绍如何软件枚举设备。

发生的 U1 或 U2 转换，软件的设备枚举过程中执行以下步骤。

1.  软件交换 U1 或 U2 退出滞后时间信息与设备在枚举过程。 作为此交换的第一部分，特定于设备的延迟将填充 bU1DevExitLat 和 wU2DevExitLat SuperSpeed USB 设备功能 （部分 9.6.2.2 的 USB 3.0 规范中定义） 字段中的设备。 作为交换的第二个部分，主机通知设备有关设备的总体退出延迟通过发送一组\_SEL 控制传输的 USB 3.0 规范 9.4.12 部分所述。 滞后时间信息包括与上游链接和控制器相关联的延迟。
2.  对于设备附加到 DS 端口，该软件配置两个值：端口\_U1\_超时和端口\_U2\_超时。 虽然确定这些值，该软件，将考虑设备 （如终结点的类型） 的特征，并与携带设备相关联的延迟从 U1 或 U2 回 U0。 下表描述了超时值。

    **表 1。端口\_U1\_超时和端口\_U2\_超时值**

    | 值   | 描述                                                                                                                                                                                                                  |
    |---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | 01H-FEH | DS 端口必须处于非活动状态一段时间后启动转换。 确切时间派生自的超时值。 端口必须接受转换，除非有挂起的流量由链接合作伙伴启动。 |
    | FFH     | DS 端口不能启动转换，但必须接受转换，除非有挂起的流量由链接合作伙伴启动。                                                                                    |
    | 0       | DS 端口不能启动转换，必须接受转换由链接合作伙伴启动。                                                                                                                |

     

3.  如果端口\_U2\_超时值为 01 H FEH 之间，则由于第 2 步硬件中发生的其他步骤。 DS 端口将其链接合作伙伴告知该值。 "直接转换从 U1 到 U2"中介绍了此步骤的重要性。
4.  对于每个设备或中心，该软件配置两个值：U1\_启用和 U2\_通过发送集启用\_功能 (U1\_启用/U2\_启用) 控制传输。 下表介绍了这些值。

    **表 2。U1\_启用和 U2\_启用值**

    | 值    | 描述                                                                                                                       |
    |----------|-----------------------------------------------------------------------------------------------------------------------------------|
    | 已启用  | 美国端口可以启动转换，然后接受转换，如果设备策略允许由链接合作伙伴启动。 |
    | Disabled | 美国端口不能启动转换，但可以接受转换由链接合作伙伴启动。                          |

     
## <a name="hardware-transitions"></a>硬件转换


本主题介绍的 U1 和 U2 硬件转换。

之后该软件的初始设置，硬件转换为 U1 和 u2 自主操作而无需进一步干预的软件。

链接处于工作状态 (U0)，只要它主动传输数据包。 链接被视为处于空闲状态时要不传输任何数据包。 处于空闲状态，任何链接合作伙伴可以启动到 U1 或 U2 的转换。 其他链接合作伙伴可以选择接受或拒绝转换。 如果链接伙伴接受的转换，该链接将移动到该 U 状态。 如果它会拒绝转换，该链接会保留在 U0。

### <a name="ds-port-initiated-transitions"></a>DS 端口启动转换


DS 端口实现计时器机制，用于跟踪在端口上处于非活动状态。 获取重置计时器，每次该端口将发送或接收的数据包。 当软件程序新的超时值时还重置计时器。 如果该软件进行编程的 DS 端口启动仅 U1 或 U2 的转换，DS 端口时链接首次进入 U0 启动计时器。 计时器值取决于编写软件 U1 （或 U2） 超时值。 如果在计时器过期时该链接在 U0，DS 端口启动 U1 （或 U2） 转换。

美国端口链接合作伙伴可以选择拒绝转换，如果设备识别转换可能会影响设备的能力，以满足性能或延迟要求。 例如，如果设备已向你发送 ERDY 通知，并需要从主机的传输请求，则设备可能会拒绝 U1 或 U2 状态转换在此期间。

如果该软件进行编程的 DS 端口启动 U1 和 U2 转换，DS 端口首次启动 U1 转换基于计时器 （前面所述在本部分中）。 在本主题中描述从 U1 过渡到 U2**从 U1 到 U2 的直接转换**。

如果链接为 U1 或 U2，DS 端口可以使端口重新 U0 到每当它收到的设备连接到端口的流量。

### <a name="device-us-port-initiated-transitions"></a>设备 （美国端口） 的启动转换


设备可以选择启动 U0 从转换到 U1 或到 U2、 U0，只要启用了此功能的软件。 如果设备过渡 U1 的链接，该链接可以过渡到 U2 直接基于 U2 计时器的 DS 端口 （在"直接转换从 U1 到 U2"中所述。 但是，如果未设置 U2 计时器，设备不能启动直接转换从 U1 到 U2 本身。 在这种情况下，设备必须将该链接恢复到 U0 启动到 U2 的转换之前。

时决定何时启动这些转换时，设备应考虑其退出的延迟和性能要求。 若要帮助做出明智的决策，有关如何主动的方式启动转换的设备，软件还提供了各种退出延迟值"初始软件安装程序"中的本文档前面所述。

如果链接为 U1 或 U2，美国端口可以使端口重新 U0 到在任何时间。 通常情况下，美国端口启动转换到 U0 时它知道它是要将任何数据包发送到主机，或如果它预期从主机的数据包。

### <a name="advantages-of-device-initiated-lpm"></a>由设备发起 LPM 的优点


软件为 DS 端口设置的计时器值基于常规试探法。 同时选择这些计时器值，软件可确保设备性能不受到影响。 为了保持设备的性能，软件不能选择因太小的值。 因为 DS 端口的启动的转换基于定时器并没有考虑到帐户的设备的确切状态，此机制不能充分利用发送设备到 U1 或 U2 状态的所有可能的机会。

该设备，但是，具有有关证书特征和当前状态的准确知识。 因此，它可以进行下一步的传输时要发生智能的猜测。 根据该信息，设备可以 （而且应该） 选择主动启动这些转换而不会显著影响性能。

例如，设备具有 NRDY 通知发送给其某个终结点上，并知道，将不会有流量一段时间。 在这种情况下，设备可以立即启动到 U1 或 U2 的转换。 只需在发送前 ERDY 通知，设备可以将恢复到在发送该数据的准备 U0 链接。 有关此过程的详细信息，请参阅部分 C.3.1 的 USB 3.0 规范。

## <a name="direct-transition-from-u1-to-u2"></a>从 U1 到 U2 的直接转换


如果链接是在 U1，就可以链接可以直接转换为 U2 而无需输入 U0 之间。 可以发生而不考虑哪些链接合作伙伴启动到 U1 的转换。 但是，U1 U2 转换可能仅当链接在 DS 端口上的 U2 超时值设置为该版本 FEH 之间的值。

"初始安装软件"一节介绍允许 DS 端口与它链接的伙伴通信的超时值的其他步骤。 链接已进入 U1 之后，同时链接合作伙伴开始根据 DS 端口的 U2 超时值设置一个计时器将超时值。 如果计时器由于流量不会重置，并且已过期，这两个链接合作伙伴以无提示方式进行转换到 U2 而无需任何显式它们之间通信。

### <a name="transitions-from-u1-or-u2-to-u3"></a>从 U1 或 U2 将转换为 U3


将转换为 U1 或 U2 自主硬件中启动，但转换到 U3 启动的软件。 由于处于非活动状态一段时间后仅启动 U3 转换时，很可能是链接处于 U1 或 U2 （而非 U0） 转换前。

USB 3.0 规范并未定义从 U1 或 U2 将直接转换为 U3。 父中心或控制器负责自动转换到 U0 链接，然后将其转换为 U3。

### <a name="u1-or-u2-transitions-for-hubs"></a>集线器的 U1 或 U2 转换


USB 3.0 规范提供特定指导原则的中心有关启动 U 状态转换时其美国端口上。 如果所有 DS 端口都在链接状态 U1 或更低版本，该中心应启动 U1 转换其美国的端口，假设软件启用要启动 U1 转换的中心。

同样，如果所有 DS 端口在链接状态 U2 或更低版本，该中心应启动 U2 转换其美国的端口，假设软件启用要启动 U2 转换的中心。

**请注意**  没有附加到 DS 端口的设备，如果端口的状态是 Rx.Detect，即低于 U2。 因此如果不有未连接任何设备，中心将向 U2 发送其美国的端口。 此外，如果所有 DS 端口最初都是为 U1 或更低版本迁移到 U2 或更低版本，该中心应转换美国端口 U1 U2。 因为该转换不基于 U2 活动计时器，中心必须引入 U0 其美国端口并将其发送给 U2。

 

## <a name="packet-deferring"></a>数据包延迟


USB 3.0 规范描述一种机制，称为数据包延迟 （请参阅部分 C.1.2.2）。 该机制用于尽量 LPM 的总线利用率的影响。

如果主机将转移请求发送到设备时，其上游链接位于 U1 或 U2，主机可能最终等待返回到 U0 的链接，然后，设备能够响应浪费总线带宽。 若要避免该等待，父中心代表设备通过响应将延迟的数据包标头发送回主机。 主机处理方式类似于 NRDY 中的延迟的数据包标头，随后可用来启动与其他终结点的传输。 并行情况下，中心启动 U0 转换链接，然后延迟数据包相关通知设备。 然后，设备将 ERDY 发送到主机以指示设备现已准备好进行传输。 然后，主机可以重新计划传输到设备。

设备的重要职责是，发送 ERDY 之后, 设备负责在 U0 中保留该链接，直到主机将响应发送到 ERDY 或直到**tERDYTimeout** （500 毫秒） 的时间结束。 此期间，设备不能启动 U1 或 U2 转换，并且还应拒绝由其链接合作伙伴启动任何转换。

 

 
 

 

 



