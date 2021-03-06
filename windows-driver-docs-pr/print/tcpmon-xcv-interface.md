---
title: TCPMON Xcv 接口
description: TCPMON Xcv 接口
ms.assetid: 7b2b1cff-ab8f-44e0-9327-dc60a0072bf5
keywords:
- 打印监视器 WDK，TCPMON Xcv
- transceive （Xcv）接口 WDK 打印
- Xcv 接口 WDK 打印
- TCPMON Xcv 接口 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18800207a56cbc58a1f044f21585b25e19c38a2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838784"
---
# <a name="tcpmon-xcv-interface"></a>TCPMON Xcv 接口





本部分介绍标准 TCP/IP 端口监视器（TCPMON）的 transceive （Xcv）接口。 此接口是使用[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))和[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)函数调用实现的，使其能够使用它来配置 tcp/ip 打印机端口或获取有关 tcp/ip 打印机端口配置的信息。 本部分中所述的 Xcv 接口特定于 TCP/IP 端口。 其他 Xcv 接口可能适用于其他端口类型。

若要获取本地计算机或远程计算机的 Xcv 接口的句柄，请调用**OpenPrinter**函数（如 Microsoft Windows SDK 文档中所述）。 下面的代码示例演示如何获取端口的 Xcv 句柄：

```cpp
HANDLE hXcv = INVALID_HANDLE_VALUE;
PRINTER_DEFAULTS Defaults = { NULL, NULL, <Required Access> };

// Handle to a local machine
if (OpenPrinter(",XcvPort <PortName>", &hXcv, &Defaults )
{
 // hXvc contains an Xcv data handle to a local TCPMON port
}

// Handle to a remote machine
if (OpenPrinter("<ServerName>\\,XcvPort <PortName>", &hXcv, &Defaults )
{
 // hXvc contains an Xcv data handle to a TCPMON port on <ServerName>
}
```

在代码示例中， *ServerName*和*portvalue*表示服务器和端口名称字符串。 一旦获取了句柄，就可以查询特定于 TCPMON 端口监视器的信息，也可以更改端口配置。 请注意，必须在打印机\_默认结构的**DesiredAccess**成员中指定端口监视器所需的访问权限（如果不需要特殊安全性，则传递**NULL** ）。 对于对[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))函数的某些调用（如指定了 AddPort 和 DeletePort 命令时），请参阅[TCPMON Xcv 命令](tcpmon-xcv-commands.md)）、SERVER\_ACCESS\_管理权限是必需的。 有关**OpenPrinter**函数的详细信息以及在打印机\_默认结构中可能需要的访问权限，请参阅 Windows SDK 文档。

如果该端口尚不存在，则可以通过指定监视器名称从服务器中获取 Xcv 句柄。 （对于标准 TCP/IP 端口监视器端口，这是 "标准 TCP/IP 端口"。）下面的代码示例演示如何获取端口监视器的 Xcv 数据句柄：

```cpp
HANDLE hXcv = INVALID_HANDLE_VALUE;
PRINTER_DEFAULTS Defaults = { NULL, NULL, <Required Access> };

// Handle to a local machine
if (OpenPrinter(",XcvMonitor <MonitorName>", &hXcv, &Defaults )
{
 // hXcv contains an Xcv data handle to the monitor <MonitorName>
}

// Handle to a remote machine
if (OpenPrinter("<ServerName>\\,XcvMonitor <MonitorName>", &hXcv, &Defaults )
{
 // hXcv contains an Xcv data handle to the monitor 
 // <MonitorName> on the server <ServerName>
}
```

在代码示例中， *ServerName*和*portvalue*表示服务器和端口名称字符串。 获取 Xcv 数据句柄后，可以通过调用[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))函数向监视器发出指令和请求。

请注意，从**XcvData**函数返回的值仅指示数据是否已正确发送到端口监视器。 如果返回值**为 TRUE** ，则表示操作成功。 若要确定操作是否成功，请检查 \**pdwStatus*中的值。 下表汇总了这些状态值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态值</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NO_ERROR</p></td>
<td><p>操作成功。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_ACCESS_DENIED</p></td>
<td><p>用户的权限不足。 命令需要 SERVER_ACCESS_ADMINISTER 权限。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INSUFFICIENT_BUFFER</p></td>
<td><p>需要输出缓冲区，但其小于所需的大小。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_DATA</p></td>
<td><p>需要输入缓冲区，但指向它的指针为<strong>NULL</strong>，或</p>
<p>输入缓冲区的大小小于所需的大小。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_HANDLE</p></td>
<td><p>Xcv 数据句柄无效。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_LEVEL</p></td>
<td><p>输入或输出数据结构的版本不正确。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_PARAMETER</p></td>
<td><p>需要输出缓冲区，但它为<strong>NULL</strong>，或</p>
<p>output required 参数为<strong>NULL</strong> ，输出缓冲区太小，或</p>
<p>标准 TCP/IP 端口监视器不理解正在发出的命令。</p></td>
</tr>
</tbody>
</table>

 

 

 




