---
title: DIF_NEWDEVICEWIZARD_POSTANALYZE
description: DIF_NEWDEVICEWIZARD_POSTANALYZE
ms.assetid: 81d609e6-9562-4738-b3ba-c29b24612f91
keywords:
- DIF_NEWDEVICEWIZARD_POSTANALYZE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_POSTANALYZE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf4653ff7b50fb5d3b81562936d9444c0a74377a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387044"
---
# <a name="difnewdevicewizardpostanalyze"></a>DIF_NEWDEVICEWIZARD_POSTANALYZE


DIF_NEWDEVICEWIZARD_POSTANALYZE 请求可让安装程序提供的 Windows 设备节点之后向用户显示向导页 (*devnode*) 注册，但在 Windows 安装设备驱动程序之前。 在手动安装的非 PnP 设备期间，才使用此请求。

### <a name="when-sent"></a>发送时间

Windows 注册设备，从而使之前 devnode"活动状态，"但之后将 Windows 安装设备的驱动程序。

### <a name="who-handles"></a>谁处理

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>类共同安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
<tr class="even">
<td align="left"><p>设备共同安装程序</p></td>
<td align="left"><p>不处理</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>安装程序输入

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_NEWDEVICEWIZARD_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)与关联结构*DeviceInfoData*。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改中设备安装参数的标志。 Windows 不会检查此 DIF 请求完成后的标志。 但是，它将检查它们在安装过程中更高版本。

<a href="" id="class-installation-parameters"></a>类的安装参数  
安装程序可以修改[ **SP_NEWDEVICEWIZARD_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)提供自定义页面。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序不处理此 DIF 请求会返回 NO_ERROR 从其预处理阶段。 如果共同安装程序将处理此请求它可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

类安装程序返回 NO_ERROR，如果它已成功提供页面。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

DIF_NEWDEVICEWIZARD_POSTANALYZE 请求可让安装程序提供注册 devnode 后但在 Windows 安装设备驱动程序之前，Windows 向用户显示的向导页。 在手动安装的非 PnP 设备期间，才使用此请求。

如果安装添加自定义 postanalyze 页面，安装程序应首先检查是否**NumDynamicPages**类安装参数已达到 MAX_INSTALLWIZARD_DYNAPAGES。

之后用户可单击**下一步**在自定义的页上，Windows 安装设备的驱动程序和 PnP 管理器启动设备。 Postanalyze 向导页是安装程序来完成工作所加载的驱动程序和设备启动之前的最后机会。

安装程序应提供 Wizard 97 标头标题和自定义向导页的 PROPSHEETPAGE 结构中的标头副标题。 安装程序不应取代系统提供向导标题。 请参阅 Microsoft Windows SDK for PROPSHEETPAGE 结构的文档和有关属性页的详细信息。

有关差异代码的详细信息，请参阅[处理 DIF 代码](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Microsoft Windows 2000 和更高版本的 Windows 支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h （包括 Setupapi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DIF_NEWDEVICEWIZARD_PREANALYZE**](dif-newdevicewizard-preanalyze.md)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](dif-newdevicewizard-preselect.md)

[**DIF_NEWDEVICEWIZARD_SELECT**](dif-newdevicewizard-select.md)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

[**SP_NEWDEVICEWIZARD_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)

 

 






