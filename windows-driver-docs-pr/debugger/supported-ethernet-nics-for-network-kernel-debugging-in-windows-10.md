---
title: Windows 10 中的网络内核调试支持的以太网 NIC
description: 当目标计算机运行 Windows 时，可以通过以太网网络电缆进行内核调试。 目标计算机必须具有支持的网络接口卡（NIC）或网络适配器。
ms.assetid: F98A7ACE-DD04-423C-A438-89E21363C693
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: a44c6eebc06d394e034a352d8c86bd7f21a6b7d9
ms.sourcegitcommit: d728d086444a8a820fb098df34414ccdb3f32100
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2020
ms.locfileid: "84784633"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-10"></a>Windows 10 中的网络内核调试支持的以太网 NIC

当目标计算机运行 Windows 时，可以通过以太网网络电缆进行内核调试。 目标计算机必须具有支持的网络接口卡（NIC）或网络适配器。

在内核调试过程中，运行调试器的计算机称为*主机计算机*，被调试的计算机称为*目标计算机*。 有关详细信息，请参阅[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

若要通过网络电缆进行内核调试，目标计算机必须具有支持的网络适配器。 当目标计算机运行 Windows 时，此处列出的网络适配器支持内核调试。

**版本信息**

支持的适配器列表适用于以下版本的 Windows

- Windows 10 版本 2004
- Windows Server 2019

**Windows 以前版本的适配器支持**  

若要确定适用于任何特定版本的 Windows 的 Nic 集，请检查 `VerifiedNicList.xml` 由该特定版本的 windows 附带的 WDK 安装的 "调试器" 目录中的文件。 对于64位 Windows，默认情况下，它将安装在此目录中：

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\VerifiedNicList.xml`

针对特定版本检查 WDK 中随附的 VerifiedNicList.xml 是必需的，因为其他硬件支持已添加到以前版本中不存在的新版本的 Windows 中。  因此，你必须检查该特定版本的 VerifiedNicLIst.xml 文件。

## <a name="finding-the-vendor-id-and-device-id"></a>查找供应商 ID 和设备 ID

查找目标计算机上的网络适配器的供应商 ID 和设备 ID。

- 在目标计算机上，打开设备管理器（在命令提示符窗口中输入**devmgmt.msc** ）。
- 在设备管理器中，找到要用于调试的网络适配器。
- 右键单击网络适配器节点，然后选择 "**属性**"。
- 在 "**详细信息**" 选项卡的 "**属性**" 下，选择 "**硬件 id**"。

供应商和设备 Id 显示为即使 \_ *VENDORID*和 DEV \_ *DeviceID*。 例如，如果你看到 PCI \\ 即使 \_ 8086&DEV \_ 104B，则供应商 id 为8086，设备 id 为104B。

## <a name="vendor-id-8086-intel-corporation"></a>供应商 ID 8086，Intel Corporation

对于供应商 ID 8086，支持以下设备 Id：

0001 0008 000C 000D 0438 043A 043C 0440 0470 1000 1001 1004 1008 1009 100C 100D 100E 100F 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101D 101E 1026 1027 1028 1049 104A 104B 104C 104D 105E 105F 1060 1071 1075 1076 1077 1078 1079 107A 107B 107C 107D 107E 107F 108A 108B 108C 1096 1098 1099 109A 10A4 10A5 10A7 10A9 10B5 10B9 10BA 10BB 10BC 10BD 10BF 10C0 10C2 10C3 10C4 10C5 10C6 10C7 10C810C9 10CB 10CC 10CD 10CE 10D3 10D5 10D6 10D9 10DA 10DB 10DD 10DE 10DF 10E1 10E5 10E6 10E7 10E8 10EA 10EB 10EC 10EF 10F0 10F1 10F4 10F5 10F6 10F7 10F8 10F9 10FB 10FC 11A9 1501 1502 1503 1507 150A 150B 150C 150D 150E 150F 1510 1511 1514 1516 1517 1518 151C 1521 1522 1523 1524 1525 1526 1527 1528 1529 152A 1533 1534 1535 1536 1537 1538 1539 153A 153B 1546 154A 154D 1557 1558 1559 155A 1560 1563 156F1570 157B 157C 15A0 15A1 15A2 15A3 15AA 15AB 15AC 15AD 15AE 15B7 15B8 15B9 15BB 15BC 15BD 15BE 15D6 15D7 15D8 15DF 15E0 15E1 15E2 15E3 17D0 1F40 1F41 1F45 1F63 1F72 211B 2159 294C 8976

## <a name="vendor-id-10ec-realtek-semiconductor-corp"></a>供应商 ID 10EC，Realtek 半导体公司。

对于供应商 ID 10EC，支持以下设备 Id：

2502 2600 3000 8125 8136 8137 8161 8166 8167 8168 8169 8225

## <a name="vendor-id-14e4-broadcom"></a>供应商 ID 14E4，Broadcom

对于供应商 ID 14E4，支持以下设备 Id：

1600 1601 1614 1639 163A 163B 163C 163D 163E 1641 1642 1643 1644 1645 1646 1647 1648 164A 164C 164D 164E 164F 1650 1653 1654 1655 1656 1657 1659 165A 165B 165C 165D 165E 165F 1662 1663 1665 1668 1669 166A 166B 166D 166E 1672 1673 1674 1676 1677 1678 1679 167A 167B 167C 167D 167F 168A 168D 168E 1680 1681 1682 1683 1684 1686 1687 1688 1690 1691 1692 1693 1694 1696 1698 1699 169A 169B 169D 16A0 16A116A2 16A4 16A5 16A6 16A7 16A8 16AA 16AC 16AE 16B0 16B1 16B2 16B3 16B4 16B5 16B6 16B7 16C6 16C7 16C9 16CA 16CE 16CF 16D0 16D1 16D2 16D5 16D6 16D7 16D8 16D9 16DD 16DF 16E0 16E2 16E3 16E4 16E9 16F0 16F1 16F7 16FD 16FE 16FF 170D 170E 170F D802

## <a name="vendor-id-1969-atheros-communications"></a>供应商 ID 1969，Atheros 通信

对于供应商 ID 1969，支持以下设备 Id：

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1

## <a name="vendor-id-19a2-serverengines-emulex"></a>供应商 ID 19A2，ServerEngines （Emulex）

对于供应商 ID 19A2，支持以下设备 Id：

0211 0215 0221 0700 0710

## <a name="vendor-id-10df-emulex-corporation"></a>供应商 ID 10DF，Emulex Corporation

对于供应商 ID 10DF，支持以下设备 Id：

0720 E220

## <a name="vendor-id-15b3-mellanox-technology"></a>供应商 ID 15B3，Mellanox 技术

对于供应商 ID 15B3，支持以下设备 Id：

1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 100A 100B 100C 100D 100E 1010 1013 1015 1017 1019 100F 101B 101D 101F 102B 1021 1023 1025 1027 1029 102F 6340 6341 634A 634B 673C 673D 675A 676E 6354 6368 6369 6372 6732 6733 6746 6750 6751 6764 6765

## <a name="vendor-id-1137-cisco-systems-inc"></a>供应商 ID 1137，Cisco 系统 Inc。

对于供应商 ID 1137，支持以下设备 Id：

0043

## <a name="related-topics"></a>相关主题

[在 Visual Studio 中设置通过网线进行的内核模式调试](setting-up-a-network-debugging-connection-in-visual-studio.md)

[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)

[手动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection.md)

[Windows 8 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

[Windows 8.1 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

 

 






