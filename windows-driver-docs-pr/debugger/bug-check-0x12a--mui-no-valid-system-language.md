---
title: Bug 检查 0x12A MUI_NO_VALID_SYSTEM_LANGUAGE
description: MUI_NO_VALID_SYSTEM_LANGUAGE bug 检查具有 0x0000012A 值。 这表示 Windows 未找到任何已安装的、 经过许可的语言包为系统默认 UI 语言。
ms.assetid: 6424FC7D-BD39-4F35-9E72-E9730D27CC24
keywords:
- Bug 检查 0x12A MUI_NO_VALID_SYSTEM_LANGUAGE
- MUI_NO_VALID_SYSTEM_LANGUAGE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUI_NO_VALID_SYSTEM_LANGUAGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 048a661a1b2009c99673d6a81a30379818db45f5
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520666"
---
# <a name="bug-check-0x12a-muinovalidsystemlanguage"></a>Bug 检查 0x12A：MUI\_否\_有效\_系统\_语言


MUI\_否\_有效\_系统\_语言错误检查的值为 0x0000012A。 这表示 Windows 未找到任何已安装的、 经过许可的语言包为系统默认 UI 语言。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="muinovalidsystemlanguage-parameters"></a>MUI\_否\_有效\_系统\_语言参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">检测的错误的子类型
<p>0x1:Windows 找不到任何已安装语言包在阶段我初始化。</p>
参数 2-NT 状态代码描述失败的原因。
<p>0x2:Windows 找不到任何已安装的、 经过许可的语言包的系统默认 UI 语言为内核缓存创建过程。</p>
参数 2-NT 状态代码描述失败的原因。
.</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">保留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




