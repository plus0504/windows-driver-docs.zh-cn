---
title: KSPROPERTY\_音频\_3D\_接口
description: KSPROPERTY\_音频\_3D\_接口属性指定了用于处理声音缓冲区中的数据的3D 算法。
ms.assetid: 76c56e61-23ef-43ad-b66b-2412fd247b6e
keywords:
- KSPROPERTY_AUDIO_3D_INTERFACE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_3D_INTERFACE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f40ff187306401a7357351063eff2de5b6377d1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831128"
---
# <a name="ksproperty_audio_3d_interface"></a>KSPROPERTY\_音频\_3D\_接口


KSPROPERTY\_音频\_3D\_接口属性指定了用于处理声音缓冲区中的数据的3D 算法。

## <span id="ddk_ksproperty_audio_3d_interface_ks"></span><span id="DDK_KSPROPERTY_AUDIO_3D_INTERFACE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定3D 算法的 GUID。 此值可以是头文件 Dsound 中的以下 Guid 之一：

-   DS3DALG\_默认值

-   DS3DALG\_不\_虚拟化

-   DS3DALG\_HRTF\_FULL

-   DS3DALG\_HRTF\_

有关这些 Guid 的详细信息，请参阅 Microsoft Windows SDK 文档中的 DSBUFFERDESC 结构的**guid3dAlgorithm**成员的说明。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_3D\_接口属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md)

 

 






