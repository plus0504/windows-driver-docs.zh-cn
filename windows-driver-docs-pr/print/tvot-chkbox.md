---
title: TVOT\_CHKBOX
description: TVOT\_CHKBOX
ms.assetid: 66e9879e-c101-4367-b1ee-0746e6a71bc3
keywords:
- TVOT_CHKBOX 打印设备
topic_type:
- apiref
api_name:
- TVOT_CHKBOX
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6335ca9337cf1d39f19cfd62bd12ce3f5927b05a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845258"
---
# <a name="tvot_chkbox"></a>TVOT\_CHKBOX


## <span id="ddk_tvot_chkbox_gg"></span><span id="DDK_TVOT_CHKBOX_GG"></span>


TVOT\_CHKBOX 选项类型包括分组框中的复选框。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)构造  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
未使用。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)结构数组（ [**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)的**pOptParam**成员）  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
未使用。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
标识要与复选框关联的图标。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
未使用。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)构造  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**类别**  
TVOT\_CHKBOX

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**计**  
1

<span id="Style__________"></span><span id="style__________"></span><span id="STYLE__________"></span>**样式**   
未使用。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
如果[**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)中的**pDlgPage**标识 CPSUI 提供的页面，或[**DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)中的**DlgTemplateID**标识 CPSUI 提供的模板，则不使用**BegCtrlID** 。

否则， **BegCtrlID**必须包含按顺序编号的控件标识符集的第一个控件标识符。 控件标识符必须标识以下 Windows 控件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>控件标识符</th>
<th>Windows 控件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容</p></td>
<td><p>分组框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 1</p></td>
<td><p>标题文本</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 2</p></td>
<td><p>复选框</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>复选框图标</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 4</p></td>
<td><p>"扩展" 复选框或扩展的 "推送" 按钮（可选）</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>"扩展" 复选框或 "扩展" 推送按钮图标（可选）</p></td>
</tr>
</tbody>
</table>

 

有关其他信息，请参阅[自定义 CPSUI 支持的窗口控件](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-cpsui-supported-window-controls)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Compstui （包括 Compstui）</td>
</tr>
</tbody>
</table>

 

 




